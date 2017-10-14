# Setting Up `vue-router`

[Vue Router](https://router.vuejs.org/en/) (`vue-router`) is the tool that we will use to route our users within our applications. This is a core piece of the Vue.js framework, and there is [a great documentation site ](https://router.vuejs.org/en/)available to learn about it. We will cover the fundamental details in this section, but feel free to review the additional documentation.

Getting `vue-router` into our applications is easy when using the Vue CLI because it can be included as part of the project skeleton. If we wanted to add `vue-router` to an existing project, we could follow [the guide provided in the Vue Router documentation](https://router.vuejs.org/en/installation.html).

## Bootstrapping a Project with `vue-router`
When we bootstrap a project, we can choose to use `vue-router`. This results in a setup that includes a routes definition and the integration of the routes in several places in the project.

First, in the `src/main.js` we can see that the router is included in the imports and setup of the app itself:

```js
import Vue from 'vue'
import App from './App'
import router from './router'

Vue.config.productionTip = false

new Vue({
  el: '#app',
  router,
  template: '<App/>',
  components: { App }
})
```
If we look at the file in `src/router/index.js` we can see the route definitions:

```js
import Vue from 'vue'
import Router from 'vue-router'
import FormsPractice from '@/components/FormsPractice'

Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/',
      name: 'Forms',
      component: FormsPractice
    }
  ]
})
```

In the `App` component, found in `src/App.vue`, we can see that the template now includes a `<router-view>` element:

```html
<template>
  <div id="app">
    <h1>Practicing with Forms</h1>
    <router-view/>
  </div>
</template>
```

The `<router-view>` element is the location in the App template where the router's view will be injected into the application. It replaces the use of the component tag in the template like we saw used in the previous Vue.js projects in this book. This will inject whatever component we have defined in the routes into the HTML at that location. Of course, the next question is: How do we define routes?


## Defining Routes
We define routes in the `routes/index.js` file as part of the `routes` Array. This definition looks something like this:

```js
import Vue from 'vue'
import Router from 'vue-router'
import Home from '@/components/Home'
import Login from '@/components/Login'
import Register from '@/components/Register'

Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/',
      name: 'Home',
      component: Home
    },
    {
      path: '/login',
      name: 'Login',
      component: Login
    },
    {
      path: '/register',
      name: 'Register',
      component: Register
    }

  ]
})
```
In the example configuration above, we see three different route objects defined: `Home`, `Login`, and `Register`. These three route objects have the same set of properties: `path`, `name`, and `component`. These properties are commonly used, and often the routing for our apps need not get any more complex. Let's take a look at what these properties mean.

The `path` property is the desired URL for the route. These URLs should begin with a forward slash (`/`), and they  can include any URL safe characters. This the URL the user will see in their browser's location bar, and it should make sense based on the content of the view.

The `name` property is a unique name for this route in the Vue.js application. The name can be used to reference the route in templates, so instead of linking to `/some-view-location` we can link to `ViewName`. The advantage here is that we can alter the URLs used in the app by modifying the `routes/index.js` file without modifying every template where we link to those routes. This is a very helpful feature of `vue-router` and is a common feature among URL routing systems in various frameworks. (We will look more at building navigational linkage in our templates later.)

Finally, the `component` property indicates which component should be injected into the `<router-view>` element in the application template. This component might utilize several other components as part of its template, and there are even ways to get more complex with loading multiple components in each route, but for most cases this feature works perfectly as it is.

In addition to these fundamentals of route definition, there are a few other more advanced features we often need to use in our route definition.

### Dynamic URLs
Sometimes it is necessary to create a URL using data known in the system. A common use case for this is showing a user profile at a URL that looks like this:

```html
http://example.com/user/username
```

When linking to user profiles in a system, it's necessary to read that `username` value out of the URL and process the user profile view accordingly. We can define a route that will give us access to the `username` value like this:

```js
const router = new VueRouter({
  routes: [
    { 
      path: '/user/:username', 
      name: 'UserProfile',
      component: User 
    }
  ]
})
```
In this case, the `:username` portion of the URL defines a "route parameter", which is what we call these variables that are inserted into the URL of a route definition. We use route parameters to modulate the content of the view we show to our users. Route parameters can be referenced in our component logic like this:

```html
<template>
  <div class="component">
    <h2>{{ welcome }}</h2>
    <p>{{ $route.params.username }}</p>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        salutation: 'Ahoy'
      }
    },
    computed: {
      welcome: function () {
        return this.salutation + ', ' + this.$route.params.username
      }
    }
  }
</script>
```

In this example we can see that we are using the `$route.params` object in both the component template and logic. In the template, we can directly reference `$route.params` to use in creating the interface. In the component logic, we can refer to the route parameters in the same way we refer to other properties defined as part of the component's `data` object: `this.$route.params`. Any value we assign in the URL of the route definition will be revealed as a property in `this.$route.params`.

In the example above, we can see that there is a computed value called `welcome` that is being generated. This `welcome` value uses `this.salutation` and `this.$route.params.username` to create a welcome message that is interpolated into our template. If the URL is changed, the page will properly reflect the change in the `this.$route.params.username` value. 

**Note:** If we are using more complex components (as we do later in this book) that define a `created` function or do other initialization work in the component, we may need to re-initialize the component when the `$route.params` object is changed. More information about making that happen can be found on [the Dynamic Matching documentation](https://router.vuejs.org/en/essentials/dynamic-matching.html) as part of the Vue Router docs.

We could also add multiple values to a route definition. Here is a helpful table showing how route parameters get used in various URLs:

| Route Definition | Actual URL | Route Parameters |
|------------------|------------|------------------|
| `/:username` | `/shawnr` | `{ 'username': 'shawnr' }` |
| `/:username` | `/jdoe` | `{ 'username': 'jdoe' }` |
| `/:username/posts/:postid` | `/shawnr/posts/12345` | `{ 'username': 'shawnr', 'postid': 12345 }` |
| `/:username/posts/:postid` | `/jdoe/posts/9876` | `{ 'username': 'jdoe', 'postid': 9876 }` |

Route parameters are powerful tools for coordinating information between different views in our applications, and we will explore many use cases for them throughout this book.

### Nested URLs

Sometimes we wish to define URLs as part of a "section" of our site. For example, in many sites we would have some kind of user profile page located at `/username`. However, we might also have the following URLs:

* `/user/username/profile` &mdash; User profile page
* `/user/username/profile/edit` &mdash; Edit user profile page
* `/user/username/settings` &mdash; Site settings page for a specific user
* `/user/username/posts` &mdash; Listing of all posts the user has made
* `/user/username/post/12345` &mdash; View for a single post made by the user

We see these kinds of related URLs all the time online, and they make sense: We like to group pages with similar functionality under similar URLs. It helps us as developers, and our users, understand our websites and applications better.

The route definition that would create some of these URLs would look like this:

```js
{
  path: '/user/:username',
  component: User,
  children: [
    {
      // UserProfile will be rendered inside User's <router-view>
      // when /user/:username/profile is matched
      path: 'profile',
      name: 'UserProfile',
      component: UserProfile
    },
    {
      // UserPosts will be rendered inside User's <router-view>
      // when /user/:username/posts is matched
      path: 'posts',
      name: 'UserPosts',
      component: UserPosts
    }
  ]
}
```

In this case, we have a general `/user/:username` URL that loads the `User` component. The `User` component will inject an appropriate _nested_ route according to the `path` values we have defined. We define nested routes using the `children` property on a route definition. This property accepts an array of additional route definitions. 

The `<router-view>` element in the `User` component template looks like this:

```html
<template>
  <div class="user">
    <h2>{{ welcome }}</h2>
    <router-view></router-view>
  </div>
</template>
```
The `UserProfile` and `UserPosts` components will be rendered inside the `<router-view>` tag within the `User` template. Each of these components can access the `$route.params.username` value in their templates or component logic. Note that the URLs of nested routes defined in the `children` property do not use absolute paths&mdash;they do _not_ begin with a forward slash ('/'). Rather, they are understood to continue from the `path` definition on the parent route.

## Moving On
Now that we've got the basics of how routes work, let's move on and discuss creating new components as well as linking our URLs together using `<router-link>` tags. There are more features in `vue-router` that we have not covered here. Some of those will be touched on later in this book, but it's always worthwhile to visit [the official Vue Router documentation](https://router.vuejs.org/en/) to learn more.









