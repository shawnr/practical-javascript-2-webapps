# Messaging
Clear messaging is a great technique for informing the user about what is happening in our software at any given point in time. As discussed earlier, using either global or local messages on a page can really improve the user experience and help the user succeed at accomplishing their goals. The ways we implement messages can vary widely, but they don't need to be terribly complex. There are many ways to solve the messaging problem in Vue.js, and plenty of third-party tools we can rely on to help us handle messages.

## Loading Throbbers
We can create a simple loading throbber component for use whenever we need to load data from a third-party API. The component can be used like any other child component within a template, and easily turned "on" and "off" using a boolean value in our component logic. Here is what a load throbber component might look like:

```html
<template>
    <div v-if="showThrobber" class="spinner"></div>
</template>

<script>
export default {
  name: 'LoadThrobber',
  data () {
    return {

    }
  },
  props: {
    showThrobber: true
  }
}
</script>

<style scoped>
.spinner {
  width: 40px;
  height: 40px;
  background-color: #333;

  margin: 100px auto;
  -webkit-animation: sk-rotateplane 1.2s infinite ease-in-out;
  animation: sk-rotateplane 1.2s infinite ease-in-out;
}

@-webkit-keyframes sk-rotateplane {
  0% { -webkit-transform: perspective(120px) }
  50% { -webkit-transform: perspective(120px) rotateY(180deg) }
  100% { -webkit-transform: perspective(120px) rotateY(180deg)  rotateX(180deg) }
}

@keyframes sk-rotateplane {
  0% {
    transform: perspective(120px) rotateX(0deg) rotateY(0deg);
    -webkit-transform: perspective(120px) rotateX(0deg) rotateY(0deg)
  } 50% {
    transform: perspective(120px) rotateX(-180.1deg) rotateY(0deg);
    -webkit-transform: perspective(120px) rotateX(-180.1deg) rotateY(0deg)
  } 100% {
    transform: perspective(120px) rotateX(-180deg) rotateY(-179.9deg);
    -webkit-transform: perspective(120px) rotateX(-180deg) rotateY(-179.9deg);
  }
}
</style>
```
Notice that this component is very simple: Merely a single `div` element with a class applied to it. It uses a boolean value to show/hide itself. The load throbber (or "spinner" as it's labeled in the CSS) was borrowed from [the SpinKit set](http://tobiasahlin.com/spinkit/), which is a great resource. There are many ways to make an animated load throbber, including using animated GIFs, SVGs, or pure CSS animations. 

## Global Messages
Global messages can also be handled nicely with child components. Message styles can be contained in the dedicated component, and that component can be used by any other components that need to produce global messages. Messages can be styled to show like "toast" displays (popping up from the bottom or out from another side of the viewport), or they can simply fade in or overlay on the page content.

## Local Messages








