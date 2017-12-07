# Appendix B: API Suggestions

This book includes several sections dedicated to using third-party APIs in order to have access to dynamic data that is useful to a user. There are many APIs in the world, but not all of them are easy to use or friendly towards JavaScript applications. Some APIs require complex authentication in order to use them which is beyond the scope of this book. Other APIs are designed only to be used by certain types of systems and might cause issues when used with a JavaScript application in the browser.

The following APIs have been reviewed for use with the kinds of code we cover in this book. They should provide decent fodder for experimentation and minimal barriers to entry.

## No API Key Required
<ul>
<li><a href="http://jsonplaceholder.typicode.com/">JSON Placeholder API</a></li>
<li><a href="https://www.datamuse.com/api/">Datamuse Word API</a></li>
<li><a href="https://swapi.co/">Star Wars API</a></li>
<li><a href="http://www.pokeapi.co/">Pok&eacute;mon API</a></li>
<li><a href="https://yesno.wtf/">Yes/No API</a></li>
<li><a href="https://affiliate.itunes.apple.com/resources/documentation/itunes-store-web-service-search-api/">iTunes Search API</a></li>
<li><a href="https://sunrise-sunset.org/api">Sunrise/Sunset API</a></li>
<li><a href="https://randomuser.me/">Random (fake) User Data API</a></li>
<li><a href="https://anapioficeandfire.com/">Game of Thrones API</a></li>
<li><a href="http://open-notify.org/Open-Notify-API/ISS-Location-Now">Location of International Space Station API</a></li>
<li><a href="http://open-notify.org/Open-Notify-API/People-In-Space">Number of People in Space API</a></li>
</ul>

## API Key Required

<ul>
<li><a href="https://developers.soundcloud.com/docs/api/guide">Soundcloud API</a></li>
<li><a href="http://openweathermap.org/api">Open Weather Map API</a></li>
<li><a href="https://www.flickr.com/services/api/">Flickr API</a></li>
<li><a href="https://www.omdbapi.com/">Open Movie Database API</a></li>
<li><a href="https://developers.google.com/books/docs/v1/getting_started">Google Books API</a></li>
<li><a href="https://developer.spotify.com/web-api/user-guide/">Spotify API</a></li>
<li><a href="https://www.themoviedb.org/documentation/api">The Movie Database API</a></li>
</ul>

## Cross-Origin Proxies
Some of the APIs listed here do not allow direct requests from JavaScript due to [Cross-Origin Resource Sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing) restrictions. CORS is a concept that keeps browsers more secure by limiting the ways that JavaScript can communicate with third-party servers, possibly without the user's knowledge. Some APIs allow developers to configure the domain their apps are hosted on, which then allows the API service to provide the correct CORS headers to allow communication directly through the API. Other API services, such as the Datamuse service, allow all domains to access their server, so there is no need to fuss with domain configurations.

When attempting to use an API that does not allow domain configurations necessary for CORS to allow the API requests, it is necessary to use a "cross-origin proxy." These proxies use a server-based application to pass requests through to the API service and then relay responses back to the user's browser. There are two cross-origin proxies we suggest for new developers attempting to experiment with APIs using JavaScript:

* [Crossorigin.me](https://crossorigin.me)
* [Rashrewind.com](http://rashrewind.com)

Either of these proxies will work in most cases, although they do function slightly differently, so some situations may warrant choosing one over the other. These proxies will only allow GET requests, so it is impossible to use some features of some APIs that require POST or PUT requests. In order to protect the security of our user's data, **we should never send sensitive or confidential information through these public proxies.**

The list of APIs above was largely drawn from [Terence Eden's list here](https://shkspr.mobi/blog/2016/05/easy-apis-without-authentication/).