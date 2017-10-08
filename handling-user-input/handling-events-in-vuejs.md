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

## Preventing Default Event Handling

## Detecting Keyboard Input

## Other Event Modifiers












