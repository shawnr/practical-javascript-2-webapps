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

## Transitioning Single Elements

## Transitioning Groups of Elements

## Reusable Transitions



