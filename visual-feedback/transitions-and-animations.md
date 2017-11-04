# Transitions and Animations
When data changes on the screen, we often use transitions and animations to call the user's attention to what has just been added or removed. The movement we use often mimics the change that we are trying to illustrate. For example, a user might delete an item from a list, which might slide out and fade away. Or a refresh of data might cause items to enter a list, sliding in from the side and landing with a bounce.

This movement makes our interfaces feel more lively and helps conceptually ground the action the user has taken. The addition of movement makes our software feel more real. Fortunately, Vue.js gives us a few powerful tools for animating transitions within our applications.

## Enter/Leave/List Transitions
Whenever content enters or leaves the screen, or whenever information is added or removed from a list, Vue.js will automatically add some specific classes to the HTML elements. These classes can be defined by developers to trigger whatever animation or transition we wish.

Here is the full list of transition classes provided by Vue.js.

Class Name | When Applied | When Removed | Definition
-----------|--------------|--------------|-----------
`.v-enter` | Before the element is inserted. | One frame after the element is inserted. | Starting state for enter.
`.v-enter-active` | During entire enter phase. | When transition finishes. | Active state for enter.
`.v-enter-to` | One frame after element is inserted (when `.v-enter` is removed). | When transition finishes. | Ending state for enter.
`.v-leave` | Immediately when leaving animation is triggered. | One frame after leaving animation is triggered. | Starting state for leave.
`.v-leave-active` | During entire leave phase. | When transition finishes. | Active state for leave.
`.v-leave-to` | One frame after leaving animation is triggered. | When transition finishes. | Ending state for leave.
~~~~~~~~~~~~~~~|~~~~~~|~~~~~~|~~~~~~

These are the default names of the classes that are applied as content is added to or removed from the display. It is possible when defining a transition to provide a unique prefix for these classes that will replace the `v-` part of the name. For example, if we named a transition `foo`, then we would write the styles `.foo-enter` and `.foo-leave` instead of `.v-enter` and `.v-leave`. 

By defining different styles for each of these points, and setting up CSS transitions between these styles (or using CSS animations to provide more complex animations), we can create fade in and out effects. But in order to apply these styles, we must wrap content in our templates in a `<transition>` component in order to let Vue.js know we want to use these styles when elements are added and removed from the display.

## Transitioning Single Elements
To transition a single element, we can use the `<transition>` component, which is provided by the Vue.js framework and can be used without importing it or adding it to our project. The `<transition>` component accepts a `name` attribute, and it should wrap a single HTML element. The `name` attribute will cause that name to be prepended to the transition class names applied by Vue.js. Transitions can be applied to any element that is controlled with a `v-show`, `v-if`, or any dynamic components or component root nodes. So we can always animate the display or removal of an entire component, but this is not the component that handles transitions for other elements (such as list items). (We will explore that other component shortly.)

As an example, we can look at how we might animate the display of the FAQ answers from our old FAQ example. The FAQ display uses a `Question` component that handles the showing/hiding of the answer text. We can wrap the answer in a transition and make the display of that information more eye-catching:

```html
<template>
  <div class="question">
    <h2><a v-on:click="toggleAnswer">{{ question }}</a></h2>
    <transition name="fade">
      <p v-show="showAnswer" class="answer">{{ answer }}</p>
    </transition>
  </div>
</template>

<script>
export default {
  name: 'FAQ',
  data () {
    return {
      showAnswer: false
    }
  },
  props: [
    'question',
    'answer'
  ],
  methods: {
    toggleAnswer: function () {
      this.showAnswer = !this.showAnswer;
    }
  }
}
</script>

<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s
}
.fade-enter, .fade-leave-to {
  opacity: 0
}
h1, h2 {
  font-weight: normal;
}
a {
  color: #42b983;
  cursor: pointer;
}
</style>
```
We can see that the `p.answer` element has been wrapped in a `<transition>` component with the name `fade`. This corresponds to the styles that have been defined: `.fade-enter-active`, `.fade-leave-active`, `.fade-enter`, and `.fade-leave-to`. Note that it is not required to define styles for every single class used in the transition. Using different classes will lead to different results, and the possibilities are incredibly diverse. We could just as easily be using other CSS animations to do fly-ins, bounce-outs, or whatever other effect we feel best serves our users.

![FAQ Example Fades](/img/faq-fades.gif)
<br>FAQ Example Fades

This single element transition is commonly found, but it is also common for us to want to animate items being added to or removed from other elements (or multiple elements together). In these cases, we must use the `<transition-group>` component.

## Transitioning Groups of Elements
In order to transition groups of elements (list items or other things generated using a `v-for` directive), we can use the `<transition-group>` component. This component functions in a way similar to the single `<transition>` component. It also takes a name attribute to modify the names of the classes that are automatically added to the elements as they transition. We can also use the other attributes that are available on the `<transition>` element (such as the `appear` attribute, which makes an animation take place when the content appears on the page without being toggled by the user). 

In order to use the `<transition-group>` component, we must label each item we want to transition with a key, which we can do by binding a unique value to the key as we process a `v-for` loop. We must also specify a tag that the transition will wrap around the group of elements included in the effect. The `<transition>` component defaults to using a `<span>` tag to wrap the elements. But we can modify that easily. Here is an example of how we add animations to list items using the `Forecast` screen from the previous project.

**template**
```html
<transition-group name="fade" tag="div" appear>
  <li v-for="forecast in weatherData.list" v-bind:key="forecast">
    <h3>{{ forecast.dt|formatDate }}</h3>
    <weather-summary v-bind:weatherData="forecast.weather"></weather-summary>
    <weather-data v-bind:weatherData="forecast.main"></weather-data>
  </li>
</transition-group>
```

**styles**
```css
.fade-enter-active, .fade-leave-active {
  transition: opacity 1s
}
.fade-enter, .fade-leave-to {
  opacity: 0
}
```
We can see that we have specified a `<div>` element to wrap all of our list items. We have not modified our list output at all except for the addition of the `key` attribute on the `<li>` tag. We have bound the `forecast` value to the key, which gives us the unique identifier the transition group needs to operate. In the styles block, we have defined the same fade effects we used on the previous example. We could have defined any other transition effect if we preferred. We have also used the `appear` attribute on the `<transition-group>` component so the list items will be animated the first time they appear on the screen (without any change from the user).

![Forecast Fade-In](/img/forecast-fade.gif)
<br>Forecast Fade-In

This effect creates a nice visual cue that information has been updated. In other situations, we could add effects to make it more obvious when data is removed from a list or added to the list. We can even explore more of the features of transition groups to animate the re-ordering of a list, which is a valuable effect in some situations.

## Pushing Further

Although we have learned enough in this section to dramatically improve our interface, it is possible to do more with transitions than we have explored here. If we're feeling like a challenge, or more exploration, it's worthwhile to dig into the [Vue.js Guide](https://vuejs.org/v2/guide) and learn about [list move transitions](https://vuejs.org/v2/guide/transitions.html#List-Move-Transitions) and [reusable transitions](https://vuejs.org/v2/guide/transitions.html#Reusable-Transitions) among other fascinating details.

In addition to the built-in features of Vue.js, it is worthwhile to explore some of the other third-party modules that have been created to provide some great animation and transition experiences. [The Animation section on the Awesome Vue list](https://github.com/vuejs/awesome-vue#animation) is a great place to start. [The `vue2-animate` package](https://github.com/asika32764/vue2-animate) will be used in the project that goes with this section.

