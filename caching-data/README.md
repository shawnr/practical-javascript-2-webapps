# Caching Data

As frontend developers, we do not need to do much with the creation of databases and management of those systems. We typically interact with those systems through established means, especially in the world of single page applications that use APIs to provide the bulk of their functionality. Although the API itself is an application running on a server, and most APIs deal with the retrieval of information from a database, as frontend developers our challenge is primarily to get to know the data and features the API provides.

Although we get a bit of a break in terms of designing data models and managing database systems, we do have a set of challenges that uniquely affect the frontend: How can we leverage tools for caching information in order to make our applications more performant and friendly to API providers?

"Caching information" in the web application context refers to the process of saving a copy of data so it can be accessed without making another network request. Saving data locally provides many opportunities for us to improve our websites and applications, and to provide a more efficient user experience.

Most API providers limit the frequency with which we can make API requests. If we have established a private API server to handle the functions of our product system, then we have a vested interest in minimizing the impact we put on that system in order to stretch our resources further and provide speedier responses. We want to provide a higher level of convenience for our users, so they do not have to re-configure the system or re-enter data required by the system. We also want to be smart about when we make a request to a remote API server, preferring to avoid those calls when possible.

We can accomplish these goals using some basic tools provided in the browser and made available through JavaScript. We can even leverage some helpful modules to enhance those core features so we can more effectively work with the tools provided by the browser. These tools allow us to store data and retrieve it without making a network request.

As with many aspects of web development, there are multiple ways of approaching the task of saving information about the user and/or caching API responses. In this section we will explore a couple of them.