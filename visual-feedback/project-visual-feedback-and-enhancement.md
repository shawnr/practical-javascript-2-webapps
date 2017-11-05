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

* Use the `showSpinner` value to modulate the display of the `CubeSpinner` component when appropriate
* Add an animation to the items of the WordList for when new items are added and removed
* Add an animation to the items of the results list when a search is completed
* Add messaging to results display area let the user know when no results are found
* Add global messaging child component (`MessageContainer`) to `WordSearch` component
* Add a global "success" message to let the user know that a word has been successfully added to the WordList
* Add a global "info" message to let the user know when they try to add a word to the WordList that has already been added
* Add a global "success" message to let the user know that a word has been successfully removed from the WordList
* Add a global "error" message to display any errors from the API request (aside from "no results found")

## Working the Project

## Wrapping Up
Now that we've completed the project, here are what each of our changed files look like in their entirety. We can reference these examples to check our own work.



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
