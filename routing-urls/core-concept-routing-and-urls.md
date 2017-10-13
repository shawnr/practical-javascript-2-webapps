# Core Concept: Routing and URLs
The concept of routing to control what the user sees in our web applications is common and pervasive. Whether we're using a backend framework like Django or Rails, or a frontend framework like Angular or Vue.js, we are probably implementing some form of routing. This notion of creating "routes" is a physical metaphor for moving users through our applications. We want to provide pathways to locations in our applications. Those locations are denoted by URLs. Given the nature of the Web, URLs are beneficial to us in many ways.

Working with routing in an application can be simple or complex. In this section we will talk about routing in more general terms, then we will look at how to implement routes in our applications in the following sections. Later in the book we will explore more complex approaches to routing afforded to us by virtue of using Vue.js, but for now we will focus on the fundamentals.

## What URLs Do
The URL is one of the fundamental building blocks of the web. It is a "universal resource locator" that allows us to reference the network location of any file, directory, or server. We can bookmark URLs, share them with people via email or messaging, and rely on the consistency of the information we find at a URL. URLs often explain to us what they are all about:

```
http://www.imdb.com/title/tt4846340/
```

From this URL we can tell a lot about the site: It's not using any encryption when sending data. It is located on the `www.imdb.com` server. We can look at the path and see that this is the URL for a specific `title` with the ID `tt4846340`. This is a common way to form URLs with a path that includes the content type and a content item ID. 

If we look at URLs from our favorite websites, we will probably see that they use similar labeling methods. The idea of using an ID or some other representative label (often called a "slug" in web development terminology) is extremely common. A URL like this tells a savvy user what they can expect to see on that page.

URLs provide a way for us to identify content online. They provide a way for us to save that location (because they are simple text that can be saved in myriad ways). They provide us a way to share content. And they give us a better understanding of what we are looking at on any given website. 

## Routing Views
When we talk about routing the user, we will also talk about the "view" that each route leads to. This is akin to a "page" in traditional websites, but since we are working with a single page application framework we do not use traditional pageviews. Instead, our views are more representative of the "state" of the application: Where is the user right now? What are they doing here?

Defining routes and the views they associate with looks different in different technologies, but they typically include a few key details:

* The URL pattern that the application is trying to match
* The view that should be rendered when the URL is matched
* Additional information needed to render or use the view (this is probably optional and used in specific cases)

In a backend technology like Django, the routing setup (which they call `urlpatterns`) looks like this:

```python
from django.conf.urls import url

from . import views

urlpatterns = [
    url(r'^/$', views.home),
    url(r'^login/$', views.login),
    url(r'^register/$', views.register),
    url(r'^user/(?P<username>\w+)/$', views.user_profile),
]
```
In a Vue.js application, a routing setup looks like this:

```js
const router = new VueRouter({
  routes: [
    { path: '/', component: Home },
    { path: '/login', component: Login },
    { path: '/register', component: Register },
    { path: '/user/:username', component: User }
  ]
})
```

We can compare these two route definitions and see that they essentially define the same navigational structure: There is a home view, a login view, an a registration view. Those URLs are defined so that they are not looking for any additional information. Then there is a user profile view that requires a route parameter: the user's username. The username is required so the profile view can make use of the logged-in user's profile data. It is common to use route parameters to allow a view to fetch the proper data. We see these when reading news articles, viewing videos, or interacting with almost any piece of content online.

This kind of navigational structure is mirrored on millions of sites online. Each site, depending on what technology powers it, probably uses a similar system for routing requests. In a large site, the route configuration can become very large, so there are sometimes ways of breaking up route definitions or organizing them to be more efficient. 

## URLs in Modern JavaScript Applications





