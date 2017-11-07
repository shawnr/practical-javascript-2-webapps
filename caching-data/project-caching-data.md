# Project: Caching Data
This project uses the [Caching Data repository](https://github.com/suwebdev/wats4000-caching-data) as a starting point. Please fork and clone this repository to your preferred work environment.

For this project, we will add some user information storage and caching to the weather application we refactored a couple sections ago. We willwork with a weather application that could have come out of that prior refactoring experience.

The weather application has three major views: `CitySearch`, `CurrentWeather`,
and `Forecast`. These three views use several child components to display all of
their information. When we first open the repository, we can notice that there is
no way to save any data, and the site is making many requests to the weather API.

In order to improve the performance and user experience in our weather app, we
will add the ability for users to save favorite cities for easy viewing when
they return to the application. We will also cache our API queries so we do not
risk running into a rate limit, and so our users do not have to wait for
information to load as often.

These changes will dramatically enhance the utility and speed of our application.
To accomplish these changes, we will cache data into `localStorage` using the
`vue-ls` module. This module helps us manage our stored information more
efficiently and makes it a snap to provide expiration times on information.

In order to complete this project, we will edit several files in the repository.
Look for the `TODO` notes in the project files for guidance and indications of how we can accomplish
our goals.

## Review the Requirements
In order to successfully complete this project, we must fulfill the following requirements.

**`main.js`**
* Add the base configuration for `vue-ls`.

**`CitySearch.vue`**
* Add the `FavoriteCities` component as a child to the `CitySearch` component (using proper imports, etc.).
* Add logic to the `created` function to initialize `this.favorites` to the value of the `favoriteCities` object in `localStorage`.
* Add logic to the `saveCity` function to update the `favoriteCities` cache in `localStorage`.
* Add logic to properly cache the API request in the `getCities` method (with proper label and expiry time).

**`FavoriteCities.vue`**
* Add logic in the `removeCity` method to remove the city from the `this.favoriteCities` array.
* Add logic to the `removeCity` method to remove the city from `localStorage`.

**`CurrentWeather.vue`**
* Add logic to properly cache the API request in the `created` function (with proper label and expiry time).

**`Forecast.vue`**
* Add logic to properly cache the API request in the `created` function (with proper label and expiry time).

## Working the Project
In order to complete this project, we will edit several files in this repository. We begin with setting up `vue-ls` for use in our project.

### Configuring Vue LocalStorage

### Adding the `FavoriteCities` Component

### 

## Wrapping Up

## Build and Deploy
Once we've finished our work, we can build and deploy the project. This project has been configured to build to the `docs/` directory, so we can follow the same pattern we used before:

1. Execute the `npm run build` command to build the files into the `docs/` directory.
2. Commit all of our code.
3. Push the code up to GitHub.
4. Go into the repository settings and set the GH Pages section to publish from the `docs/` directory.

The project should now be up and available to the public through GH Pages.

## Stretch Goals
If we crave more challenge, we can attempt these additional goals.

* Add more preferences to the system, such as the ability to load a single "favorite" city when the page is first loaded (with no clicks or search required).
* Add the ability for users to specify their own label for the favorite cities (e.g. "home", "Aunt Barb's House", etc.).
* Add a query to another API service, such as flickr, to augment this information. Build the proper caching to make efficient use of that query, too.
* Add animated transitions to the information in this project.





