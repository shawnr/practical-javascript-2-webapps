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

In modern JavaScript applications, there is a bit of trickiness around managing URLs. The concept of the URL was designed to point to a specific piece of content online. But in most dynamic web applications (including single page applications written in JS), the URLs do not map directly to content on the server. Instead, the URL is actually telling the web application how to process the request. 

In the examples above, the `/login` URL does not correspond to a directory named `login` on the server. The `/login` URL corresponds to a route definition that says, "When this route is hit, render the login view." The web application then processes that view, renders HTML custom for that user, and then shows that HTML to the user in the browser. Even in a Python or Ruby server-side web application, the URLs do not map to files on the server.

### Hash Mode
To make this work for single page JS applications, we use two major techniques. The first technique, which is the most common and requires no significant server support, is the "hash" approach. This writes all URLs using a hash mark:

```html
http://example.com/#/login
```
This works in all browsers because the `#` symbol is seen as an internal page reference. This is the same syntax we would traditionally use to reference a specific element in the page by ID:

```html
<a href="#map">Jump to the Map</a>

... lots of HTML content ...

<h2 id="map">Map</h2>
... a map ...
```

In the example above, we see how the hash is traditionally used. To link directly to the map on this page, we could use the link: `http://example.com/#map`. 

When working with a single page JS application, we abandon this technique for internal page links. Instead, we use the hash to denote a location in the application itself. This is a tradeoff we're willing to make, and we can still scroll users to internal page content using other approaches.

### History Mode
The alternative approach is to utilize the HTML5 History API, which allows us to create "normal" links:

```html
htp://example.com/login
```

This approach works fine in all modern browsers, and it produces a somewhat "cleaner" look to the URL (no hash mark or extra punctuation). In order to use this approach in a single page application, we must be deploying on a server that will ignore the paths after the domain and send all traffic to the same `index.html` file. We can configure any server software to allow for this, so it's a matter of setting up Apache or nginx or whatever other server we're using to, itself, properly route requests. Here is an example Apache configuration from the Vue-Router documentation:

```bash
<IfModule mod_rewrite.c>
  RewriteEngine On
  RewriteBase /
  RewriteRule ^index\.html$ - [L]
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteRule . /index.html [L]
</IfModule>
```

Although we won't dive into the details of configuring the server to support history mode in this book, we can appreciate that in the example above the Apache configuration has been set up so that all requests will be sent to `/index.html`. In the case of a single page application, this is the correct way to handle the requests.

It's worthwhile to mention that this is also basically what server-side applications do when they are serving dynamic HTML content. The server is configured to hand off all user requests to the application itself, which then constructs the proper response based on analysis of the URL. In this example taken from the Django Project website, we can see that the same basic idea is at play:

```bash
WSGIScriptAlias / /path/to/mysite.com/mysite/wsgi.py
WSGIPythonHome /path/to/venv
WSGIPythonPath /path/to/mysite.com

<Directory /path/to/mysite.com/mysite>
<Files wsgi.py>
Require all granted
</Files>
</Directory>
```
In the case of a Django app, the WSGI standard is used. Each Django app contains a `wsgi.py` file that handles the requests that come in. When deploying a Django application, we configure Apache to hand off all requests to the `wsgi.py` file.

Again, these examples are intended to illustrate the similarities of how we handle these problems across different technologies. Although the specifics vary, the core concepts are largely the same. In the next sections we will look more closely at how to set up routing in our Vue.js applications.



