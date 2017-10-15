# Responding to User Input Part One
For this section's project, we will begin work on a small sequence of forms that we will finish out in the next section. [The starter repository for this project is located here](https://github.com/suwebdev/wats4000-multi-view-app). As usual, we will begin by forking the repository on GitHub into our own account, and then cloning the repository to wherever we are doing our development. Once we have the project cloned into our development environment, we are ready to get started.

## Review the Requirements
As with all of our projects, we begin by reviewing the `README.md` file in the root of the repository. This file will tell us the requirements we must fulfill in order to successfully complete this project. For this first part of the project, we will focus on the requirements outlined for the `Home.vue` file. We will finish the remaining requirements in the next section of the book (Routing and URLs).

In its entirety, this project asks us to create a couple of forms and move the user through multiple locations in the application to complete those forms. For this first part of the project, we will focus primarily on creating and validating the sign up form. When the user provides valid data, we will display a success message. If the user provides invalid data, we will display an error message.

The Basic Requirements for this project are broken into requirements for each of the files. Stretch goals are provided that apply to all of the work in this project. We are encouraged to push this experiment as far as possible, so adding or altering form fields, adjusting validation logic, and providing more textured error messages are all fair game for stretching this project in this section. (But remember, to fully complete the project we must complete the second part in the Routing and URLs section.)

## Working the Project 
To begin working on the file, it is necessary to install our dependencies (by running `npm install` inside the project repository), and then we will want to run our development server (by running `npm run dev` inside the project repository). Once we have the project running, we will see this in the browser:

![Home view](/img/project8_starterHello.png)
<br>Home view

Work on this part of the project will happen in the `src/components/Home.vue` file. This file contains the `Home` component, which controls the first page of our project website. In the initial state, the view contains no form input fields and it shows the success message right away. We must fill in the details to make this a functioning sign up form. 

### Show/Hide Form and Thank-You Message
We begin with a set of data defined in the component's `data` object. One of those data values is `showForm`, which is set to `true` by default. The first `TODO` in the file tells us to modulate the display of the form container (`<div class="form-container">`). If we glance down a little further, we can see that we also need to modulate the display of the `<div class="success-message">` element, which contains the success message the user should see after successfully submitting the form. We can tackle both of these `TODOs` at once.

First, we can add a `v-show` directive to the `<div class="form-container">`:

```html
<div class="form-container" v-show="showForm">
```
If `showForm` is `true` (which it is at the beginning), this form container will be shown. Remember that `v-show` accepts a conditional statement, so we can use conditional operators with the `v-show` directive, too. We will do that to hide the success message until the right time. 

In order to handle the show/hide of the success message, we can add another `v-show` directive to that element:

```html
<div class="success-message" v-show="!showForm">
```
In this case, we want to show the success message when the form is NOT showing. Essentially, the success message is the opposite of the form container. We use the `!showForm` syntax to specify that when `showForm` is `false`, this element should be shown. Once we implement these two `v-show` directives, we should see that the success message is hidden by default:

![Hiding the success message](/img/project8_showhide.png)
<br>Hiding the success message

### Create Error Message
The next `TODO` we come across asks us to make an error message and use `v-show` to make it appear when the form has an error. First, we must add the element that we will modulate. If we glance at the styles defined in the `Home` component, we can see there is a class defined to style an error element: `.error`. We will use that class and add the following to the component template:

```html
<p class="error" v-show="showError">Please check the information you have entered. Be sure to fill in all fields.</p>
```
By default, this warning will not show up. In order to complete our work here, we must alter the `showError` value in the component to be `true`. If we just adjust the value where it is defined in the `data` object we can see the error message:

![Error message displayed](/img/project8_errorMessage.png)
<br>Error message displayed

Now we can reset the initial value of `showError` to be `false` (we don't want to show the error when the user first arrives on the site), and we can alter the value in the `validateForm` method accordingly.



## Wrapping it Up

## Build and Deploy
Once we've finished our work, we can build and deploy the project. This project has been configured to build to the `docs/` directory, so we can follow the same pattern we used before:

1. Execute the `npm run build` command to build the files into the `docs/` directory.
2. Commit all of our code.
3. Push the code up to GitHub.
4. Go into the repository settings and set the GH Pages section to publish from the `docs/` directory.

The project should now be up and available to the public through GH Pages.

## Stretch Goals

There are many more fun things we can do with this project. The `README.md` file lists several possible stretch goals:

* Enhance the sign up form to collect additional info, different info, or to use different input types to collect the data
* Enhance the validation to be more specific (e.g. verify no numbers in the name, or there is an `@` and a `.` in the email address, etc.)
* Enhance error messages to be more specific (e.g. build a message that mentions which field is causing the problem)

There are many other ways we could push this forward. Feel free to explore and experiment with forms and methods to handle user input. Keep pushing, and have fun!












