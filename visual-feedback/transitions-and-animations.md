# Transitions and Animations
When data changes on the screen, we often use transitions and animations to call the user's attention to what has just been added or removed. 

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



