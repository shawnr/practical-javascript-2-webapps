# Project: Visual Feedback and Enhancement

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
In order to complete this project, we will mainly be adding elements to enhance the messaging and visual presentation of the application. We must complete the following requirements, which will have us editing several files in the project. (Each file contains `TODO` notes, so look for those.) Here are the basic requirements:

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


### Add Messages to `addWord` Method

### Add Messages to `removeWord` Method

### Display Errors with Messages

## Wrapping Up
Now that we've completed the project, here are what each of our changed files look like in their entirety. We can reference these examples to check our own work.

**`WordSearch.vue`**

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
* Add animations to additional components to make the whole interface feel like jelly
* Add a shuffle feature to the wordlist along with the accompanying animation
* Make other layout or design improvements that help the application be more helpful to our users
