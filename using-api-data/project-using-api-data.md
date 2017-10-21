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


## Wrapping Up

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













