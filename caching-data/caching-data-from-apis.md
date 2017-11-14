# Caching Data from APIs
When we work with APIs we often run up against API "rate limits." Most API providers do not want developer applications to hit their API endpoints more than necessary. Extra requests to an API create additional delay for our users, and they potentially impact the performance of the API server, causing delays for other users as well. It is both neighborly and pragmatic to do what we can to minimize the number of API requests that we make to a server.

We can reduce the number of API calls we make to a server by caching responses. When working with RESTful APIs, each unique request can be cached. Depending on the API, we might not expect the data to change very often, so we can usually cache the data returned by the API for some period.

For example, an API that provides access to an encyclopedia of data (such as all the Pokémon or everything about Star Wars) is unlikely to update very often. Most weather APIs publish a refresh window that is 15 minutes or more. Whatever we are building, there is a good chance that we could delay the refresh of data by some amount of time.

This is especially relevant when we put an API call on a `created ()` function in our components. These components are designed to show data, so they must request the data when they are instantiated, but they do not always need to make a call to the API server. If we consider how many times we might refresh our page in the browser during development, we can see how quickly we could eat up any API rate limit that might apply.

Of course, storing API data isn't our only problem. We also need to be able to know when our data was cached and clear it if it gets too old. This is often referred to as telling the difference between a "fresh" and "stale" cache. For user-generated data, we want to keep the information around forever. But for API data, we want to expire the cache when needed.

<div class="tip-box">
  <h3>Caching vs. Browser Cache</h3>
  <p>It's worthwhile to note that when we discuss caching throughout this section, we are talking about the general concept of storing data that will be referenced again later. This is the definition of the term "caching" as we mean it. A "cache" is some store of data that can be referenced by an application. This is a general concept in computing, and we find caches of data stored all over our systems for use by all different software.</p>
  <p>In the browser, we also have a "browser cache," which we think about often because we must "clear the cache" when we have issues with web pages. The reason we "clear" the cache is to delete the stored data, which in the case of web pages can sometimes cause problems (especially as we develop new features). This browser cache is used to speed up websites in a variety of ways, so it will do all kinds of things to try to store requests and avoid repeating them. This is helpful, but it's not what we are working with when we use cookies,  localStorage, sessionStorage, or IndexedDB.</p>
</div>

## Determine How Often
We must figure out how often our API needs to refresh. If we are making calls to create new data on a system (such as submitting a new blog post), then obviously that call needs to be made whenever the user clicks "save." But if we are making calls to retrieve weather data, we do not need to refresh any given API call for at least 15 minutes. 

Each data set will have a different refresh rate depending on what data it is using. Each API will also have a different rate at which they publish new information. Be sure to consult the API documentation and use some well-reasoned consideration to determine an interval for caching API data.

Keep in mind that times in JavaScript are generally calculated using [`Date.now()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/now), which returns the number of milliseconds since the Unix epoch began. This number is precise (down to the millisecond), but it requires us to think in milliseconds when we are determining lengths of time. Because of this, we must calculate the times we need to compare.

For example, if we had a timestamp of `1510013577637`, we could check to see if 15 minutes has gone by like this:

```js
let timestamp = 1510013577637;
let cacheExpiry = 15 * 60 * 1000; // 15 minutes in milliseconds

if ( Date.now() < (timestamp + cacheExpiry) ) {
    console.log('Do not refresh cache.');
} else {
    console.log('Refresh cache. 15 minutes has passed.');
}
```
We calculate the 15 minute time difference by multiplying `15 * 60` to get the number of seconds, and then that number times `1000` to get the number of milliseconds. (There are 1000 milliseconds in a second.) This kind of calculation allows us to easily determine the difference in time and make decisions based on that difference. If we needed to do more complex calculations (like number of days) we could calculate new [`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) objects and use the methods provided there to add/subtract days, weeks, or months. But we usually cache data for minutes or hours in our web applications.

