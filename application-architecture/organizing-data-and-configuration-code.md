# Organizing Data and Configuration Code
As we work on different parts of our applications, we often find that we have similar needs in different places. We might have specific formatting we want to remain consistent across templates, or system data that needs to be available to different components. We might find that we are making API requests to the same API in different components and we want to minimize the amount of repetitive code we are using. In each of these cases, what we absolutely want to avoid is duplicating the same data or logic in multiple locations.

As we saw in previous sections, we will make our applications easier to maintain, build, and enhance if we can adhere to a clean separation of concerns and utilize some common strategies for managing components that need to be reused throughout the application. In this section we will look at some techniques for organizing reusable pieces of our system.

<div class="tip-box">
  <h3>ES6 Modules</h3>
  <p>The Vue CLI setup we have been using supports ECMAScript 6 (ES6) and uses a tool called Babel to provide some level of backwards compatibility for browsers that do not yet support ES6 features. Luckily, most of the browser market and related technologies now fully support ES6 features, which opens the door for us to improve how we write code. (For developers who are unaware, ECMAScript is the standard that governs JavaScript so the two names should be synonymous, although they often are not.)</p>
  <p>One powerful feature of ES6 that we will make extensive use of in this section is the creation, export, and import of "modules." JavaScript has had a notion of modules for awhile now: It was first created using external libraries like RequireJS and AMD, and then it made its way to ES5. But the latest version of modules in JavaScript is a major improvement and allows for techniques like those described in this section.</p>
  <p>We can learn more about using modules to export and import components in our software on the Mozilla Developers Network pages for <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import">Import</a> and <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export">Export</a>, respectively. There are <a href="https://hackernoon.com/import-export-default-require-commandjs-javascript-nodejs-es6-vs-cheatsheet-different-tutorial-example-5a321738b50f">many</a> <a href="https://medium.com/dailyjs/es6-modules-node-js-and-the-michael-jackson-solution-828dc244b8b">other</a> <a href="http://exploringjs.com/es6/ch_modules.html">great resources</a> to explore online, and more will be created in the near future, too. Seize the power of this new modules system to make our apps as powerful as possible.</p>
</div>

## Common Data Techniques
A common case that often comes up is the need to store system-specific data that can be accessed from any component. This is often used for sets of static metadata that are specific to the project and which are not subject to change. These are usually considered "constants" in the system: They are not meant to be altered by the user or to change during the use of the application or site.

Since we can easily import objects into our components, all we need to do is make sure we have properly structured our data file to export an object. We can store these files wherever makes sense: a `/common/` directory in our `/src/` directory, a well-named file, or somewhere else within the project.

Here is an example of a data file that can be imported into a Vue.js component. Assume this code is in the file `/src/common/constants.js`.

```js
export default {
    'metadataProperty': 'Some value',
    'someChoices': [
        { name: 'Choice One', value: 1 },
        { name: 'Choice Two', value: 2 },
        { name: 'Choice Three', value: 3 }
    ]
}
```
We could make use of this data object by importing it into a Vue.js component:

```html
<script>
import SystemData from `@/common/constants.js`;

export default {
  name: 'demoComponent',
  data () {
    return {
      formOptions: SystemData.someChoices
    }
  }
}
</script>
```

As we've seen in previous projects and examples, we can import the content of `constants.js` with the name `SystemData` inside our component. We can then use that data however we would like within our component logic. In this case, we have set the component's `formOptions` value to the `SystemData.someChoices` array. This could be used to provide a form input with consistent choices and formatting across the entire application.

This technique also shows the fundamental principle at play in the following examples. First we create a `.js` file that contains some object. We must make sure that object is properly "exported" with the `export` command. Then, we can import that object wherever we need it. This is fundamentally the same process we use to accomplish the other techniques for organizing information in our Vue.js applications.

## Common Configuration Techniques
Previously in this book we explored using the Axios module to perform HTTP requests to API endpoints. This is a powerful tool, and on a modern web project we might use several different API services that are all controlled by our backend systems. It is very common for developers to consume their own API services to build multiple frontends (e.g. mobile app and website). 

When using multiple endpoints on the same API service provider, it is often necessary to provide basic authentication information, to complete some sort of authentication handshake, or to otherwise use a common configuration. If we are making API calls from multiple components, we might find that we've duplicated this common data and logic several times throughout our application. We can refactor those API calls to use the same base instance.

This approach can work in many situations with JavaScript modules that rely on some form of common configuration. Let's take a look at an Axios example to get a better idea of what this looks like. The following code is stored in the file `/src/common/api.js`.

```js
import axios from 'axios';

export const API = axios.create({
  baseURL: `http://api.openweathermap.org/data/2.5/`
})
API.interceptors.request.use(function (config) {
    // Set APPID on each request
    config.params.APPID = 'YOUR API KEY HERE';
    return config;
  }, function (error) {
    // Do something with request error
    return Promise.reject(error);
  });
