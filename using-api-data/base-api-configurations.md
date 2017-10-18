# Base API Configurations
It is common for us to write JavaScript applications that use the same API in multiple components. If we refer back to the illustration for Service Oriented Architecture, we can imagine a single page application that would need to perform multiple API requests to different URLs on a single domain. It's also very common for API services to require some API key or other authorization token to allow access to the API.

![Service Oriented Architecture](/img/soa.png)
<br>Service Oriented Architecture

In these cases, it becomes repetitive and error-prone to repeat the code required to add the correct authorization headers or query string parameters. We want to avoid repeating ourselves as much as possible. This can be accomplished by setting up a base API configuration that we can use to build every other API request.