## Make an Identifier
When we make an API request, or when we just store user data, we often need to construct a unique key. These are sometimes called "slugs" in web development lingo: a "safe" term that indicates one piece of data in the system. We use slugs to indicate blog posts, or items, or users, etc. The slug is a unique ID, and regardless of what we call it, that is the key piece of information we need to make caching work in our application.

Sometimes it's easy to make a unique ID. If I have an API to an endpoint that looks up a city's weather by City ID, then I can likely use the City ID as the unique identifier for the cache. There are many situations where we are looking up data by a single ID or a set of latitude and longitude coordinates, and those things are relatively easy to put together into a unique ID.

In other cases, we must combine several pieces of information into a unique ID. Let's once again consider [the `WordSearch` project](/visual-feedback/project-visual-feedback-and-enhancement.md) from the previous section of the book. In that application, we make a call to the Datamuse API, and it would be nice to cache those queries. But those queries have several data points the user can modify.

In order to cache those queries, we need to assemble a unique ID inside the `findWords` method:

```js
let queryID = `${this.phrase}-${this.soundsLike}-${this.startLetter}-${this.endLetter}`;
```
We have simply mashed together the unique elements into a query ID. We can then use that to establish the identifier for the cached data in `localStorage`. Care needs to be taken when determining a unique ID for any cache we try to store, but there is always a way to indicate a unique query.

## Implement Some Cache Checking
We can use more complex tools for caching API requests, and if we were writing an application with many requests then it would be recommended to use a more robust tool for caching API requests. But for our purposes here, we can manually manage our API requests and avoid making those requests if we prefer. To help us a little bit, we will rely on the `expiry` ability of the `vue-ls` module.

The `vue-ls` module allows us to specify an expiration time for information we store. This allows us to set the expiration time when we store the data and then we don't need to worry about clearing it later. We can set an expiry time in milliseconds that will allow us to expire our cached information without any additional effort. 

We can make the following changes to the `WordSearch` project:

```js
findWords: function () {
  this.results = null;
  let queryID = `${this.phrase}-${this.soundsLike}-${this.startLetter}-${this.endLetter}`;
  let cacheExpiry = 24 * 60 * 60 * 1000; // 24 hours cache duration
  console.log('queryID: ' + queryID);
  let cachedQuery = this.$ls.get(queryID);
  if (cachedQuery) {
    console.log('Previous query cache detected.');
    this.results = cachedQuery;
  } else {
    console.log('No cache detected for: ' + queryID);
    this.fetchAPIResults();
  }
},
fetchAPIResults: function() {
  this.results = null;
  let queryID = `${this.phrase}-${this.soundsLike}-${this.startLetter}-${this.endLetter}`;
  let cacheExpiry = 24 * 60 * 60 * 1000; // 24 hour word search cache.
  axios.get('https://api.datamuse.com/words', {
    params: {
      ml: this.phrase,
      sl: this.soundsLike,
      sp: `${this.startLetter}*${this.endLetter}`
    }
  })
  .then( response => {
    this.$ls.set(queryID, response.data, cacheExpiry); // Cache the API response for 24 hours
    console.log('Cache created for: ' + queryID);
    this.results = response.data;
  })
  .catch( error => {
    this.errors.push(error);
  })
}
```
We have separated the API call out of the `findWords` method, and moved it to the `fetchAPIResults` method. The `findWords` method now tries to load the data from the cache, and if it can find no cache then it will execute the `fetchAPIResults` method. The `fetchAPIResults` method now also saves the results into `localStorage` before it sets `this.results` equal to `response.data`. We are applying a 24 hour expiry to the information stored in `localStorage`. After 24 hours, the data will no longer be available in `localStorage`, and the API request will happen again.

This kind of caching will greatly reduce the number of queries we send to the API server. Many API services require some form of request caching on the application side in order to minimize the load on the server itself. This not only helps the API server, but it also saves our users from repetitive waits as they move around inside our application.












