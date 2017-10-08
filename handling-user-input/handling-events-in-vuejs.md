# Handling Events in Vue.js
Events are a key part of any web-based application. The user interacts with a page by scrolling, clicking, hovering, touching, dragging, submitting forms, and more. All of these interactions can be captured. Responding to these events is a primary method we have for building reactive interfaces that help the user accomplish their goals.

As a quick recap about what events are: Many components of HTML will emit (signal, or "fire") ["events."](https://developer.mozilla.org/en-US/docs/Web/Events) Events are meant to provide a signal that something interesting has happened, and much of what we do in our coding is to create situations where responding to these built-in events becomes useful to the user. For example, when a button is clicked, a "click" event is fired. This event can be detected in our code and we can respond by doing something the user expects.

Events are "handled" by event listeners (which we will often just call "listeners"). Listeners are specific watchers we have defined to detect an event and then execute some code in response to the event. Events are happening all the time when a user interacts with a website, but if no listeners have been defined then only the default event "handlers" will be invoked. 

For example, a web browser will automatically submit a form when the form emits the `submit` event. A form could be submitted by a user pressing `enter` on their keyboard, or by clicking a button to submit the form. Regardless, the browser has a default event listener watching for that signal from any HTML forms, and it will execute code to respond to an event. 

As developers, we can also detect events and we can choose to augment or replace the default response to any event. Vue.js provides us with a range of tools for [working with events](https://vuejs.org/v2/guide/events.html). These tools make it much easier to define, manage, and execute event handling in Vue.js projects.

## Defining Event Listeners
The core directive used to define event listeners is the `v-on` directive. This directive takes an argument, which is the name of the event for which to listen. Because each HTML element can emit a different set of events, it's best to refer to a list of relevant events (such as the [Web Events page at MDN](https://developer.mozilla.org/en-US/docs/Web/Events)) to know we are using the proper event label. But much of the time we use relatively standard events in our projects (e.g. `submit`, `click`, `keydown`, `keyup`, etc.). 

Here is an example of a simple `v-on:click` listener that increments the value of a `counter` variable in the template context:

```html
<h2>Counter</h2>
<button v-on:click="counter++">Add 1</button> {{ counter }}
```

All of the logic that responds to this event is in the template here. As long as `counter` is initialized to `0` in the component's data, no other logic is required in the component to make this work. When the template loaded in a browser, it looks like this:

![Simple click event handler](/img/event-handler-click-counter.gif)
<br>Simple click event handler

This is easy enough to set up, but usually we want to do something more with our event handlers. Typically, rather than executing a simple line of code when an event is detected, we execute a component method to handle the event. Component methods can be used in many ways, and they are straightforward to add to our components.

## Component Methods
Component methods are functions that can be executed in various ways within a Vue.js component. Much of the time, these methods will be executed in response to some event that has been triggered in the system. The `v-on` directive can define a method call that will be executed in response to an event signal. Let's look at an example:

```html
<template>
  <div class="events">
    <h2>Message: {{ message }}</h2>
    <p><button v-on:click="setMessage('Danger! Danger!')">Show Danger Message.</button></p>
    <p><button v-on:click="setMessage('All Clear!')">Show All Clear Message.</button></p>
  </div>
</template>

<script>
export default {
  name: 'EventDemos',
  data () {
    return {
      message: 'Component loaded successfully.'
    }
  },
  methods: {
    setMessage: function (text) {
      this.message = text
    }
  }
}
</script>
```
In this example, there is only one variable revealed to the template: `message`. The message is initialized to a load statement, but the user can click a button to change the message. Each button has a `click` event listener defined using the `v-on` directive. When the `click` event is detected on one of the buttons it will execute the `setMessage` method. This method is a function that expects to receive some text to change the value of the `message` variable. In this example, the text is set by hand, but this text could also be provided by referencing another variable or data point.

Here is what this code looks like when displayed to the user:

![Event handler using component method](/img/event-handler-method1.gif)
<br>Event handler using component method

We can see that when the user clicks the buttons the message is changed instantly. This demonstrates the fundamental ability to use methods to respond to events. With this tool, we can make all sorts of things happen in our interfaces.

## Preventing Default Event Handling
Although we can now respond to events, there are situations when we will find ourselves fighting against the default event handling provided by the web browser. Vue.js provides us with several modifiers we can use alongside the `v-on` directive to prevent the default actions from taking place. We should keep the following modifiers in mind as we work through trickier event handling situations.

### `.prevent`
The `.prevent` modifier will prevent the default event handlers from executing when an event is triggered. This is most commonly used to prevent form submissions. If no `action` property is supplied on a `<form>` element, the browser will still refresh the page. That refresh could be enough to really interrupt our well-planned user experience. Luckily, it's easy to prevent the default form submit event from happening thanks to `.prevent`.

```html
<template>
  <div class="forms">
    <h2>Message: {{ message }}</h2>
    <form v-on:submit.prevent="handleMyForm">
      <p><label>New Message: <input v-model="newMessage" type="text"></label></p>
      <p><input type="submit"></p>
    </form>

  </div>
</template>

<script>
export default {
  name: 'FormsPractice',
  data () {
    return {
      message: 'Submit the form to change this text.',
      newMessage: ''
    }
  },
  methods: {
    handleMyForm: function () {
      this.message = this.newMessage
    }
  }
}
</script>
```
Rather than directly binding the `message` value to the form input, this example uses a component method to handle the form submission. The method is called `handleMyForm` and it changes the value of the `message` variable. Note the use of `.prevent` on the `<form>` element's event listener: This is used to prevent the browser from refreshing to submit the form. 

Here is what this example looks like to the user:

![Using .prevent on a form](/img/event-handler-prevent.gif)
<br>Using .prevent on a form

### `.stop`
In some situations there could be multiple event handlers that could be triggered when we perform a single action. It's common for HTML elements and their parent or child elements to each have events defined, and in those cases the event "bubbles" up the DOM from child to parent to grandparent and beyond. This could lead to multiple event handlers being executed in quick succession when a single event is triggered.

In order to stop the bubbling of events through the DOM, JavaScript has a `stopPropagation` method that we use. In Vue.js, we can simply apply the `.stop` modifier to a `v-on` directive. This will stop the bubbling of the event through the DOM and prevent any other event handlers from firing. Here is an example of how this looks:

```html
<a v-on:click.stop="handleMyClick">Click me</a>
```

**Note:** This is different from `.prevent`, which only prevents the _default_ event handlers from firing. The `.stop` modifier will stop all other events handlers from being executed. It is sometimes desirable to both stop the event from propagating through the DOM and to prevent the default event handlers from executing. Luckily, directive modifiers can be chained in Vue.js:

```html
<a v-on:click.stop.prevent="handleMyClick">Click me</a>
```

It's important to keep in mind that chained modifiers are possible with any modifier, and that they are executed in the order they are chained. The order of chaining modifiers can dramatically alter their effect, so we must pay close attention to our ordering of modifiers.

### `.once`
It is possible that we have an event we only wish to trigger once. For example, submitting a payment form should only be done once, but it's common for users to double-click the submit button or click submit a second time after they wait for a moment. We might use the `.once` modifier to prevent that behavior:

```html
<form v-on:submit.prevent.once="handleMyForm">
```

We can see that we can also chain the `.once` modifier with the `.prevent` modifier to fully handle the form with our custom component method.

There are additional modifiers available, but these are the most commonly used. Refer to [the Vue.js Events Guide](https://vuejs.org/v2/guide/events.html) for more details about modifiers.

## Detecting Keyboard Input
Keyboard events are helpful for building an interface that is both efficient for users prefer keyboard navigation and accessible to users who are forced to use keyboard navigation. Adding hotkeys, keyboard shortcuts, and general navigational support via keyboard can be a great enhancement to any user experience. Detecting keyboard and device events is straightforward with Vue.js.

The [events associated with keyboards](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent) are: 
* `keydown` &mdash; When the key is first pressed down by the user.
* `keypress` &mdash; If the key is not a modifier (`alt`, `opt`, `ctrl`, `cmd`, etc.), this event is fired.
* `keyup` &mdash; When the key is released by the user.

Users are accustomed to these events being used in different ways. The `keydown` event is somewhat "instrumental": We expect to hear a sound when we press the key down on the piano, for example. This is also how we expect game controls to work much of the time. The `keypress` event is often used to filter out modifier keys, which is helpful for page shortcuts, and this is the way we expect keyboard combinations to work. The `keyup` is the event that we most associate with single-key keyboard commands: A command executes when we release the key, not when we first press it. It's worthwhile to experiment with these different events to get a better feel for how keyboard interfaces work.

### Responding to Specific Keys
We often do not want to just randomly respond to every keyboard event. Usually, we want to set specific events  for specific keys or key combinations. Keyboard events include a `keyCode` that can be used to identify the key being pressed. We can find the `keyCode` for any key using a tool like [keycode.info](http://keycode.info/).

Luckily, Vue.js provides quite a few aliases for these codes that make it easier to define an event listener for a specific key. For example, if we wanted our users to submit a form by pressing the `enter` key, we could use this directive:

```html
<form v-on:keyup.enter="handleMyForm" v-on:submit.prevent>
```
In this example, the user would be able to either click a `submit` button or press the `enter` key to submit the form. In both cases, the form will be handled by the `handleMyForm` component method. (Also note that we can have multiple event listeners defined on a single element.)

Here is the full list of `keyCode` modifier aliases provided by Vue.js:

* .enter
* .tab
* .delete (captures both “Delete” and “Backspace” keys)
* .esc
* .space
* .up
* .down
* .left
* .right

If the key we need to respond to is not in this list of modifier aliases, we can still refer to it by the numeric code:

```html
<a v-on:keyup.78="createNewItem">New</a>
```

In this example, we have mapped the key `78` (which corresponds to the `n` key) to a component method that will create a new item. We can pair this reference to a `keyCode` with a modifier key using one of the modifiers listed here:

* .ctrl
* .alt
* .shift
* .meta

We often pair keyboard shortcuts with modifier keys such as `ctrl` or `alt`. It has become increasingly common to let users do more significant actions by pressing `shift + enter`, too. We could accomplish a feature like that with a simple `v-on` directive:

```html
<form v-on:keypress.shift.enter="handleMyForm">
```
In this example we have used the combination of `shift` and `enter` to handle the form submission. We could apply other keyboard shortcuts in more conventional ways, too. Here is a new item shortcut that uses the `ctrl + n` keyboard combination:

```html
<a v-on:keypress.ctrl.78="createNewItem">New</a>
```

With all of the tools Vue.js gives us for handling keyboard input, it's incredibly easy to add keyboard navigation and robust keyboard features to our websites and applications. This can help us present better, more accessible experiences to our users.


## `v-on` Shorthand
If we get sick of writing `v-on:click`, we can alter our templates to use the shorthand version: `@click`. Here is an example of what one of our previous templates would look like using the shorthand.

```html
<template>
  <div class="events">
    <h2>Message: {{ message }}</h2>
    <p><button @click="setMessage('Danger! Danger!')">Show Danger Message.</button></p>
    <p><button @click="setMessage('All Clear!')">Show All Clear Message.</button></p>
  </div>
</template>
```











