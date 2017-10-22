# Project: Using API Data

In this project, we will use the [Using APIs](https://github.com/suwebdev/wats4000-using-apis) repository as our starting point. This project asks us to create a rhyming thesaurus using the [Datamuse API](http://www.datamuse.com/api/). The Datamuse API is a wonderful tool that allows us to do all sorts of interesting look-ups to find suggested words. In this project, we will be looking for words that rhyme with one word (or phrase), but which also have some relation to another word (or phrase): a rhyming thesaurus. This is a tool that could be incredibly useful for poets, songwriters, battle rappers, and many others.

**Please note:** There are many features in the Datamuse API that can be used to create other types of applications ranging from avant garde algorithmic poetry to pragmatic, helpful writing tools. Feel free to explore the many possibilities of this free and open API.

## Review the Requirements
This project requires us to make an API call when the user clicks a search button. We want to take some input from the user, which we will use to form our API request. First, we will walk through tasks outlined in the `Rhymesaurus.vue` file, which guides us toward creating the rhyming thesaurus interface. Then, we are asked to create a brand new Vue.js component that makes use of a different API call to the Datamuse API. Our goal is to link together the Rhymesaurus and our new tool within our site so users can access whichever they need.

Here are the Basic Requirements from the project's `README.md` file:

**`/src/components/Rhymesaurus.vue`**

`<template>`

* Set up an event handler to trigger the `findWords` method when the `form` is submitted
* Use a conditional to control the display of the `ul.results` element so it only displays when results are ready to be shown
* Use a loop to process all of the results into list items
    * Output the word in each list item
    * Output the score for each word in each list item
* Use a conditional to control the display of the `.no-results` message, which should only show when the user has attempted a search and no words have been found
* Use a conditional to control the display of the `ul.errors` element so it only displays when there are errors ready to be shown
* Use a loop to process all of the errors and display them for the user

`<script>`

* Import axios for use in the component logic
* Create a method called `findWords` (don't neglect to add the `methods` attribute to this component)
* Within the `findWords` method, create an `axios.get()` statement that will make a request to `https://api.datamuse.com/words`
    * Define the `params` for `ml` (which should map to the `phrase`) and `rel_rhy` (which should map to the `rhyme`)
    * Define a `then` clause that sets the component's `results` value to the value of `response.data`
    * Define a `catch` clause that will add any error to the `errors` array in the component

**`/src/components/NewComponent.vue`**

(Please do not actually name the new component `NewComponent.vue`. This name is only being used for reference here. Name the component according to whatever feature it provides.)

* Create a new component (use the boilerplate component code, or copy the component you just created)
* Refer to the Datamuse API documentation to determine a way to modify your code to provide an alternative way to find words (e.g. "sounds like", "related to", "adjectives that go with a word", "words that often follow a word", etc.).
* Implement a similar interface to perform this new search
    * Create the necessary template to allow the user to enter at least one search parameter
    * Create the necessary method to handle the form submission and API request
* Implement the proper template elements to output the results to the user
    * Show all relevant results returned by the API
    * Show all errors to the user
    * Show a message when no results have been found, so the user knows the system is working even though the data is not there

**`/src/router/index.js`**

* Add the new component to the import statements in the router definitions file
* Add the new route to the router definitions list (use a sensible URL and name for it)

**both `/src/compnents/Rhymesaurus.vue` and `/src/components/NewComponent.vue`**

* Add navigation elements to provide links between the two search pages
* Use proper `router-link` tags to create links
* Allow the user to easily switch between the two pages in the application.

## Working the Project
For this project walkthrough, we will focus on the initial work to complete the rhyming thesaurus. After we finish that work, we will offer some guidance to putting together the new component, but that will primarily be left as a challenge to complete based on understanding from previous sections and projects. Refer back to how we previously created new components and set up new route definitions in the [Responding to User Input](/routing-urls/project-responding-to-user-input-part-two.md) project.

### Set Up the API Request
Rather than jumping immediately into the template work, it's probably more streamlined for us to write the API request so we can test it as we build out our template features. The first `TODO` in the `<script>` area of the `Rhymesaurus.vue` component asks us to import `axios` for use in our `findWords` method. Assuming we have installed `axios` in the project with the standard `npm install --save axios` command, this import statement should work:

```js
import axios from 'axios';
```

That makes the `axios` object available within our component logic, so we can then write the `findWords` method. To add the `findWords` method, we must create the `methods` property on the component object. Then, we can define `findWords` like so:

```js
methods: {
  findWords: function(){
    axios.get('https://api.datamuse.com/words', {
      params: {
        ml: this.phrase,
        rel_rhy: this.rhyme
      }
    })
    .then(response => {
      this.results = response.data;
    })
    .catch(error => {
      this.errors.push(error);
    });
  }
}
```
As we can see, `findWords` is a fairly simple method that uses `axios` to make a call to the Datamuse API. The request to the API is formed around the `ml` and `rel_rhy` parameters. These two parameters are explained in the [Datamuse API Documentation](http://www.datamuse.com/api/) (keep that link handy because we'll refer to it later on, when we build our new component). The `ml` parameter indicates "means like", which returns synonyms for words and phrases. The `rel_rhy` parameter attempts to find words that rhyme with the supplied words. By combining these parameters we can find words or phrases that are synonymous with `this.phrase` and which also rhyme with `this.rhyme`. 

Notice that in addition to the URL for the API request, we have also supplied a configuration object in the `axios.get()` call. This configuration object only specifies `params` at the moment, but if we needed we could specify other types of configuration options (e.g. `headers`, `transformResponse` functions, etc.). It's critical that the `params` property names match the parameter names used by whatever API we are calling (in this case, the Datamuse API). Refer to the API documentation for the specific names an API uses and then use those in the `params` object when setting up `axios` requests.

This is an example of the kind of unorthodox tool we can build by using discrete features of an API. There are plenty of tools and books to look up rhymes for words (we call them  "rhyming dictionaries"). And there are tools and books to look up synonymous words (we call that a "thesaurus"). But what we are creating here is a "rhyming thesaurus", which is a much more unusual type of tool. It's also the kind of cross-lookup that would be difficult to replicate in print, making it especially suitable for building as a software application.

If we are using Postman (which we should be using) to test our API queries, we can try something like this:

```html
https://api.datamuse.com/words?ml=test&rel_rhy=ham
```
This API request should return words that are synonymous with "test" and also rhyme with "ham". The list should include "exam" and variations on that word. If we test that query in Postman, we can see the results we hope for:




## Wrapping Up
TODO


## Build and Deploy
Once we've finished our work, we can build and deploy the project. This project has been configured to build to the `docs/` directory, so we can follow the same pattern we used before:

1. Execute the `npm run build` command to build the files into the `docs/` directory.
2. Commit all of our code.
3. Push the code up to GitHub.
4. Go into the repository settings and set the GH Pages section to publish from the `docs/` directory.

The project should now be up and available to the public through GH Pages.

## Stretch Goals

There are many more fun things we can do with this project. The `README.md` file lists several possible stretch goals:

* Create a similar application using a different API. ([Find suggested APIs for experimenting with here](https://shawnr.gitbooks.io/practical-javascript-2-building-applications/appendices/appendix-b-api-suggestions.html).)
* Add a second API to this application and mingle the results in some interesting way
* Use the "score" data from the API to modify the visual presentation of the words to indicate which ones are the best matches for the user's search parameters
* Use the data returned from the API to modify the appearance or interface in some other way

There are many other ways we could push this forward. Feel free to explore and experiment with the many other features of the Datamuse API and all the things we can build with it.













