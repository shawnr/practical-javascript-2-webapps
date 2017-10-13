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

That is the location in the App template where the router's view will be injected into the application. It replaces the use of the component tag in the template like we saw used in the previous Vue.js projects in this book.


## Defining Routes


START HERE








