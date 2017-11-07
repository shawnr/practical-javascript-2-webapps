# Caching Data from APIs
When we work with APIs we often run up against API "rate limits." Most API providers do not want developer applications to hit their API endpoints more than necessary. Extra requests to an API create additional delay for our users, and they potentially impact the performance of the API server, causing delays for other users as well. It is both neighborly and pragmatic to do what we can to minimize the number of API requests that we make to a server.

We can reduce the number of API calls we make to a server by caching responses. When working with RESTful APIs, each unique request can be cached. Depending on the API, we might not expect the data to change very often, so we can usually cache the data returned by the API for some period.

For example, an API that provides access to an encyclopedia of data (such as all the Pokémon or everything about Star Wars) is unlikely to update very often. Most weather APIs publish a refresh window that is 15 minutes or more. Whatever we are building, there is a good chance that we could delay the refresh of data by some amount of time.

This is especially relevant when we put an API call on a `created ()` function in our components. These components are designed to show data, so they must request the data when they are instantiated, but they do not always need to make a call to the API server. If we consider how many times we might refresh our page in the browser during development, we can see how quickly we could eat up any API rate limit that might apply.

## Determine How Often
Figure out how often your API needs to refresh. If you are making calls to create new data on a system (such as submitting a new blog post), then obviously that call needs to be made whenever the user clicks "save." But if we are making calls to retrieve weather data, we do not need to refresh any given API call for at least 15 minutes. 

Each data set will have a different refresh rate depending on what data it is using. Each API will also have a different rate at which they publish new information. Be sure to consult the API documentation and use some well-reasoned consideration to determine an interval for caching API data.










