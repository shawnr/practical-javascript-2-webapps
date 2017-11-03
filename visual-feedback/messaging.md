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

As with so many aspects of web development, if we would prefer to use a solution created by somebody else, we can leverage one of the [many projects listed on the Awesome Vue list under Loaders](https://github.com/vuejs/awesome-vue#loader).

## Global Messages
Global messages can also be handled nicely with child components. Message styles can be contained in the dedicated component, and that component can be used by any other components that need to produce global messages. Messages can be styled to show like "toast" displays (popping up from the bottom or out from another side of the viewport), or they can simply fade in or overlay on the page content.

Here is an example of a simple message list component that could be used in multiple locations throughout an application:

```html
<template>
    <ul v-if="messages.length > 0" class="message-container">
      <li v-bind:class="message.type" v-for="message in messages">
        <h2>{{ message.title }}</h2>
        <p>{{ message.content }}</p>
      </li>
    </ul>
</template>

<script>
export default {
  name: 'Messages',
  data () {
    return {

    }
  },
  props: {
    messages: []
  }
}
</script>

<style scoped>
.message-container li {
  padding: 10px;
  margin: 5px;
  font-size: 1rem;
}
.error {
  color: red;
  background: pink;
}
.info {
  color: black;
  background: #e8e8e8;
}
.success {
  color: white;
  background: green;
}
.warning {
  color: black;
  background: yellow;
}
h2 {
  font-size: 1rem;
}
</style>
```

We can see that we have a simple template defined to output messages. The message `type` is used to determine the styles that should be applied to the message. Each message consists of a `title` and `content`. These are common attributes for generic messages. We could easily maintain an array of messages that should be displayed. We could even break this down further and enhance this component with child components of its own that would allow us to close a message when the user clicks an icon or provide a timeout on messages so they fade away after some period.

Of course, there is really no reason to build our own messaging system other than the fact that we can learn more and control more by doing it that way. [The Awesome Vue list has several Notifications modules](https://github.com/vuejs/awesome-vue#notification) we can leverage to easily add robust messages and notifications to our applications.

## Local Messages

Local messages can be inserted into templates and controlled via `v-if` directives to provide whatever other messaging or information we need. These methods of controlling the display of content in a very localized fashion have already been covered in previous sections of this book. Those same methods will work for very many local message use cases.

Where our previously-covered methods may not work as well is when we are validating form data. We have previously looked at providing feedback in terms of form validation, and we can always write our own validation logic. But it is also possible to, once again, leverage the efforts of the community. We can bring in [any number of form validation packages for Vue.js](https://github.com/vuejs/awesome-vue#validation) and use those.

Another use case for very localized messaging is in the "tooltip", which is a message usually tied to a specific HTML element. We often see tooltips when we hover over elements on the screen. They are also used to explain details about form fields and other interface elements. And, once again, there are [numerous packages that provide tooltip features for Vue.js projects](https://github.com/vuejs/awesome-vue#tooltip).

Although Vue.js gives us the tools to easily create these features for ourselves, we still can benefit from using existing packages to help us move along and focus on more unique aspects of our projects. Each of the packages suggested on the Awesome Vue list works in a slightly different way, and each one might be better or worse for your purposes. Be sure to browse around and get an idea of how these different packages work, but the only way to know for sure is to dive in and try some of them out. If we don't find what we need, we can always build it ourselves.