```
In this example, we are using the Open Weather Map API, which requires an API Key (called `APPID` in the querystring parameters). Obviously, we would prefer not to repeat this configuration in every single `.vue` file where we make a call to a different API endpoint. There are several endpoints (`find`, `weather`, `forecast`, etc.) and if we were building a full app we would use each of those endpoints.

Now that we have our basic API configuration abstracted into a standalone file, we can use it in another component. Let's imagine we have a component called `CitySearch.vue` that allows users to look up the weather summary for a city:

```html
<script>
import {API} from '@/common/api.js';

export default {
  name: 'CitySearch',
  data () {
    return {
      results: null,
      errors: [],
      query: ''
    }
  },
  methods: {
    getCities: function () {
      API.get('find', {
        params: {
            q: this.query,
            units: 'imperial'
        }
      })
      .then(response => {
        this.results = response.data
      })
      .catch(error => {
        this.errors.push(error)
      });
    }
  }
}
</script>
```
Notice that in this example we don't need to specify anything beyond the endpoint path (`weather`). Our API call is much smaller than in previous examples. And if we used a different endpoint to get the forecast for a post, the API call would look something like this:

```html
<script>
import {API} from '@/common/api.js';

export default {
  name: 'Forecast',
  data () {
    return {
      weatherData: null,
      errors: [],
      query: ''
    }
  },
  created () {
    API.get('forecast', {
      params: {
          id: this.$route.params.cityId,
          units: 'imperial'
      }
    })
    .then(response => {
      this.weatherData = response.data
    })
    .catch(error => {
      this.errors.push(error)
    });
  }
}
</script>
```
In this example, we have a component that expects to receive a `cityId` parameter as part of the URL. This component is going to make a request to get the forecast for a given city and display the results. The API request is once again formed by importing the `API` object, and the URL for the endpoint is `forecast`. Some query string parameters are added to the request (setting the `id` value), but otherwise the request looks the same as the previous request. And once again we have not duplicated the basic configuration information.

Not only is this a cleaner way of using the the same API service in multiple components, but it also opens the door for us to provide a mechanism to switch between a "production" and "development" API server. Now that our configuration is abstracted into a single location, we could enhance that configuration to properly alter which API server the application should contact. This is a very common use case for developers, who must often work with new functionality or data that is unavailable on the production API service.

## Common Filters and Methods

When working with components, we often find ourselves performing the same tasks over and over. For example, formatting dates, text, or monetary values is a common need in our templates. This formatting is best accomplished with a "filter", which can be applied to the output of a value in the template. Since most of the logic within a component is packaged as a JavaScript object, it is easy to define objects that can be imported and used within multiple components.

Let's consider the example of a filter that capitalizes a String value. This is often needed when displaying user data in a template because we cannot be sure the user themselves capitalized the text. We can follow the same patterns we used above to accomplish this goal.

First, let's make a file called `/src/common/filters.js`:

```js
export default {
  capitalize: function (value) {
    if (!value){
     return '';
    }
    value = value.toString();
    return value.charAt(0).toUpperCase() + value.slice(1);
  }
}
```
This file defines an object that has one property: `capitalize`. That property is a function, that expects an argument called `value` and returns a modified form of the `value`. (This is the standard format for a Vue.js filter.)

We can use this filter in a component by importing it in the component logic and then using it in the template.

```html
<template>
  <div class="item">
    <h2>{{ name|capitalize }}</h2>
    <p>Price: ${{ price }}</p>
    <button v-on:click="addToShoppingCart">Add to Cart</button>
  </div>
</template>

<script>
import CommonFilters from '@/common/filters.js';

export default {
  name: 'item',
  data () {
    return {

    }
  },
  props: [
    'name',
    'price'
  ],
  methods: {
    addToShoppingCart: function () {
      console.log(`Adding ${ this.name } to cart.`);
      this.$emit('addedItem');
    }
  },
  filters: CommonFilters
}
</script>
```

In this component, we have used the `capitalize` filter to make sure the name of each item is capitalized. We could define additional filter functions in the `/src/common/filters.js` file, and each of those would also become available to every component that makes use of this technique. It is much easier to maintain consistent formatting and functionality by consolidating filters in this way.

This same technique can be used to consolidate other aspects of a component definition, too: If the same methods are used on multiple components, they can also be abstracted into a common file. Similar techniques can work for managing sets of `props` or other properties, too.

Each of the techniques described in this section revolve around creating common sources that can be accessed from anywhere in our application to provide consistent functionality. By organizing our application with these sorts of consolidations, we can provide a more understandable and less error-prone development environment for the team.







