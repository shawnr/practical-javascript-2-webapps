# Exploring an API
Whenever we begin using a new data API, it's good to spend a little time exploring the API documentation and trying requests using an API browser tool like [Postman for Google's Chrome browser](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop?hl=en).

![Postman for Google Chrome Interface](img/postman1.png)

Postman allows us to construct HTTP requests to any API. We can set necessary headers, query parameters, form data, and more. Results are clearly displayed so we can truly begin to understand the shape of the data that comes back from the API. Each API will deliver a different type of data object, and all the attributes contained in these responses become available to us inside our application once we set up our API calls correctly. 

That means we can use an API browser tool to get a clear view of what information exists in the data coming back from your API service. Since the API data objects are translated directly into JSON objects in our application, we can easily see how to access the specific information we require for your purposes. 

These tools also help us form proper API requests. If our request is not properly formed, then we will not get the data we need back from the API service. Luckily, modern JavaScript modules make it easy to create basic requests, but it can still be tricky to work out how to form our request in the first place. A good API browser tool will help us formulate correct requests and will allow you to know exactly what you are getting back. You can even use it to help test edge cases and learn how the API responds if, for example, you send some data value it does not expect.

[The Postman Documentation site](https://www.getpostman.com/docs) has a lot of useful information, tutorials, and guides for using Postman to explore API services. We should read up on how to use this tool, or find a similar tool you prefer and use that one. It is very essential to have a way to view the data coming into your app, and to test your app's API queries, apart from your custom Javascript code.

## Exploring an API With Postman
We can plug in API URls and explore them in Postman. Let's practice with a common placeholder resource for API content, [JSON Placeholder API](http://jsonplaceholder.typicode.com/). We can see from the documentation on their homepage that they offer a few different API endpoints to experiment with. We will experiment with the `/posts/` endpoint in these examples.

First, let's set up a query to `http://jsonplaceholder.typicode.com/posts`. We should make this a `GET` query, and we do not need to supply any additional parameters or authentication. Paste the API URL into the location box and click Send. We should see a result that looks something like this:

![Postman Query](/img/postman1.png)
<br>Postman Query

We can see in this image that we have received a response that is an array of JavaScript objects representing the "posts". These posts are described using JSON notation, so we should recognize the structure of the information. We can see that each post object has `userId`, `id`, `title`, and `body` properties. 

We could alter our query by clicking the "Params" button in Postman to reveal a way to set key/value pairs that will be translated into the query string of the API URL. If we click the Params button we can set the `userId` value to `2`. This will perform an API request that will only fetch the posts that have been authored by the user with the `userId` of `2`. Here is what that looks like:

![Postman Query for userId 2](/img/postman2.png)
<br>Postman Query for `userId=2`

As we can see, the results have changed so that they all have the same `userId` value. This is a common way for APIs to filter results according to our request. Other APIs will reveal different information and will accept different parameters. It's worthwhile to test out any API we plan to work with using a tool like Postman in order to get a feeling for the way the API works. Although most APIs adhere to the rules of RESTful API design, each API is still a unique system with its own quirks and features.

## Using other APIs
You can use the patterns described in this book to use any other REST API that serves JSON results. There are many, many APIs that fit that description. Some APIs require you to do more arduous authentication or to have your app approved before you will be granted developer privileges. Other APIs have steep charges for using them, and although you may be able to develop against them reasonably it would be prohibitively expensive to release a website using that API. These considerations and more should inform your decision as you look for APIs.

[The Suggested API List in Appendix B](/appendices/appendix-b-api-suggestions.md) of this book is a great place to find other APIs worth trying out.

