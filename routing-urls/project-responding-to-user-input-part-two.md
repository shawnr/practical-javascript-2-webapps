# Project: Responding to User Input Part Two

In the previous section, we worked on the first part of [the Multi-View Application project](https://github.com/suwebdev/wats4000-multi-view-app). For this final part of the project, we should continue working on the repository we cloned in the last section. We will work a bit more with forms and explore how to set up simple routes in our application to provide bookmarkable locations for our users.

It's assumed that we've already forked, cloned, and set up our workspace. We should be able to continue from where we left off last time.

## Review the Requirements
In this second part of the project, we will set up another form and also some new routes in our application. The new routes will allow us to experiment with using `vue-router` to move the user to different locations within our site. The goal is to allow the user to click to the new member survey page, and then to move the user to the secret page once they have completed the survey successfully.

To do this, we will need to edit four files: Three components and the router definitions. There are `TODO` notes in each of the files to help us find what we need to edit, and we should be able to use the examples that came previously in this section to complete the work.

Here are the Basic Requirements outlined in the project `README`:

**In the `src/components/Survey.vue` file**
* Complete the survey form by filling in the TODO notes
* Use `v-for` loops in the template to create options for the checkbox groups
* Create a validation method to handle the rules outlined in the component comments
* Use a `$router.push` statement to move the user to the Secret page

**Create the `src/components/Secret.vue` file**
* Create a basic component from scratch called `Secret`
* The content of the `Secret` page should be something you come up with: A favorite tip about web development, a funny joke, a humorous image, etc.
* Provide links back to the other two pages using `<router-link>` tags in the template

**In the `src/router/index.js` file**
* Import the Survey component properly
* Import the Secret component properly
* Add the Survey component at the `/survey` path
* Add the Secret component at the `/secret` path

Please note: We will not be tackling these requirements exactly in order, but we will complete each of these.

## Working the Project
As we begin work we will need to have the following files open:

* `src/components/Home.vue`
* `src/components/Survey.vue`
* `src/components/Secret.vue`
* `src/router/index.js`

We will move between these files to complete all of the work for this project.

### Creating the Form in `Survey.vue`

### Adding the Survey View to the Routes Array

### Adding the Link to the Survey from the Home View

### Creating the Secret View

### Adding the Secret View to the Routes Array

### Finishing the Validation Method for the Survey


## Wrapping Up
Several files have been modified to complete this project. Here are the complete files so we can check our work against them.

### `src/components/Home.vue`

### `src/components/Survey.vue`

### `src/components/Secret.vue`

### `router/index.js`

## Build and Deploy
Once we've finished our work, we can build and deploy the project. This project has been configured to build to the `docs/` directory, so we can follow the same pattern we used before:

1. Execute the `npm run build` command to build the files into the `docs/` directory.
2. Commit all of our code.
3. Push the code up to GitHub.
4. Go into the repository settings and set the GH Pages section to publish from the `docs/` directory.

The project should now be up and available to the public through GH Pages.

## Stretch Goals

There are many more fun things we can do with this project. The `README.md` file lists several possible stretch goals:

* Add a navigation element to the `src/App.vue` template, and be sure to use the `router-link-active` class to style the current page link
* Add more pages of content to the site to practice creating new components from scratch and adding them to the routes Array

And it's still worthwhile to pursue the stretch goals from the previous portion of this project:

* Enhance the sign up form to collect additional info, different info, or to use different input types to collect the data
* Enhance the validation to be more specific (e.g. verify no numbers in the name, or there is an `@` and a `.` in the email address, etc.)
* Enhance error messages to be more specific (e.g. build a message that mentions which field is causing the problem)

There are many other ways we could push this forward. Feel free to explore and experiment with forms and methods to handle user input. Keep pushing, and have fun!












