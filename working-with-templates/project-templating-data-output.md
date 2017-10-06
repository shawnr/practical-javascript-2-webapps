# Project: Templating Data

For this project, we will practice with some of the techniques used to output data in the template. We will use the [Templates and Data Starter Repository](https://github.com/suwebdev/wats4000-templates-and-data) to provide the data and basic application structure for this project.

As usual, the project repository defines a set of requirements that we must fulfill in order to complete this project. It's recommended to read through all of the directions before we begin working, and it might be preferable to work on the project before continuing to read through this section. If you become stuck, a full walkthrough of the project continues below.

As with all of the projects, we should begin by forking the starter repo to our own GitHub account, and then cloning it to our workspace.

## Review the Directions and Data
The `README.md` file for the project outlines the requirements for completion and provides some ideas for how to push the project further if we crave additional challenge. Before we get too deep in working on this challenge, it's worthwhile to review the JSON object in the `src/apiresults.js` file. This JSON object is a captured result from [The Movie Database API](https://themoviedatabase.org). It contains the top 20 movies from the 20th Century, sorted in order of popularity. We can see from the results that there are about 147,445 movies from the 20th Century in the TMDb system, but we are only seeing the top 20 most popular.

In the data we will notice some "metadata" about the search itself: How many total results, what page we're looking at, and how many total pages there are. We can also see an array called `results` that contains objects representing each of the 20 movies in the list. These objects all have the same data points:

```js
{
  "vote_count":3676,
  "id":78,
  "video":false,
  "vote_average":7.9,
  "title":"Blade Runner",
  "popularity":105.797529,
  "poster_path":"/p64TtbZGCElxQHpAMWmDHkWJlH2.jpg",
  "original_language":"en",
  "original_title":"Blade Runner",
  "backdrop_path":"/k36huckDH0v3LP1zo7maFt3mJC0.jpg",
  "adult":false,
  "overview":"In the smog-choked dystopian Los Angeles of 2019, blade runner Rick Deckard is called out of retirement to terminate a quartet of replicants who have escaped to Earth seeking their creator for a way to extend their short life spans.",
  "release_date":"1982-06-25",
  "genres":[
    "Science Fiction",
    "Drama",
    "Thriller"
  ]
}
```
When we loop through each of the results in our template, each of these data objects will become available to our template. We can rely on each object having these same data points, and we can write our template accordingly. We will need to refer back to these property names so we can be sure to spell and capitalize everything properly.

## Working the Project
First, be sure we have run `npm install` in the project repository to install the application dependencies. When that finishes, we can run `npm run dev` to run the development server. We should see the beginning template provided in the repository:

![Starter template](/img/project-7-starter_repo.png)
<br>Starter template

To begin working the project, we should open up the `src/components/Results.vue` file. This file contains the template that we need to alter in order to display our work. When we first open the file, we can see that the template is full of static information, and it only shows one movie result. Our goal is to enhance this template to make it dynamic so it can show the full set of data we have in the `src/apiresults.js` file. This data is revealed to the template context. We will access this data in our template in order to fill in the proper information.

### Search Metadata
Most search interfaces provide us with "metadata" about the search itself: How many items were found, how many pages there are, and what page we are currently viewing. This information is present at the top of the JSON object returned by TMDb. We must output the data into the proper area of the template:

```html
<p class="search-meta">
  <span class="current-page"><b>Current Page:</b> 1</span>
  <span class="total-pages"><b>Pages:</b> 777</span>
  <span class="total-results"><b>Count:</b> 3232</span>
</p>
```

The relevant values in the root of the JSON object are:

```js
"page":1,
"total_results":147445,
"total_pages":7373,
```

So we can add those values to our template by using basic data interpolation and their property names:

```html
<p class="search-meta">
  <span class="current-page"><b>Current Page:</b> {{ page }}</span>
  <span class="total-pages"><b>Pages:</b> {{ total_pages }}</span>
  <span class="total-results"><b>Count:</b> {{ total_results }}</span>
</p>
```
This is the basic way we interpolate data into our templates. Since these properties all exist at the root (main level) of the JSON object, we can just use their names to reference them.

### Movie Items

The meat of the page is really the movie items themselves. The HTML structure for the movie items has been provided for you: These will be formed by list items (`<li>` elements) within an unordered list. This is a convenient way to format these elements, and we can add all sorts of HTML elements within each `<li>` in order to achieve our desired effect.

The overall structure of each movie item is this:

```html
<li class="movie-item">
  <img src="https://image.tmdb.org/t/p/w150_and_h225_bestv2/p64TtbZGCElxQHpAMWmDHkWJlH2.jpg" alt="Title of Movie Poster" class="poster-image">
  <h2 class="title"><a href="https://www.themoviedb.org/movie/78">Movie Title Goes Here</a></h2>
  <div class="ratings">
    <span class="rating-category critics-choice">Critic's Choice</span>
    <span class="rating-category well-liked">Well Liked</span>
    <span class="rating-category stinker">Stinker</span>
    <span class="vote-average">8.4</span> with <span class="vote-count">3676</span> votes 
  </div>
  <p class="overview">
    Movie overivew goes here. Aenean tellus metus, bibendum sed, posuere ac, mattis non, nunc. Cras dapibus. Praesent porttitor, nulla vitae posuere iaculis, arcu nisl dignissim dolor, a pretium mi sem ut ipsum.
  </p>
  <p class="release-date">Original Release: 1999-12-31</p>
  <ul class="genre-list">
    <li>genre</li>
  </ul>
</li>
```

The first thing we need to do is set up the loop that will 


## Wrapping it Up

The final result of all this work is the following finished template:

```html
<template>
  <div class="results">
    <h1>Top Movies from the 20<sup>th</sup> Century</h1>
    <p class="search-meta">
      <span class="current-page"><b>Current Page:</b> {{page}}</span>
      <span class="total-pages"><b>Pages:</b> {{total_pages}}</span>
      <span class="total-results"><b>Count:</b> {{total_results}}</span>
    </p>

    <ul>
      <li class="movie-item" v-for="result in results">
        <img v-bind:src="'https://image.tmdb.org/t/p/w150_and_h225_bestv2'+ result.poster_path" alt="Title of Movie Poster" class="poster-image">
        <h2 class="title"><a v-bind:href="'https://www.themoviedb.org/movie/'+result.id">{{ result.title }}</a></h2>
        <div class="ratings">
          <span class="rating-category critics-choice" v-if="result.vote_average > 8">Critic's Choice</span>
          <span class="rating-category well-liked" v-if="(result.vote_average > 7) && (result.vote_average <= 8)">Well Liked</span>
          <span class="rating-category stinker" v-if="result.vote_average <= 7">Stinker</span>
          <span class="vote-average">{{ result.vote_average }}</span> with <span class="vote-count">{{ result.vote_count }}</span> votes
        </div>
        <p class="overview">
          {{ result.overview }}
        </p>
        <p class="release-date">Original Release: {{ result.release_date }}</p>
        <ul class="genre-list">
          <li v-for="genre in result.genres">{{genre}}</li>
        </ul>
      </li>
    </ul>
  </div>
</template>
```















