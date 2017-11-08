# Project: Caching Data
This project uses the [Caching Data repository](https://github.com/suwebdev/wats4000-caching-data) as a starting point. Please fork and clone this repository to your preferred work environment.

For this project, we will add some user information storage and caching to the weather application we refactored a couple sections ago. We willwork with a weather application that could have come out of that prior refactoring experience.

The weather application has three major views: `CitySearch`, `CurrentWeather`,
and `Forecast`. These three views use several child components to display all of
their information. When we first open the repository, we can notice that there is
no way to save any data, and the site is making many requests to the weather API.

In order to improve the performance and user experience in our weather app, we
will add the ability for users to save favorite cities for easy viewing when
they return to the application. We will also cache our API queries so we do not
risk running into a rate limit, and so our users do not have to wait for
information to load as often.

These changes will dramatically enhance the utility and speed of our application.
To accomplish these changes, we will cache data into `localStorage` using the
`vue-ls` module. This module helps us manage our stored information more
efficiently and makes it a snap to provide expiration times on information.

In order to complete this project, we will edit several files in the repository.
Look for the `TODO` notes in the project files for guidance and indications of how we can accomplish
our goals.

**NOTE:** Before we start work on this, it's crucial to obtain an APPID from [OpenWeatherMap.org](https://openweathermap.org).

## Review the Requirements
In order to successfully complete this project, we must fulfill the following requirements.

* Sign up to [OpenWeatherMap.org](https://openweathermap.org/) and generate an API Key.
* Paste your API Key (which will be used as the `APPID` parameter) into the appropriate locations in the `CitySearch.vue`, `CurrentWeather.vue`, and `Forecast.vue` files.

**`main.js`**
* Add the base configuration for `vue-ls`.

**`CitySearch.vue`**
* Add the `FavoriteCities` component as a child to the `CitySearch` component (using proper imports, etc.).
* Add logic to the `created` function to initialize `this.favorites` to the value of the `favoriteCities` object in `localStorage`.
* Add logic to the `saveCity` function to update the `favoriteCities` cache in `localStorage`.
* Add logic to properly cache the API request in the `getCities` method (with proper label and expiry time).

**`FavoriteCities.vue`**
* Add logic in the `removeCity` method to remove the city from the `this.favoriteCities` array.
* Add logic to the `removeCity` method to remove the city from `localStorage`.

**`CurrentWeather.vue`**
* Add logic to properly cache the API request in the `created` function (with proper label and expiry time).

**`Forecast.vue`**
* Add logic to properly cache the API request in the `created` function (with proper label and expiry time).

## Working the Project
In order to complete this project, we will edit several files in this repository. We begin with getting an API key for use on this project.

### Make an OpenWeatherMap.org API Key
To get the project running, we need to make an account on [OpenWeatherMap.org](https://openweathermap.org/) and generate an API key. Once we have created an account, the API Keys can be found under our Account page ([located here](https://home.openweathermap.org/api_keys)). Create a new API Key and then open the project repository in a preferred editor. We must find the `YOUR_APPID_HERE` placeholder in the `src/common/api.js` file and update it.

![Working home screen](/img/project11-home1.png)
<br>Working home screen

Once we've replaced that information the project should become operational. Run `npm run dev` and verify that the project works. Once we've made sure the project is working, we can configure Vue LocalStorage for use in our application.

### Configuring Vue LocalStorage
To add the `vue-ls` module to our project, we must import it in our `src/main.js` file and tell our `Vue` instance that we want to use it. We do this with these lines of code:

```js
import VueLocalStorage from 'vue-ls';

let options = {
  namespace: 'weather__'
};

Vue.use(VueLocalStorage, options);
```
First, we have our import statement. This module has already been added to our project by running `npm install --save vue-ls`, so it can be imported like this. Then, we define an `options` object, which only has one property: `namespace`. We then execute a `Vue.use()` command to let our `Vue` instance know we are using the `VueLocalStorage` module (aka `vue-ls`).

Now we can access `this.$ls` in any component we use in our application. 

### Adding the `FavoriteCities` Component
In the `src/components/CitySearch.vue` file, we must add the `FavoriteCities` component as a child component. This requires us to import the component, then to define it in the `components` object, and finally to add a tag to our template where the component should be displayed.

The logic changes to add the `FavoriteCities` component look like this:

```js
// ... previous imports ... //
import FavoriteCities from '@/components/FavoriteCities';


export default {
  name: 'CitySearch',
  components: {
    'weather-summary': WeatherSummary,
    'weather-data': WeatherData,
    'load-spinner': CubeSpinner,
    'message-container': MessageContainer,
    'favorite-cities': FavoriteCities
  },
  
  // ... more code ... //
```
We can see how the `import` statement and the `components` object have been updated. In the template, the tag is straightforward to drop in:

```html
<favorite-cities v-bind:favoriteCities="favorites"></favorite-cities>
```
We use the tag and bind the `favorites` value from the `CitySearch` component to the `FavoriteCities` component. At this point, we should see our component show up with no cities listed.

![Empty Favorites Listing](/img/project13-empty_favorites.png)
<br>Empty Favorites Listing

### Make Favorite Cities Work in `CitySearch`
In order to make our favorite cities listing work in our application, we must actually save data when the user clicks the "Save City to Favorites" button. In order to make it work, we must update two parts of our code. First, we need to allow users to save a city. There is a `saveCity` method defined for us, so we can fill in the logic there:

```js
saveCity: function (city) {
  this.favorites.push(city);
  this.$ls.set('favoriteCities', this.favorites);
}
```
To save a city, we simply `push` the `city` object into the `this.favorites` array. We then cache these favorites using `this.$ls.set()`. Because we only have one list of `favoriteCities` we can just specify the name of the cache label directly, and we do not need to set a cache expiration time because we want this data to persist forever.

Now we should be able to see our information updating on the screen and in our devtools. Open the "Application" tab in our devtools panel and select our `localhost` domain under `localStorage`. We should see all of the values updating in all the right places. 

![Storing cities in localStorage](/img/project13-localstorage.gif)
<br>Storing cities in localStorage

### Make Favorite Cities Removable
Now that we have made it possible to save cities in both component data and localstorage, we should make it possible for our users to remove cities. Since we are syncing our data through the caching system using `localStorage`, we can remove cities in the `FavoriteCities` component, where it's easier to respond to the user's click action.

A `removeCity` method is provided for us, so we will place our logic there:

```js
removeCity: function (city) {
  let cityIndex = this.favoriteCities.indexOf(city);
  this.favoriteCities.splice(cityIndex, 1);
  this.$ls.set('favoriteCities', this.favoriteCities);
}
```
In this example, we have used `indexOf` on the `favoriteCities` array to find the index of the city object. Once we have that index, we can use the `splice()` command to remove only that object from the `favoriteCities` array. Then, we can save the `favoriteCities` cache again. The next time the page loads, it will load the proper cache.

Once we have that code in place, we can add and remove values at will.  

### Cache `CitySearch` API Requests
Now that we've enhanced the application with the ability to save cities to a list of favorites, we can provide some performance enhancements by caching API requests so we do not make as many. In order to set up the caching of the API requests, we will tackle the same few tasks each time:

1. We will make a cache label (called `cacheLabel`) to represent the unique query. This label will allow us to cache individual queries.
2. We will create an expiration time (called `cacheExpiry`) to tell the system how long it should store the query cache.
3. We will wrap our API request in a conditional that will check for the existence of a cache. If it finds cached data, it will use that data. If the data has expired, or has never before been requested, then it will make the request.
4. When a request is made, the data will be cached.

For the next three sets of changes we are essentially implementing the same thing. This is what it looks like:

```js
getCities: function () {
  this.results = null;
  this.showLoading = true;

  let cacheLabel = 'citySearch_' + this.query;
  let cacheExpiry = 15 * 60 * 1000; // 15 minutes

  if (this.$ls.get(cacheLabel)){
    console.log('Cached query detected.');
    this.results = this.$ls.get(cacheLabel);
    this.showLoading = false;
  } else {
    console.log('No cache available. Making API request.');
    API.get('find', {
      params: {
          q: this.query
      }
    })
    .then(response => {
      this.$ls.set(cacheLabel, response.data, cacheExpiry);
      console.log('New query has been cached as: ' + cacheLabel);
      this.results = response.data;
      this.showLoading = false;
    })
    .catch(error => {
      this.messages.push({
        type: 'error',
        text: error.message
      });
      this.showLoading = false;
    });
  }
}
```
We can see that the `cacheLabel` and `cacheExpiry` values are assigned right away. These will be used in various conditions, so they are necessary and worthwhile to compute. (Remember that the `cacheExpiry` time needs to be in milliseconds.) Then, we see the first conditional. If a value does not exist in `localStorage` it will be returned as `undefined`. Since `undefined` is a `false` value, this conditional will be true only if valid data is stored in the cache that matches the `cacheLabel`.

If data is found, we log a message to the console and then set the results equal to the cache data. These results can be processed just like the API results, so our application will show the information to the user properly.

If no data is found (meaning the cache has either expired or the data has never been requested before), then we log a message to console to say that we need to make the API request. We execute the same API request as before, but in the `then` clause, we add a `this.$ls.set()` statement to save the response into the `localStorage` cache. The data is stored with the `cacheLabel` we specified, and the expiration time is set to the `cacheExpiry` value. Once we have cached the data, we log another statement to the console so we can track that everything has happened the way we expect. 

We should now be able to repeat queries in our console and see that a new query causes a new API request, but a repeated query uses cached data. We can also verify that API requests are (or are not) happening by watching the "Network" tab of our devtools while we execute searches.

The functionality of this page should be the same, with the only difference being the speed with which repeated searches are executed. Users will perceive our application as being much faster thanks to these caching changes.

### Cache `CurrentWeather` and `Forecast` API Requests
We will make the same changes to cache the API requests in the `src/components/CurrentWeather.vue` and `src/components/Forecast.vue` files. In each case we must create `cacheLabel` and `cacheExpiry` values, and then we will use the same kind of conditional to check for the value in `localStorage` and perform the API request if it is not found.

Rather than repeating these same structures multiple times on the page, refer to the full file details below for more precise examples of what this process looks like in each file.

## Wrapping Up
Once we have made all of our changes, we have an app that is more functional and faster for users. Most people would agree that makes any app better. The following files have been changed:

**`main.js`**
```js
import Vue from 'vue'
import App from './App'
import router from './router'
import VueLocalStorage from 'vue-ls';

let options = {
  namespace: 'weather__'
};

Vue.use(VueLocalStorage, options);

Vue.config.productionTip = false

new Vue({
  el: '#app',
  router,
  template: '<App/>',
  components: { App }
})

```


**`CitySearch.vue`**
```html
<template>
  <div>
    <favorite-cities v-bind:favoriteCities="favorites"></favorite-cities>
    <h2>City Search</h2>
    <message-container v-bind:messages="messages"></message-container>
    <form v-on:submit.prevent="getCities">
        <p>Enter city name: <input type="text" v-model="query" placeholder="Paris, TX"> <button type="submit">Go</button></p>
    </form>
    <load-spinner v-if="showLoading"></load-spinner>
    <ul class="cities" v-if="results && results.list.length > 0">
      <li v-for="city in results.list">
        <h2>{{ city.name }}, {{ city.sys.country }}</h2>
        <p><router-link v-bind:to="{ name: 'CurrentWeather', params: { cityId: city.id } }">View Current Weather</router-link></p>

        <weather-summary v-bind:weatherData="city.weather"></weather-summary>

        <weather-data v-bind:weatherData="city.main"></weather-data>
        <p><button class="save" v-on:click="saveCity(city)">Save City to Favorites</button></p>
      </li>
    </ul>
  </div>
</template>

<script>
import {API} from '@/common/api';
import WeatherSummary from '@/components/WeatherSummary';
import WeatherData from '@/components/WeatherData';
import CubeSpinner from '@/components/CubeSpinner';
import MessageContainer from '@/components/MessageContainer';
import FavoriteCities from '@/components/FavoriteCities';


export default {
  name: 'CitySearch',
  components: {
    'weather-summary': WeatherSummary,
    'weather-data': WeatherData,
    'load-spinner': CubeSpinner,
    'message-container': MessageContainer,
    // TODO: Add FavoriteCities child component here
    'favorite-cities': FavoriteCities
  },
  data () {
    return {
      results: null,
      query: '',
      showLoading: false,
      messages: [],
      favorites: []
    }
  },
  created () {
    if (this.$ls.get('favoriteCities')){
      this.favorites = this.$ls.get('favoriteCities');
    }
  },
  methods: {
    saveCity: function (city) {
      this.favorites.push(city);
      this.$ls.set('favoriteCities', this.favorites);
    },
    getCities: function () {
      this.results = null;
      this.showLoading = true;

      let cacheLabel = 'citySearch_' + this.query;
      let cacheExpiry = 15 * 60 * 1000;
      
      if (this.$ls.get(cacheLabel)){
        console.log('Cached query detected.');
        this.results = this.$ls.get(cacheLabel);
        this.showLoading = false;
      } else {
        console.log('No cache available. Making API request.');
        API.get('find', {
          params: {
              q: this.query
          }
        })
        .then(response => {
          this.$ls.set(cacheLabel, response.data, cacheExpiry);
          console.log('New query has been cached as: ' + cacheLabel);
          this.results = response.data;
          this.showLoading = false;
        })
        .catch(error => {
          this.messages.push({
            type: 'error',
            text: error.message
          });
          this.showLoading = false;
        });
      }
    }
  }
}
</script>

<style scoped>
.errors li {
  color: red;
  border: solid red 1px;
  padding: 5px;
}
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  width: 300px;
  min-height: 300px;
  border: solid 1px #e8e8e8;
  padding: 10px;
  margin: 5px;
}
a {
  color: #42b983;
}
</style>
```


**`CurrentWeather.vue`**
```html
<template>
  <div>
    <h2>Current Weather <span v-if="weatherData"> for {{ weatherData.name }}, {{weatherData.sys.country }}</span></h2>
    <message-container v-bind:messages="messages"></message-container>
    <p>
      <router-link to="/">Home</router-link> |
      <router-link v-bind:to="{ name: 'Forecast', params: { cityId: $route.params.cityId } }">View 5-Day Forecast</router-link>
    </p>
    <load-spinner v-if="showLoading"></load-spinner>
    <div v-if="weatherData">

      <weather-summary v-bind:weatherData="weatherData.weather"></weather-summary>

      <weather-data v-bind:weatherData="weatherData.main"></weather-data>

    </div>

  </div>
</template>

<script>
import {API} from '@/common/api';
import WeatherSummary from '@/components/WeatherSummary';
import WeatherData from '@/components/WeatherData';
import CubeSpinner from '@/components/CubeSpinner';
import MessageContainer from '@/components/MessageContainer';

export default {
  name: 'CurrentWeather',
  components: {
    'weather-summary': WeatherSummary,
    'weather-data': WeatherData,
    'load-spinner': CubeSpinner,
    'message-container': MessageContainer
  },
  data () {
    return {
      weatherData: null,
      messages: [],
      query: '',
      showLoading: false
    }
  },
  created () {
    this.showLoading = true;

    let cacheLabel = 'currentWeather_' + this.$route.params.cityId;

    let cacheExpiry = 15 * 60 * 1000;

    if (this.$ls.get(cacheLabel)) {
      console.log('Cached value detected.');
      this.weatherData = this.$ls.get(cacheLabel);
      this.showLoading = false;
    } else {
      console.log('No cache detected. Making API request.');
      API.get('weather', {
        params: {
            id: this.$route.params.cityId
        }
      })
      .then(response => {
        this.$ls.set(cacheLabel, response.data, cacheExpiry);
        this.showLoading = false;
        this.weatherData = response.data;
      })
      .catch(error => {
        this.showLoading = false;
        this.messages.push({
          type: 'error',
          text: error.message
        });
      });
    }
  }
}
</script>

<style scoped>
.errors li {
  color: red;
  border: solid red 1px;
  padding: 5px;
}
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  width: 300px;
  min-height: 300px;
  border: solid 1px #e8e8e8;
  padding: 10px;
}
a {
  color: #42b983;
}
</style>
```


**`Forecast.vue`**
```html
<template>
  <div>
    <h2>Five Day Hourly Forecast <span v-if="weatherData"> for {{ weatherData.city.name }}, {{weatherData.city.country }}</span></h2>
    <message-container v-bind:messages="messages"></message-container>
    <p>
      <router-link to="/">Home</router-link> |
      <router-link v-bind:to="{ name: 'CurrentWeather', params: { cityId: $route.params.cityId } }">Current Weather <span v-if="weatherData"> for {{ weatherData.city.name }}, {{weatherData.city.country }}</span></router-link>
    </p>

    <ul v-if="weatherData" class="forecast">
      <transition-group name="fade" tag="div" appear>
        <li v-for="forecast in weatherData.list" v-bind:key="forecast.dt">
          <h3>{{ forecast.dt|formatDate }}</h3>
          <weather-summary v-bind:weatherData="forecast.weather"></weather-summary>
          <weather-data v-bind:weatherData="forecast.main"></weather-data>
        </li>
      </transition-group>
    </ul>
    <load-spinner v-if="showLoading"></load-spinner>
  </div>
</template>

<script>
import {API} from '@/common/api';
import WeatherSummary from '@/components/WeatherSummary';
import WeatherData from '@/components/WeatherData';
import CubeSpinner from '@/components/CubeSpinner';
import MessageContainer from '@/components/MessageContainer';

export default {
  name: 'Forecast',
  components: {
    'weather-summary': WeatherSummary,
    'weather-data': WeatherData,
    'message-container': MessageContainer,
    'load-spinner': CubeSpinner
  },
  data () {
    return {
      weatherData: null,
      messages: [],
      query: '',
      showLoading: false,
      messages: []
    }
  },
  created () {
    this.showLoading = true;

    let cacheLabel = 'forecast_' + this.$route.params.cityId;

    let cacheExpiry = 15 * 60 * 1000;

    if (this.$ls.get(cacheLabel)) {
      console.log('Cached value detected.');
      this.weatherData = this.$ls.get(cacheLabel);
      this.showLoading = false;
    } else {
      console.log('No cache detected. Making API request.');
      API.get('forecast', {
        params: {
            id: this.$route.params.cityId
        }
      })
      .then(response => {
        this.$ls.set(cacheLabel, response.data, cacheExpiry);
        this.showLoading = false;
        this.weatherData = response.data;
      })
      .catch(error => {
        this.showLoading = false;
        this.messages.push({
          type: 'error',
          text: error.message
        });
      });
    }
  },
  filters: {
    formatDate: function (timestamp){
      let date = new Date(timestamp * 1000);
      const months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'];
      const weekdays = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
      //let weekday = date.getDay();
      let daynum = date.getDate();
      let month = date.getMonth();

      let hour = date.getHours();
      if (hour === 12) {
        hour = 'Noon';
      } else if (hour === 0) {
        hour = 'Midnight';
      } else if (hour > 12) {
        hour = hour - 12 + 'PM';
      } else if (hour < 12) {
        hour = hour + 'AM';
      }
      //let year = date.getFullYear();
      return `${ months[month] } ${ daynum } @ ${ hour }`;
    }
  }
}
</script>

<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity 1s
}
.fade-enter, .fade-leave-to {
  opacity: 0
}
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  width: 200px;
  min-height: 300px;
  border: solid 1px #e8e8e8;
  padding: 10px;
  margin: 5px;
}

a {
  color: #42b983;
}
</style>
```


**`FavoriteCities.vue`**
```html
<template>
    <ul class="favorite-cities">
        <li><h2>Favorite Cities</h2></li>
        <li v-if="favoriteCities.length < 1">No favorites cities to display.</li>
        <li v-for="city in favoriteCities">
          <router-link v-bind:to="{ name: 'CurrentWeather', params: { cityId: city.id } }">{{ city.name }}</router-link> <button v-on:click="removeCity(city)" class="remove">x</button>
        </li>
    </ul>
</template>

<script>
export default {
  name: 'FavoriteCities',
  data () {
    return {}
  },
  props: {
    favoriteCities: Array
  },
  methods: {
    removeCity: function (city) {
      this.favoriteCities.splice(this.favoriteCities.indexOf(city), 1);
      this.$ls.set('favoriteCities', this.favoriteCities);
    }
  }
}
</script>

<style scoped>
.favorite-cities {
  list-style-type: none;
  padding: 10px;
  background: #ccc;
  width: 25%;
  float: right;
}
.remove {
  font-size: 0.8rem;
  color: white;
  background: #AA0000;
  padding: 2px;
  cursor: pointer;
}
</style>
```

**Note:** We also need to add our `APPID` to the `src/common/api.js` file. Don't forget!

## Build and Deploy
Once we've finished our work, we can build and deploy the project. This project has been configured to build to the `docs/` directory, so we can follow the same pattern we used before:

1. Execute the `npm run build` command to build the files into the `docs/` directory.
2. Commit all of our code.
3. Push the code up to GitHub.
4. Go into the repository settings and set the GH Pages section to publish from the `docs/` directory.

The project should now be up and available to the public through GH Pages.

## Stretch Goals
If we crave more challenge, we can attempt these additional goals.

* Add more preferences to the system, such as the ability to load a single "favorite" city when the page is first loaded (with no clicks or search required).
* Add the ability for users to specify their own label for the favorite cities (e.g. "home", "Aunt Barb's House", etc.).
* Add a query to another API service, such as flickr, to augment this information. Build the proper caching to make efficient use of that query, too.
* Add animated transitions to the information in this project.





