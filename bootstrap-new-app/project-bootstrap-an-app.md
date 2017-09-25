# Project: Bootstrap an App

To practice with making an application using the Vue-CLI tool, let's bootstrap an app that we can work with in sections 5 (Debugging the App) and 6 (Deploying the App) to practice working with the project skeletons we can create.

## Check for Vue-CLI
If we have Vue-CLI installed properly, then we can run the command `vue --version` from anywhere on our command line and see the version of the Vue-CLI that we have installed. We should see a number above `2.8`. If we see an error (something about the `vue` command not existing), then we should install Vue-CLI by running this command:

```
npm install -g vue-cli
```

## Bootstrap the Application
Once we have Vue-CLI properly installed, we can bootstrap our project skeleton. This will create all the files we need to get started writing our application. Create a new app using the `webpack` template:

```
vue init webpack test-project
```

Answer the questions like we see in the screenshot below:

![vue init results](/img/vue-init.png)
<br>The results of the `vue init` command.

Once the project skeleton is available, `cd` into the directory where your project was created.

## Install Dependencies
After creating the project skeleton, we still need to install the Node modules that the project depends upon. We do this with the command:

```
npm install
```

Once the installation is complete, we can test the project by running:

```
npm run dev
```

We should see the development server start up and a new tab should open in the default web browser with our project loaded.

![Default screen from webpack project template](/img/vue-default-web.png) 
<br>Default screen from Webpack project template

If we see a screen that looks like the one above, then we have successfully installed our dependencies and our project is up and running. Now that we have a working project, we can begin to explore some of the parts of the application and see how they work together. The next steps are meant to expose us to different aspects of the software, but rest assured that we will cover these concepts and techniques in more depth in future sections.

## Modify Hello
In the default application, there are two Components at play: `App` and `Hello`. In order to experiment with the application, we will modify the `Hello` component. Open the file `src/components/Hello.vue` and look at the parts. Each `.vue` file is broken into three main areas: The template, the scripts, and the styles. These are denoted by corresponding tags.

### The Template
Let's modify the template code to reflect our own content. Here is the original template code from `src/components/Hello.vue`:

```html
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <ul>
      <li><a href="https://vuejs.org" target="_blank">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank">Forum</a></li>
      <li><a href="https://chat.vuejs.org" target="_blank">Community Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank">Twitter</a></li>
      <br>
      <li><a href="http://vuejs-templates.github.io/webpack/" target="_blank">Docs for This Template</a></li>
    </ul>
    <h2>Ecosystem</h2>
    <ul>
      <li><a href="http://router.vuejs.org/" target="_blank">vue-router</a></li>
      <li><a href="http://vuex.vuejs.org/" target="_blank">vuex</a></li>
      <li><a href="http://vue-loader.vuejs.org/" target="_blank">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank">awesome-vue</a></li>
    </ul>
  </div>
</template>
```

We can see from the page in the browser that this code is creating most of the content on the page. Let's alter that content:

```html
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>2 Things that are difficult in JavaScript</h2>
    <ol>
      <li>naming things</li>
      <li>recursion</li>
      <li>off-by-one errors</li>
    </ol>
  </div>
</template>
```

These changes result in the following changes in the browser:

![After changes to template](/img/project-bootstrap2.png)
<br>After changes to the template

Vue.js component templates can have any HTML in them. We can create whatever structures we need, and they can even include other component tags (as with the `src/App.vue` file, which uses the `Hello` component in its template). Any HTML that shows up between the `<template>` tags will be inserted into the app when this component is executed.

### The Styles
Inside each Vue.js component is also a style block, defined by the `<style>` tags. We can see in the screenshot above that the list items are not numbered and they are laid out horizontally. Let's replace the numbers and make them go vertical again. 

Here is the original code:

```
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
```
The `scoped` attribute on the `<style>` tag insures that these styles will not apply to anything outside of the component itself. This is very handy on large projects where overlapping styles can be problematic. Because of this tight scoping, we can approach each component on its own terms, name the parts of the component in a way that makes sense, and generally pursue a more modular approach to styles.

In order to change the list the way we want, let's make these changes:

```
<style scoped>
h1, h2 {
  font-weight: normal;
}

ol {
  list-style-type: decimal;
  width: 40%;
  margin: auto;
}

li {
  display: list-item;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
```

There is nothing special about these styles, but it's interesting to note that if we inspect our styles in our developer tools, we can see how the styles are scoped to the specific component:

![Scoped styles in developer tools](/img/project-bootstrap3-scoped-styles.png)
<br>Viewing the scoped styles in developer tools

By using the attribute selector these style definitions are sure to never apply to any other elements on the page. So if we write a style for `p` or `div` or `ul` it will only apply to those elements when they show up inside this specific component template.

### The Logic
The last part of the component that we have to explore is the logic itself. For the most part, this logic is pretty simple when it is generated in the project skeleton. The script tags in the default `Hello` component contain the following code:

```
<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>
```

This logic does not do too much except define the `data` function with an object that contains the `msg` property. The `data` object is what gets revealed to the template for processing. Any property of the `data` object is accessible as a variable inside the template. The `msg` property is used in the `Hello` component template to create the content of the `<h1>` tag:

```
<h1>{{ msg }}</h1>
```

We can change the message of that tag by altering the definition of the `msg` property in the script:

```
<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'This Data Has Been Altered'
    }
  }
}
</script>
```









