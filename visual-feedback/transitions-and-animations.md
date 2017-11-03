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
wwwwwwwwwwwwwww|wwwww|wwww|wwww

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

<!-- Add "scoped" attribute to limit CSS to this component only -->
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
We can see that the `p.answer` element has been wrapped in a `<transition>` component with the name `fade`. This corresponds to the styles that have been defined: `.fade-enter-active`, `.fade-leave-active`, `.fade-enter`, and `.fade-leave-to`.


## Transitioning Groups of Elements

## Reusable Transitions



