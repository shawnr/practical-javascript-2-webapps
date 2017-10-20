# Building Navigation

Building navigation in a Vue.js application is made easy by the tools `vue-router` gives us. We can use the custom [`<router-link>` tag](https://router.vuejs.org/en/api/router-link.html) to insert links in templates by name or by path. We can programmatically move users to different parts of the application within the component logic. And `vue-router` even handles properly denoting when a particular link is "active" based on the current path. Let's dive in and learn how to use all these features to our advantage.

## Router Links

We create links to other routes by using the `<router-link>` tag in our templates. This tag is automatically converted into an `<a>` tag when it is processed by Vue.js, but it has the advantage of coming with extra functionality to make all of our route links work flawlessly. Here is an example of how we could create a navigation in our templates using `<router-link>`:

```html
<ul class="nav">
    <li>
        <router-link v-bind:to="{name: 'Home'}">Home</router-link>
    </li>
    <li>
        <router-link v-bind:to="{name: 'NewComponent'}">New Component</router-link>
    </li>
</ul>
```
When we use the `<router-link>` element to create links, we also use a `to` attribute instead of a typical `href` attribute. The `to` attribute accepts _either_ the `name` or the `path` property of the route. In the example above we have used the `name` property. But we could achieve the exact same result (with slightly less typing) using the `path` property:

```html
<ul class="nav">
    <li>
        <router-link to="/">Home</router-link>
    </li>
    <li>
        <router-link to="/newcomponent">New Component</router-link>
    </li>
</ul>
```

<div class="tip-box">
    <h3>Use Named Routes</h3>
    <p>To many new web developers, the idea of using named routes seems a little strange. After all, why add another thing to remember when we could just refer to the route by the path, which is required by Vue Router? This is a reasonable question, but the value of using named routes outweighs the difficulty of defining and remembering the name.</p>
    <p>Named URLs pay off in a few ways: First, they allow us to alter the paths in our application without editing our templates. We can alter the path in the route definition, and we do not need to touch any other files if we have only used named routes in our links. Second, paths can become long and difficult to remember. It can be especially difficult to remember the order of route parameters, and on a large project this only becomes more difficult. Third, named routes can be named in a sensible way so it's easy to remember which route handle what, and that can allow us to use abbreviated paths when suitable (such as when building a complex document retrieval system).</p>
</div>

## Passing Data as Route Parameters
When creating links, we often need to supply some information for the route parameters. Imagine that we are building the user pages we defined in the previous section:

```js
routes: [
    { 
      path: '/user/:username', 
      name: 'UserProfile',
      component: User 
    }
]
```
In order to link to the `UserProfile` page, we need to provide a `username` parameter. We would write this link in the template like this:

```html
<router-link v-bind:to="{ name: 'UserProfile', params: {username: 'jdoe'} }">Profile</router-link>
```

We must use the `v-bind` directive to supply a JavaScript object to the `to` attribute. The JS object we create has a property called `name`. We could alternatively use the `path` property if we wished to define this link with a `path` instead of a `name`. We also supply a `params` property that contains an object with all the parameters this route requires. In this case, that is just a `username` value, which we have set to `'jdoe'`. The result of this tag in our template would be a link that points to `/user/jdoe`. 

It's more likely that rather than providing the username as a static string, we would want to use some value known to the component to create this link. If we imagine that we have a `user` object defined in our component data, the `<router-link>` tag would look more like this:

```html
<router-link v-bind:to="{ name: 'UserProfile', params: {username: user.username} }">Profile</router-link>
```
All that we've changed here is to refer to `user.username` instead of `'jdoe'`. This is a common way to use dynamic route parameters with the `<router-link>` tag.

## Using `router-link-active`
One common design pattern for frontend code is to label the link to the current page with an `active` class. This allows us to write styles for our navigation system that indicate which page the user is currently viewing. Many sites use convoluted systems to coordinate the current path in the location of the browser to the navigation links on the pages. Luckily, `vue-router` takes care of this for us when we use the `<router-link>` tag to define our internal site links.

When we view a page in our Vue.js app, we can look at the links we've defined with `<router-link>` and see that the currently active link has a `router-link-active` class appended to it. If we style that class in our `App` component code, then we can see our currently active links indicated as we navigate around our Vue.js website. This is a handy feature and saves us yet another small development headache.

## Programmatic Navigation
Although we mostly will move users around with links that the user clicks, sometimes it is necessary to move users from one location to another programmatically. For example, when a user fills out a complex form, we might verify we have all the correct data before moving them off to the confirmation page. Or we might build a "wizard" style interface that walks users through the different steps of a process. In that case, it might be useful to push users to the next step automatically. To accomplish this, we use [the `router.push()` method](https://router.vuejs.org/en/essentials/navigation.html) supplied by `vue-router`.

Just like with the `<router-link>` tag, we can use `router.push()` with either a simple route `name` or `path`, or we can use it with a more complex object that defines a route `name` or `path` and a `params` data object. Here is the simple way to use `router.push()`:

```html
<script>
  export default {
    data () {
      return {
        validated: false
      }
    },
    methods: {
      validate: function () {
        if (this.validated) {
            router.push('confirm');
        }
      }
    }
  }
</script>
```
In this example, we can imagine that we have some form being presented to the user. When it is filled in with data the `validate` method would be executed. If `validated` is `true`, then the user would be moved to the `confirm` route.

```html
<script>
  export default {
    data () {
      return {
        validated: false,
        orderID: 123
      }
    },
    methods: {
      validate: function () {
        if (this.validated) {
            router.push({ name: 'confirm', params: {orderID: this.orderID} });
        }
      }
    }
  }
</script>
```

In this second example, the same scenario applies, but this time we want to supply the `orderID` value to the `confirm` route. To do so, we construct an object very much like we did with the `<router-link>` tag, and we define our route parameters in a `params` object. Now, when the form is validated all of this data will be properly assembled into a route reference.

All of these features combine to allow us to build a huge variety of navigational elements in our sites and applications. We can use whichever approach works to fulfill our requirements, and we can integrate this navigation at every level of our application.














