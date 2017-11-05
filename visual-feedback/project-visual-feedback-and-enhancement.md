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