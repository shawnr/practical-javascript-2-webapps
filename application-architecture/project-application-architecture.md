# Project: Application Architecture and Refactoring Practice
The [Refactoring Practice project repository](https://github.com/suwebdev/wats4000-refactoring) provides you with a working weather application that can be improved through refactoring. 
The weather app uses three major views: City Search, Current Weather, and 5 Day Forecast. Users
can search for their city and then view weather data. The weather data is
requested from the [OpenWeatherMap.org API](https://openweathermap.org/), which
is free and available for any developer to use. (**NOTE:** You will need to
sign up to get an OpenWeatherMap.org API Key to complete this project.)

In the initial state, this application will work (once you insert your API key
into the proper locations), but the structure of the application could be
significantly improved. We will practice creating child components that can
accept data from the parent component, abstract base API configurations away
from each individual API call, and consolidate other HTML and CSS blocks to
minimize the pain of maintenance.

## Review the Requirements
In order to complete this project, we must fulfill the following Basic Requirements. These requirements are all focused around refactoring the application into a more organized structure that will make future maintenance and improvements easier. Remember that we are **not** trying to improve the performance or add any new features to the project. The goal here is purely around refactoring. The end result should appear to the user exactly like the current version.

* Sign up to [OpenWeatherMap.org](https://openweathermap.org/) and generate an API Key.
* Paste your API Key (which will be used as the `APPID` parameter) into the appropriate locations in the `CitySearch.vue`, `CurrentWeather.vue`, and `Forecast.vue` files.
* Verify the site works with your key. You should be able to search for a city and see weather data.
* Abstract the base configuration for the API requests to a common file to reduce duplication of the base URL and `APPID`.
* Create a child component called `WeatherDisplay` that can accept weather information and produce a well-formatted display.
* Use the child component in each of the views to eliminate the redundant HTML and CSS styles used.
* Create a child component called `ErrorList` to handle display of error messages. Replace the error message handling in the templates of the three parent components with this child component.
* Clean up any extraneous code, comments, or files that are unused.
* Add comments where they would be helpful to improve the readability of the project.

## Working the Project
In order to get this project working, we should first fork the repository from the main [Refactoring Practice repository](https://github.com/suwebdev/wats4000-refactoring), then we should clone the files to our local development area. We will need to install the project dependencies by running `npm install` from the project root directory.

### Make an OpenWeatherMap.org API Key
To get the project running, we need to make an account on [OpenWeatherMap.org](https://openweathermap.org/) and generate an API key. Once we have created an account, the API Keys can be found under our Account page ([located here](https://home.openweathermap.org/api_keys)). Create a new API Key and then open the project repository in a preferred editor. We must find the `YOUR_APPID_HERE` placeholders in the `CitySearch.vue`, `CurrentWeather.vue` and `Forecast.vue` files and replace those placeholders with our actual API Key (called an `APPID` by OpenWeatherMap.org).

Once we've replaced that information the project should become operational. Run `npm run dev` and verify that the project works. Once we've made sure the project is working, we can begin refactoring.

### Abstract the Base API Configuration
TODO

### Create `WeatherDisplay` Child Component
TODO

### Create `ErrorList` Child Component
TODO

### Clean Up Extraneous Files
There are several files that appear to be remnants of previous development. Clean up the extra file in the `src/components/` directory and the extra experimental data file. Take another pass through all of the code files and remove any extraneous `TODO` comments or other irrelevant comments.

### Enhance Comments
If we haven't already been conscientious about commenting our changes so developers reviewing our work will be able to tell how things work, then now is the time to go back through and do that work. We must leave comments that allow developers to more quickly understand non-obvious details about the code and how to use it.

## Wrapping Up

### Components
TODO

### Base API Configuration
TODO

## Build and Deploy
Once we've finished our work, we can build and deploy the project. This project has been configured to build to the `docs/` directory, so we can follow the same pattern we used before:

1. Execute the `npm run build` command to build the files into the `docs/` directory.
2. Commit all of our code.
3. Push the code up to GitHub.
4. Go into the repository settings and set the GH Pages section to publish from the `docs/` directory.

The project should now be up and available to the public through GH Pages.

## Stretch Goals

Stretch goals are provided to gain extra practice and a higher degree of challenge. If this work has been straightforward, then we are encouraged to keep pushing. There are several more opportunities to improve the organization and structure of this project, so feel free to keep honing it until it is as lean and mean as possible.

* Abstract the addition of the `&deg; F` formatting on temperatures to a filter used in a common file.
* Abstract the `formatDate` filter to a common file.
* Create a child component to provide navigation between city search, current weather, and forecast views. Implement this component on each URL.