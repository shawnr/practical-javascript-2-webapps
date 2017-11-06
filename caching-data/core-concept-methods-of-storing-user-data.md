# Core Concept: Methods of Storing Frontend Data

There are several methods made available to us for storing data on the frontend (in the browser). These include [cookies](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies), [session storage](https://developer.mozilla.org/en-US/docs/Web/API/Window/sessionStorage), [local storage](https://developer.mozilla.org/en-US/docs/Web/API/Storage/LocalStorage), [IndexedDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API/Basic_Concepts_Behind_IndexedDB), and Web SQL (which is [deprecated](https://www.html5rocks.com/en/tutorials/webdatabase/websql-indexeddb/), so we won't be covering it). All of these technologies get wrapped up into the ["Storage"](https://developer.mozilla.org/en-US/docs/Web/API/Storage) concept in the browser, which seeks to unify the many methods of storing information on behalf of the user.

Later in this section of the book, we will work with `localStorage` to improve the functionality of our webapps. But let's first look at how each of these technologies works, and what we use it for.

## Cookies

One of the oldest tools for storing information in the browser on behalf of the user is the "cookie." [Cookies](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies) have often been maligned in mainstream media, and reliance on cookies can be problematic in some cases, but these have always been useful tools for storing small pieces of information. We often use cookies to store a "logged in" token for a user, so they do not have to login each time they return to the site. We control that cookie with the "remember me" checkbox that is on so many login forms around the web.

We also use cookies to store other small bits of information, such as site preferences or tokens. Since cookies can contain just about any blob of text data, they can be used to store all sorts of information (such as tracking numbers, passwords, etc.). These uses are regulated in some areas, such as in the EU where a site must make us aware if they are using cookies. 

Cookies are tied to the domain that set the cookie in the browser. Domains can only read cookies associated with them, and when a user hits a domain that corresponds to a stored cookie, then the cookie is automatically sent to that domain.

Cookies default to existing for the duration of the user's session on the server, and they will disappear when the user closes their browser. However, it is possible to specify an expiration date for a cookie, allowing it to be "permanent" until that specified date. This is how cookies used for maintaining login states work: They are set for some period of time, after which the user must login again to re-establish a new cookie.

It is possible to increase the security of cookies by marking them "secure" or "HTTP Only." These denotations help systems maintain a higher level of security around the cookie, but they should never be considered fully secure. Sensitive data should **never** be stored in a cookie.

There are many known security issues with cookies. Cross-site scripting (XSS) attacks can be used to harvest cookies from sites where the cookies have been set to secure and/or HTTP Only. Cross-site request forgery (CSRF) attacks can be used to execute a request on a third-party site on behalf of the user without them being aware of the request. In both cases, it is possible to prevent this abuse, and many application frameworks and tools take these risks into account.

Cookies are still a commonly-used technique in the web development landscape, but they are limited in how useful they can be. For the purposes of persisting sessions and tracking lightweight configuration data, they can be helpful. But they are not meant to store lots of information and they are not secure enough to store sensitive information.

## `localStorage` and `sessionStorage`
A common replacement for cookie storage is to use [`localStorage`](https://developer.mozilla.org/en-US/docs/Web/API/Storage/LocalStorage) and [`sessionStorage`](https://developer.mozilla.org/en-US/docs/Web/API/Window/sessionStorage). These forms of [storage](https://developer.mozilla.org/en-US/docs/Web/API/Storage) are revealed through the JavaScript API and accessible to our web applications. It is common to use third-party tools to provide helpful features for managing our storage options, but it is not necessary.

The main difference between `localStorage` and `sessionStorage` is that `localStorage` is persistent (meaning it exists even after the user closes the tab/browser and then returns to the site at a later date), while `sessionStorage` goes away when the user ends their session. Because of the ability of `localStorage` to persist across sessions, it is an ideal tool for caching information in the browser that the user will need on subsequent sessions.

Both forms of storage allow us to create "key/value pairs", which means that we can give a name (the "key") to a "value" (which can be any String information). Since we can reduce any data to a String, we can store any data structure in these storage options. We can turn JSON data into a String using [`JSON.stringify`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify) and we can turn the string back into a JSON object using [`JSON.parse`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse).

A variety of third-party tools allow us to move between `sessionStorage` and `localStorage` and give us built-in features to manage the manipulation of data into and out of String formats. These tools (such as [`vue-ls`](https://github.com/RobinCK/vue-ls)) can make it very easy to use these storage mechanisms in our applications to cache API data and store user-generated information. We can allow a lot of functionality in our applications even if the network is not available by caching information on behalf of our users. 

We should keep in mind that these storage mechanisms are all susceptible to user manipulation. Users can clear their browser data at any time, which will wipe out any information stored in `localStorage` or `sessionStorage` (or cookies, for that matter). As developers, we must take care to provide mechanisms to detect and restore cached data when the user clears it, and we should never leave the user with a broken application because we assume too much about what data will exist in storage.

## IndexedDB

Cookies are good for storing tiny bits of information: A 32-bit token, a handful of interface preferences, etc. The storage mechanisms are good for storing larger chunks of data in individual keys, which is useful for things like caching user profiles, individual API responses, or lists of data objects created by the user. But what about when we want to cache significant amounts of data in the browser for the user? What if we want to provide a quality experience for the user to browse their movie collection or email while they are offline? These other methods will not suffice.

This is where the [IndexedDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API/Basic_Concepts_Behind_IndexedDB) technology comes into play. IndexedDB is a non-relational database technology that stores key/value pairs. Unlike the key/value pairs of the storage mechanisms, IndexedDB can store complex objects as the value, and properties of those objects can be used to create "indexes" in the system. The indexes provide faster methods of searching the data in an IndexedDB, and developers can use complex queries to get exactly the data they need at any given time.

The IndexedDB gives database abilities on par with any other non-relational database. This database is suitable for storing large data sets that can even contain images or files. A user could store the data about their entire movie library, their book collection, or their emails, and that data could be referenced even when the network is not available. An email client can use IndexedDB to support an offline mode and to speed functions for the user. A todo list could use IndexedDB to allow for offline functionality so it even works inside buildings with no mobile signal. 

IndexedDB databases are tied to a specific domain and implement a "same domain policy," which means they can only be accessed by code running at the location where they were created. This means that a malicious site cannot reach into the data of any other site for nefarious purposes. Although IndexedDB databases are safe(r) from hacking, they are still vulnerable to user manipulation.

The user is always in control of the data on their computer, and they can easily wipe out any IndexedDB database. This means that care should always be taken to build proper synchronization routines into web software to rebuild the database in the event of corruption or deletion. It also means that the IndexedDB database should never be the primary source of information for a website or application. It is a caching tool to provide additional user convenience, but not a substitute for a proper data storage system.












