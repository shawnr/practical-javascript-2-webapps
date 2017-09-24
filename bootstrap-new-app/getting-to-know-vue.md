# Getting to Know Vue

Vue.js is an application framework primarily based on the concept of [Web Components](https://www.webcomponents.org/introduction). It is designed to be approachable for newer developers, but it allows for extension to become as feature rich as any other application framework out there. This approach is mirrored at many levels within the Vue.js project: The system itself is meant to be lean and then augmented by adding additional modules. And the projects we build with Vue.js are meant to be composed of simple components that combine to create more complex applications.

![Vue.js system illustration](https://vuejs.org/images/components.png)
<br>Vue.js system illustration

As we can see in the illustration above, everything we see in the interface of our application is related to a specific Component within our application code. A "Web Component" is a self-contained set of HTML, CSS, and JS functionality that is revealed through a unique, custom HTML tag. In the illustration, we can see the wireframe representing components on the page. Those components are related within the logic of the Vue.js application, too, which is what is shown in the hierarchical diagram to the right.

![Lego Simpsons Minifigs Parts](/img/lego-minifigs-assorted.jpg)
<br>Lego Simpsons Minifigs Parts (All rights belong to owner.)

This is probably the correct place to bring up a metaphor based on a favorite modular toy. If we imagine that a framework is like a box of Legos, for example, then each block type would be a Component. We could build a Lego person by combining a head block, body block, and legs block. With Legos we even have modular hair blocks that we can customize to get the character we want. 

Our Vue.js applications are sets of special blocks that we create (or which others have created and we simply make use of). We put them together to create the unique experience we want.

It can be tricky to really understand how components in Vue.js applications work together. So let's take a closer look at the code we just generated in the project skeleton.

## Touring the Project

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

When the `App` component is executed, it runs the code contained in `App.vue`. This code defines a `<template>` tag, a `<script>` tag, and a `<style>` tag. When working with Vue.js components, we keep our HTML, JavaScript, and CSS in one location. Our CSS is automatically scoped so it will only affect the specific component, which helps prevent issues of CSS overlapping between components. The logic that makes the component function












