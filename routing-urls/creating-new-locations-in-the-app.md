# Creating New Locations in the Application
Creating new locations in a Vue.js app is as simple as adding a new route definition. However, we also will usually want to create a new component to handle the unique content that should be displayed at the new location. This is not terribly difficult to accomplish, but it can be made easier if we have some handy reference material.

In this section we will look at the basic steps involved in creating a new component and route within our Vue.js application. (There are plenty of reasons to create new components that don't necessarily map to a specific route in the application. The first part of these directions should generally work for that, too.)

## Defining a New Component
The first step in creating a new component is to create a new `.vue` component in the `src/components/` directory. All of our components follow the same pattern, so we can use a little snippet of code as a way to bootstrap the new components. 

Here is a basic Vue component skeleton. There is no logic here, and it is meant to be edited to perform the specific function we need. But this provides us with a basic template to fill up with our custom stuff.

```html
<template>
  <div class="component">
    <h2>{{ message }}</h2>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        message: 'This component works.'
      }
    }
  }
</script>

<style scoped>
  .component {
    background: #e8e8e8;
    min-height: 400px;
  }
</style>
```

To get a new component going, we can simply copy the blank template above into a file and save it into the `src/components/` directory in our project. It is important to maintain our naming pattern and give the file a `.vue` extension so it can be properly understood by our build system and framework.

Once we have bootstrapped the basic component (even in this primitive form), we can define the route that will serve our new component.

<div class="tip-box">
    <h3>Code Snippets</h3>
    <p>Many code editors allow developers to create "snippets" of code that can be re-used in different places. Developers love to create and save small chunks of code that can help them get started quicker on building a new component, or to help them stick with a proven pattern or method. Saving snippets of code can be a huge timesaver when writing complex software, especially when we work with the same frameworks and libraries over and over again.</p>
    <p>Most code editors will support a "snippets" feature. It's worthwhile to explore the features of our chosen text editors and see how they handle snippets of code. If the editor doesn't support storing random small code snippets, we can build up a set of files in a snippets directory and manage our boilerplate code that way. However we choose to manage this information, storing and accessing these quick snippets is a great way to work.</p>
</div>

## Setting up the New Route