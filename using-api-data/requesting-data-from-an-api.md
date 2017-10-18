# Requesting Data from an API
In order to make requests to an API and then receive and process the data from the API responses, we will use a JavaScript module designed for this purpose. The current most popular choice when working with Vue.js is a module called [Axios](https://github.com/axios/axios), which is a Node.js module that can be used by virtually any JavaScript application. It is possible to use an alternative, including the formerly-preferred module, [Vue Resource](https://github.com/pagekit/vue-resource). Most of the content of the examples that follow will apply to any API request module, although the specifics of the implementation will vary.

## Install Axios
In order to use Axios in our application, we must first install it. Since we are already using a well-tooled environment, we can run the `npm install` command like this:

```bash
npm install axios --save
```

This command installs Axios for use in our application, and it also saves Axios as a dependency in the `package.json` file that tracks all of the modules we use in our project. Once we've run this command, we can look in our `package.json` file and see that it is listed. (Look in the `dependencies` object.)

```js
"dependencies": {
    "axios": "^0.16.2",
    "vue": "^2.5.2",
    "vue-router": "^3.0.1"
},
```

## Use Axios in a Component
Now that we've made Axios available to our application, we can use it inside a component. The first step to make an API request within a component is to properly import Axios. This import statement should go at the top of the `<script>` section in our component:

```
import axios from axios
```

Now that we have imported `axios`, we can reference that within our component logic. We will use `axios` to make a request to an API server and then receive the response, which we will then make available as a part of the `data` object. Before we can actually perform the data request, we should initialize the `data` object properties that will be used in the template:

```js
data () {
  return {
    posts: [],
    errors: []
  }
}
```
We have initialized two values: `posts` and `errors`. Both of these are set to empty arrays. We will populate these values according to the results of our API requests. We can reference these two values in our templates in order to display the information returned by our API request.

### Creating the Request
In order to actually perform an API request, we must write some code to do so. It's very common to have a component that requires data from an API when it is first loaded. In these cases, we want to load the data as soon as the component is loaded, so we can use the `created` property of the Vue component. We will see an example shortly of using the `created` property to load data when a component is loaded, but it's worthwhile to remember that this same technique can be applied to writing component methods. In those cases, the data could be fetched whenever the user performs a specific action. This is a common way to implement API requests to refresh data or submit data customized for the user's needs.

For our first example, let's look at an API request made when the component is first loaded:

```html
<script>
import axios from 'axios';

export default {
  name: 'HelloWorld',
  data () {
    return {
      posts: [],
      errors: []
    }
  },
  created () {
    axios.get(`http://jsonplaceholder.typicode.com/posts`)
    .then(response => {
      this.posts = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
}
</script>
```
Notice that `created ()` is defined in a very similar way to the `data ()` function.

## Promises















