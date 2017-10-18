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
Notice that `created ()` is defined in a very similar way to the `data ()` function. Within the `created ()` function, we only make one JavaScript statement: a somewhat complex command using `axios`. Although this doesn't look much like the code we've been used to writing/reading, it's actually the most simple way to write an API request. Once we take a closer look, we should see that this is not as complex as it first appears.

The first line of the command is: 
```
axios.get(`http://jsonplaceholder.typicode.com/posts`)
```
This invokes `axios` and supplies the URL for the API request. This command results in the creation of a "promise", which is a JavaScript object that works as a placeholder for some information or function that will take a moment to be resolved. (We can [read more about promises here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise).) Because the request to the API cannot be resolved instantly (it takes some time to receive the data from the server, just like when we are downloading other information from a web server), we need this promise object to handle the receipt and transformation of the API data into something we can use in the application.

The next clause of the `axios` command defines what happens after the promise is resolved:

```js
.then(response => {
  this.posts = response.data
})
```
This is a `then` clause, and it will be executed when the promise is completed, regardless of what the result of the API call was. The way we use Axios in our applications, we want to use the [JavaScript "arrow function"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) to define the function that will be executed when the `then` clause is invoked (which will be when the API response is received). 

Using the arrow function syntax, the argument for this function is named `response`. This argument will be passed to the code block defined between the curly braces. (The arrow is a reminder that the `response` value will be "injected" into the code that follows.) The `response` value is an object that represents the API request we made with `axios`. The actual information received from the server is stored in `response.data`. So the `then` clause executes an arrow function that sets `this.posts` equal to `response.data`. Our template has access to `this.posts`, so it can successfully parse that data and we can output the information using a loop.

The final clause in this request is the `catch` clause:

```js
.catch(e => {
  this.errors.push(e)
})
```

The `catch` clause executed when there is an error in the request. It also uses the arrow function syntax to define the function that will be executed when an error is detected. The error is captured as the value `e`, and passed into the arrow function. We only have one line of code here, which will add this error to the array of `errors` we defined in the component's `data` object. Again, our templates will have access to these values, allowing us to present this information to our users.

```html
<ul v-if="posts.length > 0">
  <li v-for="post of posts">
    <p><strong>{{post.title}}</strong></p>
    <p>{{post.body}}</p>
  </li>
</ul>

<ul v-if="errors.length > 0">
  <li v-for="error of errors">
    {{error.message}}
  </li>
</ul>
```
We can see from this example code how the `posts` and `errors` values can be used in our templates to output useful information for our users. In this case, all of this code would combine to show the list of sample results provided by the JSON Placeholder API.

### Requests with Parameters
Axios actually lets us do quite a few different things to make our API requests more complex and functional. One case that comes up often is using user-submitted information to modify a request. We often want to have a `refreshResults` or a `search` method on our components that can be invoked to provide the user with better information.

Let's take a look at an example request made to the Datamuse API, which can return all sorts of word data. In this case, we will use a query that returns synonyms for words or phrases:

```html
<template>
  <div class="hello">
    <h1>Example Data Request</h1>
    <p>Find synonyms for <input v-model="phrase"> <button v-on:click="findSynonyms">Search</button></p>
    <ul v-if="synonyms.length > 0">
      <li v-for="synonym of synonyms">
        <p><strong>{{synonym.word}}</strong></p>
        <p>{{synonym.score}}</p>
      </li>
    </ul>

    <ul v-if="errors.length > 0">
      <li v-for="error of errors">
        {{error.message}}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'HelloWorld',
  data () {
    return {
      synonyms: [],
      errors: [],
      phrase: 'logic'
    }
  },
  methods: {
    findSynonyms: function(){
      axios.get('https://api.datamuse.com/words', {
        params: {
          ml: this.phrase
        }
      })
      .then(response => {
        this.synonyms = response.data;
      })
      .catch(error => {
        this.errors.push(error);
      });
    }
  }
}
</script>
```
In this example, we can see the template and the logic for a component that allows the user to type in a word or phrase and then receive synonyms back. If we look at the template, we see that it generally matches what we saw in the previous example. The new template includes a text input field and a button to allow the user to type in their word or phrase and then trigger the `findSynonyms` method to execute by clicking the "Search" button.

If we look at `findSynonyms`, we see that it executes an axios call similar to the previous example. The big difference is that this call includes a little extra configuration object that defines an extra "parameter" for the API request. The parameter is called `ml` and it is set equal to the value the user typed into the `phrase` input.

The result of this configuration is that the API request has the parameters appended to it as query string parameters. If a user does a search for the word "logic", then the API request URL is:

```
https://api.datamuse.com/words/?ml=logic
```
If there user were to type in a different word, it would be appended to the URL instead of "logic". This allows the user to get the specific results they desire from our interface. 

The same technique for appending parameters to a request can be used to append API keys, other static parameters that make results more useful for users, and much more. We can also use expanded configurations of the `axios` call to change the request method or add other elements like authorization headers to the API request.

<div class="tip-box">
  <h3>Advanced JavaScript Concepts</h3>
  <p>The concepts of <b>arrow functions</b> and <b>promises</b> are difficult to grasp at first. In this book we have only explained them far enough to use these concepts in relation to the API calls we're making. However, there are many ways that arrow functions and promises can be used to enhance our code. Both of these features were added to JavaScript to address weaknesses that have bothered developers for ages. In the early stages of our development careers it might be difficult to grasp just how valuable they are, but as we progress and grow as developers we will see these concepts used more often.</p>
</div>














