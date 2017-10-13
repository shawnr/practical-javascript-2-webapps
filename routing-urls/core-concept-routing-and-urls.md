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

## URLs in Modern JavaScript Applications





