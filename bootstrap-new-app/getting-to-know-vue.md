# Getting to Know Vue

Vue.js is an application framework primarily based on the concept of [Web Components](https://www.webcomponents.org/introduction). It is designed to be approachable for newer developers, but it allows for extension to become as feature rich as any other application framework out there. This approach is mirrored at many levels within the Vue.js project: The system itself is meant to be lean and then augmented by adding additional modules. And the projects we build with Vue.js are meant to be composed of simple components that combine to create more complex applications.

![Vue.js system illustration](https://vuejs.org/images/components.png)
<br>Vue.js system illustration

As we can see in the illustration above, everything we see in the interface of our application is related to a specific Component within our application code. A "Web Component" is a self-contained set of HTML, CSS, and JS functionality that is revealed through a unique, custom HTML tag. In the illustration, we can see the wireframe representing components on the page. Those components are related within the logic of the Vue.js application, too, which is what is shown in the hierarchical diagram to the right.

![Lego Simpsons Minifigs Parts](/img/lego-minifigs-assorted.jpg)
<br>Lego Simpsons Minifigs Parts (All rights belong to owner.)

This is probably the correct place to bring up a metaphor based on a favorite modular toy. If we imagine that a framework is like a box of Legos, for example, then each block type would be a Component. We could build a Lego person by combining a head block, body block, and legs block. With Legos we even have modular hair blocks that we can customize to get the character we want. 

Our Vue.js applications are sets of special blocks that we can put together to create the unique experience we need. We can create our own Components, or we can use Components created by others. Just like with the Lego figures, we can achieve a vast array of different effects by varying the elements that build our entire application.

It can be tricky to really understand how components in Vue.js applications work together. So let's take a closer look at the code we just generated in the project skeleton.

## Project Components

Inside the `src/` directory of our project is where all of the code that makes our project unique lives. If we look inside, we see the following:

```bash
drwxr-xr-x   6 shawnr  staff   204B Sep 24 13:09 .
drwxr-xr-x  15 shawnr  staff   510B Sep 24 15:11 ..
-rw-r--r--   1 shawnr  staff   446B Sep 24 13:09 App.vue
drwxr-xr-x   3 shawnr  staff   102B Sep 24 13:09 assets
drwxr-xr-x   3 shawnr  staff   102B Sep 24 13:09 components
-rw-r--r--   1 shawnr  staff   320B Sep 24 13:09 main.js
```
Looking at this listing, we can see a `main.js` file and an `App.vue` file. The other two items listed are directories: `assets` and `components`. Inside `main.js` is the code that instantiates a Vue.js application. It imports the `App.vue` file, as well as the core Vue.js framework. The result of this code is that the `App` component is inserted into the `index.html` file (in the root of our project repository) and then executed.

When the `App` component is executed, it runs the code contained in `App.vue`. This code defines a `<template>` tag, a `<script>` tag, and a `<style>` tag. When working with Vue.js components, we keep our HTML, JavaScript, and CSS in one location. Our CSS is automatically scoped so it will only affect the specific component, which helps prevent issues of CSS overlapping between components. The logic that makes the component function is included between the `<script>` tags, and that logic is applied to the template defined in the `<template>` tag.

![Code for App and Hello Components](/img/vue-app-component-code.png)
<br>Code for App and Hello Components

Inside the `components/` directory is the `hello.vue` file, which contains the `Hello` component. This component is referenced inside of the `App` component. As we can see in the illustration above, the `App` components lists the child components it's using in the `components` property of the `App` object. `Hello` is the only component listed. We can also see that in `App.vue` there is an import statement:

```js
import Hello from './components/Hello'
```

The import statement is how we can let modern JavaScript files know about other files we are working with. Notice that this import statement gives a name to the object being imported (`Hello`), and it specifies the file that is to be imported (`./components/Hello`). The `.vue` extension on the file name is not needed in the import statement, although it is needed on the file itself. The import statement understands to fill in the extension.

We can see, based on the highlights in the image above, that the `Hello` component is referenced in the template for the `App` component. The `<hello></hello>` line indicates where the content for the `Hello` component should be shown. It can be difficult to imagine what this looks like when it is displayed to the user. This next screenshot should help.

![Vue.js App Components](/img/vue-app-component-web2.png)
<br>Vue.js App Components

The image above shows the default page rendered when running the project skeleton. The green area represents the part of the page taken over by the `App` component. The `Hello` component is inserted inside of the `App` component. The blue area represents the part of the page that is generated and controlled by the `Hello` component.

## Templates and Data (and Methods)

In each Vue.js Component, we will probably provide some HTML for a template. Within templates we can invoke different kinds of logic from within the script controller of the template and we can output data values to display to the user. There is a lot of power within templates, and we will explore the power of templates in greater detail soon. For now, here are a few things to keep in mind as you're looking at and playing with this new project skeleton.

### Output Data Values

In a Vue.js template, we can output data values using the "double curly brace" syntax. This is often called "mustache" templates (because curly braces look like sideways mustaches). Here is an example from the `Hello.vue` file:

```
<h1>{{ msg }}</h1>
```

This example will output the value of the `msg` property defined in the `data` function. Most components will define some properties in their `data` function. Managing data and binding data properly to template elements is key to using templates effectively.

### Directives

In addition to just displaying data, templates can contain some logic. This logic is made available through the concept of "directives". Directives in Vue.js look like HTML attributes. They are written in the same style as HTML attributes in HTML tags. Here is an example:

```
<ol>
  <li v-for="todo in todos">
    {{ todo.text }}
  </li>
</ol>
```

We can see that the `v-for` directive is being used to create a loop. The loop will duplicate the list item for each `todo` in the `todos` Array. (Don't worry if this seems confusing now. We will look more closely at using loops and other directives in an upcoming section of the book.)

Another important directive is `v-if`, which allows us to write a conditional statement like this:

```
<div v-if="showResults">
  ... show some information ...
</div>
```

In addition to directives that allow looping and conditionals within a template, there are also directives that allow us to respond to events. The `v-on` directive allows us to specify an event and the "method" (function) that will be invoked when the event occurs. Here is an example:

```
<button v-on:click="refreshData">Refresh Results</button>
```

In the example above, we have a button that will execute the `refreshData` method defined in our component whenever the button is clicked. (Again, this is a lot to understand without additional information, but the goal here is just to begin recognizing what these parts do. We will learn more about them soon.)

Using all of these core template features, plus some of the other features provided by the Vue.js framework, we have the ability to create dynamic interfaces and useful functionality that our users will appreciate.



