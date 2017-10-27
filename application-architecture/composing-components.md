# Composing Components
Vue.js is organized around the [Web Components Standard](https://www.w3.org/standards/techs/components#w3c_all), which is an idea that has gained momentum over the past few years. The idea of web components has been popularized primarily by another single page application framework, React. React and Vue.js share a many common approaches and concepts, most of which stem from their mutual interest in web components.

[The idea of web components](https://developer.mozilla.org/en-US/docs/Web/Web_Components) is straightforward and powerful: Allow developers to create reusable, custom HTML elements that handle whatever tasks are needed in an application or site. By creating small, specific components, we can use several components together to achieve a more complex interface or experience. In the jargon of Vue.js, this process of combining components to build our interfaces is known as "composing components." 

[In Vue.js we write components](https://vuejs.org/v2/guide/components.html) that handle specific parts of our application. Most of these components should be small and dedicated completely to their role in the application: A "favorite" button, a search result, or the content of an article. Other components might handle larger pieces of the application, such as a component to control an entire "About Us" view, or a component that would build up a gallery of images or video.

Those larger components will most likely reference smaller components within their templates. This allows us to create more complex interfaces, but we can still keep our individual components as lean as possible. In each component, we want to keep our template, logic, and stylesheet as small as possible. Fewer lines makes our files more readable, more easily and immediately understandable, and eliminates many opportunities for error.

The process of determining how we should organize our applications is similar to the methods for refactoring that we discussed earlier: We want to create a solid separation of concerns, and that can be achieved by encapsulating functionality into specific components. We can also use our choices about what components we create to provide a more friendly interface for developers of our application. 

Because all of this can be difficult to imagine in the abstract, let's explore some concrete examples of how we use components together within a Vue.js project.

## Using Child Components in Templates
In any given component template, we can reference "child" components. These child components are revealed to the template as a custom HTML element, and they are defined in the `components` property. Borrowing inspiration from [the Vue.js documentation about Components](https://vuejs.org/v2/guide/components.html#Local-Registration), here is an example of how we could implement a simple `<counter>` element as a child component:

**The `Home.vue` file**
```html
<template>
  <div class="home">
    <h1>Child Components Demo</h1>
    <counter></counter> | <counter></counter> | <counter></counter>
  </div>
</template>

<script>
import Counter from '@/components/Counter';

export default {
  name: 'Home',
  data () {
    return {

    }
  },
  components: {
    counter: Counter
  }
}
</script>
```

**The `Counter.vue` file**
```html
<template>
  <button class="fave" v-on:click="incrementCounter">
    {{ counter }}
  </button>
</template>

<script>
export default {
  name: 'favorite',
  data () {
    return {
      counter: 0
    }
  },
  methods: {
    incrementCounter: function () {
      this.counter++;
    }
  }
}
</script>
```

We can see that in these two files we have two components. The `Counter.vue` file defines a component with a very simple template: It is just a `<button>`. It uses a single data value (`counter`), and it has an event listener defined to increment the counter on each click using the `incrementCounter` method. This component could be used on its own at a specific URL route, but it would not be a very interesting view. Instead, we have defined this component with the intention of using it in another component.

In the `Home.vue` file, we can see that there is a new property in the component logic called `components`. We can also see that the `Counter` component has been imported at the beginning of the logic. It is required to import each child component before using it in our component logic. The `components` property is an object, and each property of the `components` object defines a relationship between a child component and the name that will be used for the custom HTML element in the component template.

In the template of the `Home` component, we can see that we have the child component tag (`<counter></counter>`) used three times. Each of these uses will result in a button that we can click to increment the number it displays. When we view the `Home` component in the web browser, we can click the buttons and see a result that looks like this:

![Counter Buttons](/img/child_component1.gif)
<br>Counter Buttons

As we can see in the image above, when we click each button it keeps its own tally using its own counter. Although these buttons are each a _copy_ of the `Counter` component, they are individual instances. The ability to isolate functionality and data into a child component can be useful in itself, but it's often necessary to pass some information to the child component in order to do something with it.

## Setting Properties on Child Components

## Using Events and Listeners

## Syncing Properties








