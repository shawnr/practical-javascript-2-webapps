# Project: Visual Feedback and Enhancement
This project uses the [Visual Enhancement starter repository](https://github.com/suwebdev/wats4000-visual-enhancement). Be sure to fork and clone this repository to get started.

For this project, we will revisit the Datamuse API to enhance the search tools
we worked with a few projects ago. We will present one search with multiple
options, and we will allow users to save their results to a "Word List" so they
can more effectively browse for words.

This project is mostly built, but it requires some love and affection by way of
visual enhancements to make it more useful. With such a complex search tool, it
is possible for users to get no results. When that happens, we don't want them
to think the application has malfunctioned.

We are also updating information in the search results and in the sidebar Word
List. We want to use messages and animation to help users identify when data in
these areas of the page has changed.

To make it a little easier to create professional quality animations, we will
rely on the [`vue2-animate` project](https://github.com/asika32764/vue2-animate),
which makes a set of common animations available for use with Vue.js transition
components. We will also use a load spinner from Spinkit.

## Review the Requirements
In order to complete this project, we will mainly be adding elements to enhance the messaging and visual presentation of the application. We must complete the following requirements, which will have us editing the `src/components/WordSearch.vue` file. (Each requirement corresponds to the `TODO` notes, so look for those.) Here are the basic requirements:

* Use the `showSpinner` value to modulate the display of the `CubeSpinner` component when appropriate
* Add an animation to the items of the results list when a search is completed
* Add an animation to the items of the WordList for when new items are added and removed
* Add messaging to results display area let the user know when no results are found
* Add global messaging child component (`MessageContainer`) to `WordSearch` component
* Add a global "success" message to let the user know that a word has been successfully added to the WordList
* Add a global "info" message to let the user know when they try to add a word to the WordList that has already been added
* Add a global "success" message to let the user know that a word has been successfully removed from the WordList
* Add a global "error" message to display any errors from the API request (aside from "no results found")

## Working the Project
The following guide offers a walkthrough of how to complete almost every aspect of the project. 

### Add `CubeSpinner` to Indicate Loading
Like many of the tasks in this project, this one should be familiar based on the previous project. We will add the `import` statement for the `CubeSpinner` component, and then will add the component to the list of components. Once we have done that, we will add the `<spinner>` element to our template. We will use a regular `v-if` directive on the `<spinner>` element to determine whether or not to show the spinner. Here is what the basic implementation looks like:

**template**
```html
<spinner v-if="showSpinner"></spinner>
```

**script**
```html
import CubeSpinner from '@/components/CubeSpinner';

export default {
  name: 'WordSearch',
  components: {
    spinner: CubeSpinner
  },
  // ... additional code ... //
```
This is just like how we added the child components in the previous project. Now we must modulate the value of `this.showSpinner` from within the `findWords` method in order to control the show of the loading spinner. Here is how we can do that:

```js
findWords: function() {
  // Show spinner when API request begins here.
  this.showSpinner = true;
  this.results = null;
  axios.get('https://api.datamuse.com/words', {
    params: {
      ml: this.phrase,
      sl: this.soundsLike,
      sp: `${this.startLetter}*${this.endLetter}`
    }
  })
  .then( response => {
    // Turn off spinner.
    this.showSpinner = false;
    this.results = response.data;
  })
  .catch( error => {
    // Turn off spinner.
    this.showSpinner = false;  
  })
}
```
As we can see here, we can easily use the structure of the API request to turn on and off the spinner animation to indicate loading. Usually, the Datamuse API loads very quickly, but on slower connections or for more complex searches this loading spinner will help our users know exactly what is happening in the app. 

![Load Spinner](/img/project-12-load-spinner.gif)
<br>Load Spinner

Now we should be able to test and see that we have a load spinner showing up whenever the application is requesting data from the server.

### Animate the Items in the Search Results
To animate the items in the search results, we can wrap the list items in a `<transition-group>` element. We must also add a `key` attribute to each list item (`key` attributes are required whenever we use a `<transition-group>`).

```html
<transition-group name="fade" tag="div" appear>
  <li v-for="item in results" class="item" v-bind:key="item.word">
    <p class="result-word">{{ item.word }}</p>
    <p><button v-on:click="addWord(item.word)" class="add-word">Add to WordList</button></p>
  </li>
</transition-group>
```

Here we are using the `item.word` value as the `key`, and we have set the `tag` attribute on the `<transition-group>` to `"div"`. This will wrap the set of list items in a `div` tag (as opposed to the default `<span>` tag that the `<transition-group>` uses).

At this point, we should notice that this project has the `vue2-animate` module added. We can see the module listed in our `package.json` file. And we can notice at the top of the logic in our `WordSearch` component is a somewhat odd-looking line:

```js
require('vue2-animate/dist/vue2-animate.min.css');
```
The `vue2-animate` module is unusual because it is only a CSS file. It contains style classes that have been defined to work with the conventions of the `Vue.js` transition system. This means that we can access a large range of premade animations by simply naming our `<transition-group>` with the name of the animation. In the case above, we will see the items in the results list fade in. We can get a better idea of all the animations `vue2-animate` makes available by looking at [the `vue2-animate` Demo Page](http://about.asika.tw/vue2-animate/).

Experiment with a different animation and see what it looks like. It is easy to switch between animations and trying different animations will help us get an idea for how the system works.

### Animate the items in the Word List
Animating the items in the Word List works almost exactly the same way as the items in the results list. We can wrap the list items in a very similar `<transition-group>` element. We make the same changes to add a `key` to the list items and set the `name` and `tag` attributes of the `<transition-group>`.

```html
<transition-group name="slideRight" tag="div" appear>
  <li v-for="word in wordList" v-bind:key="word">{{ word }}&nbsp;<button v-on:click="removeWord(word)" class="remove-word">x</button></li>
</transition-group>
```
Notice that this time we have used the `slideRight` animation. We also have the `appear` attribute on the `<transition-group>` to make sure the animation will be shown even when the first item is added to the list. We are using the `word` value as the `key` for each list item. 

It's worthwhile to notice that when we remove a word from the list, the opposite animation happens. This is a feature of the way the `vue2-animate` styles have been defined. They combine animations to work for both entry and exit. Try different animations and see what it looks like when words are added to the list or removed.

### Add `MessageContainer` for Global Messages
A `MessageContainer` component has been provided to handle display of messages. These components can be easy to create for basic purposes, but it's also very common to use third-party components to display messages in our applications. It all depends on our specific project needs.

To use the `MessageContainer`, we need to import it into the `WordSearch` component and add it to the list of components used in `WordSearch`. This is very similar to how we previously imported and set up the `CubeSpinner` component.

```html
<script>
import axios from 'axios';
require('vue2-animate/dist/vue2-animate.min.css');

import CubeSpinner from '@/components/CubeSpinner';
import MessageContainer from '@/components/MessageContainer';

export default {
  name: 'WordSearch',
  components: {
    spinner: CubeSpinner,
    'message-container': MessageContainer
  },
  // ... more script ... //
</script>
```

Once we have added the child component to `WordSearch`, we can use it in the template:

```html
<message-container v-bind:messages="messages"></message-container>
```
The `MessageContainer` component looks for a property called `messages`, which we want to bind to the `messages` data value in the `WordSearch` component. Now we can cause messages to be displayed by adding or removing messages to the `messages` array inside of `WordSearch`.

### Add Messages to `addWord` Method
Adding messages is just a matter of pushing a `message` object into the `messages` array. The `message` object expects two properties: `type` and `text`. This allows the `MessageContainer`, and the `MessageItem` child component it uses, to properly display each message. Here is how we can add a message to indicate that a word has been added to the Word List:

```js
addWord: function (word) {
  if (this.wordList.indexOf(word) === -1) {
    this.wordList.push(word);
    this.messages.push({
      type: 'success',
      text: `${word} added to WordList.`
    });
  } else {
    this.messages.push({
      type: 'info',
      text: `${word} is already on the WordList.`
    });
  }
}
```
In the `addWord` method, we receive `word` as an argument. This `word` is compared to the existing `this.wordList` array to see if it already exists in the list. If the `word` is not found in the array, then it is a new word, and it is added to `this.wordList`. We also add a `message` object to the `this.messages` array with the `type` set to `"success"` and the `text` set to a helpful message.

If the `word` already exists in the `this.messages` array, then we do not re-add the word, and we instead create an "info" message that lets the user know why the word was not added. This is a common situation when allowing users to add items to a list of things.

### Add Messages to `removeWord` Method
Adding the message creation to the `removeWord` method is even easier than adding it to the `addWord` method because there is only one case. We can add it like so:

```js
removeWord: function (word) {
  this.wordList.splice(this.wordList.indexOf(word), 1);
  this.messages.push({
    type: 'success',
    text: `${word} removed from WordList.`
  });
}
```
We use the `splice()` method, which exists on every JavaScript Array, to remove the word we're after. Once we've done that, we alert the user. Once we get the hang of this, it becomes very easy to add messages to all the parts of our application.

Now we should see pretty much all of these features at play in our application:

![Add/Remove Words](/img/project-12-addremove-word.gif)
<br>Add/Remove Words

### Display Errors with Messages
The last place we need to add message display is to our possible API errors. We want the user to know if our application is malfunctioning because of the API; otherwise, they will assume that our application is broken and never realize that the API we depend upon is having troubles. It might be cold comfort, but it makes us feel better as developers to let our users know that we're still looking out for them even when things are going wrong beyond our control.

Adding messages to the error clause of our API request is almost the same as adding them everywhere else:

```js
.catch( error => {
  this.showSpinner = false;
  this.messages.push({
    type: 'error',
    text: error.message
  });
})
```
The only unique thing here is that we are using the `"error"` type of message, and our message content is coming from the `error` object returned by `axios` when a request goes wrong. If we want to test these messages we can do so by adding some bogus characters to the domain of our API server and then viewing our site. When we click "search" we should see a "Network Error" show up.

## Wrapping Up
Now that we've completed the project, here is what the `WordSearch.vue` file looks like:

```html
<template>
  <div>
    <div class="messages">
      <message-container v-bind:messages="messages"></message-container>
    </div>
    <div class="word-search">
      <form v-on:submit.prevent="findWords">
        <p><label>Find synonyms for <input type="text" v-model="phrase" placeholder="word or phrase"> that:</label></p>
        <ul>
          <li><label>sounds like <input type="text" v-model="soundsLike" placeholder="word or phrase"></label></li>
          <li><label>start with the letter <input type="text" v-model="startLetter" placeholder="single letter"></label></li>
          <li><label>end with the letter <input type="text" v-model="endLetter" placeholder="single letter"></label></li>
        </ul>
        <p><button type="submit">Search</button></p>
      </form>
    </div>
    <div class="word-list-container">
      <h2>Word List</h2>
      <ul class="word-list">
        <transition-group name="slideRight" tag="div" appear>
          <li v-for="word in wordList" v-bind:key="word">{{ word }}&nbsp;<button v-on:click="removeWord(word)" class="remove-word">x</button></li>
        </transition-group>
      </ul>
    </div>
    <div class="results-container">
      <spinner v-if="showSpinner"></spinner>
      <h2 v-if="results && results.length > 0">{{ results.length }} Words Found</h2>
      <ul v-if="results && results.length > 0" class="results">
        <transition-group name="fade" tag="div" appear>
          <li v-for="item in results" class="item" v-bind:key="item.word">
            <p class="result-word">{{ item.word }}</p>
            <p><button v-on:click="addWord(item.word)" class="add-word">Add to WordList</button></p>
          </li>
        </transition-group>
      </ul>
      <div v-else-if="results && results.length === 0" class="no-results">
        <h2>No Words Found</h2>
        <p>Please adjust your search to find more words.</p>
      </div>

    </div>
  </div>
</template>

<script>
import axios from 'axios';
require('vue2-animate/dist/vue2-animate.min.css');
import CubeSpinner from '@/components/CubeSpinner';
import MessageContainer from '@/components/MessageContainer';

export default {
  name: 'WordSearch',
  components: {
    spinner: CubeSpinner,
    'message-container': MessageContainer
  },
  data () {
    return {
      results: null,
      wordList: [],
      messages: [],
      phrase: '',
      soundsLike: '',
      startLetter: '',
      endLetter: '',
      showSpinner: false
    }
  },
  methods: {
    addWord: function (word) {
      if (this.wordList.indexOf(word) === -1) {
        this.wordList.push(word);
        console.log(`Added ${word} to wordList.`);
        this.messages.push({
          type: 'success',
          text: `${word} added to WordList.`
        });
      } else {
        console.log('Word is already on wordlist.');
        this.messages.push({
          type: 'info',
          text: `${word} is already on the WordList.`
        });
      }
    },
    removeWord: function (word) {
      this.wordList.splice(this.wordList.indexOf(word), 1);
      this.messages.push({
        type: 'success',
        text: `${word} removed from WordList.`
      });
    },
    findWords: function() {
      this.showSpinner = true;
      this.results = null;
      axios.get('https://api.datamuse.com/words', {
        params: {
          ml: this.phrase,
          sl: this.soundsLike,
          sp: `${this.startLetter}*${this.endLetter}`
        }
      })
      .then( response => {
        this.showSpinner = false;
        this.results = response.data;
      })
      .catch( error => {
        this.showSpinner = false;
        this.messages.push({
          type: 'error',
          text: error.message
        });
      })
    }
  }
}
</script>

<style scoped>
.word-search {
  font-size: 1.2rem;
  white-space: nowrap;
  display: inline-block;
  width: 70%;
  float: left;
}
.word-list-container {
  display: inline-block;
  width: 25%;
  background: #e8e8e8;
  padding: 0.5rem;
}
.results-container {
  clear: both;
}
input[type="text"]{
  border-top: none;
  border-left: none;
  border-right: none;
  border-bottom: 1px solid #333;
  width: 300px;
  font-size: 1.2rem;
  color: #2c3e50;
  font-weight: 300;
  background: rgba(0,0,0,0.02);
  padding: 0.5rem;
}
button{
  background: #333;
  padding: 0.5rem;
  font-weight: 300;
  color: #fff;
  border: none;
  cursor: pointer;
  font-size: 1.4rem;
  border-radius: 0;
}
button.add-word {
  background: #e8e8e8;
  color: #333;
  font-size: 0.8rem;
}
button.add-word:hover {
  background: #fde300;
}
button.remove-word {
  font-size: 0.5rem;
  padding: 2px;
  display: inline-block;
  color: #333;
  background: none;
}
button.remove-word:hover {
  background: #aa0000;
  color: #fde300;
}
h1, h2 {
  font-weight: normal;
}
ul.results, ul.word-list {
  list-style-type: none;
  padding: 0;
}
.word-list li {
  margin: 5px 0;
  padding: 5px 0;
  border-bottom: 1px solid #333;
}
.results li {
  display: inline-block;
  margin: 10px;
  border: solid 1px #333;
  padding: 0.5rem;
  width: 200px;
  min-height: 100px;
  color: #fff;
  font-weight: 300;
  font-size: 1.2rem;
  background: rgba(0,0,0,0.7);
}
ul.errors {
  list-style-type: none;
}
.errors li {
  border: 1px solid red;
  color: red;
  padding: 0.5rem;
  margin: 10px 0;
}
a {
  color: #42b983;
}
</style>
```

## Build and Deploy
Once we've finished our work, we can build and deploy the project. This project has been configured to build to the `docs/` directory, so we can follow the same pattern we used before:

1. Execute the `npm run build` command to build the files into the `docs/` directory.
2. Commit all of our code.
3. Push the code up to GitHub.
4. Go into the repository settings and set the GH Pages section to publish from the `docs/` directory.

The project should now be up and available to the public through GH Pages.

## Stretch Goals
If we crave more challenges, try tackling some of these suggestions.

* Try making custom animations for everything, and don't use `vue2-animate` animations at all
* Add a shuffle feature to the wordlist along with the accompanying animation
* Make other layout or design improvements that help the application be more helpful to our users
