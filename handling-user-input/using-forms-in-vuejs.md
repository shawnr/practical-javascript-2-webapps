# Using Forms in Vue.js

In Vue.js we can use forms to gather data from the user, and the form fields and events can easily be connected to our component logic. To accomplish this, we create bindings between the form fields and our component data. The `v-model` directive is how we assign these relationships. By binding fields to data values, we can do a lot directly in templates, or we can create event listeners and use component methods to perform actions when the form is submitted or when another event occurs.

## Basic Input Data Binding with `v-model`
The `v-model` directive associates a form input element with a variable in our component's data. This variable can be referenced within the component logic (in computed values, methods, or filters), or it can be referenced within the template for display to the user. The `v-model` directive creates a two-way binding between the value in the component logic and the value in the template, just like other variables we define in the component's `data()` function.

START HERE NEXT

## Select and Checkbox Arrays

## Generating Options with `v-for`

## Providing Default Values with `v-bind:value`

## Model Modifiers
Sometimes we need to modify the data, or how we collect the data, in a predictable way. Vue.js provides three modifiers we can use with the `v-model` directive to change the way data is bound. These allow us to provide a better user experience in many situations. 

### `.lazy`
The `.lazy` modifier allows us to alter the way data is updated throughout the system upon user input. Normally, a bound input field will update data on the `input` event fired by the field. This can be beneficial, but sometimes it is not desirable. When we would prefer to fire the event on the `change` event (as opposed to the `input` event), we can use the `.lazy` modifier. 

Here is what this would look like on a text input:

```html
<input type="text" v-model.lazy="username">
```

### `.number`
The `.number` modifier insures the value is typecast as a Number when it enters the component logic. By default, any information coming out of a text input field will be typed as a String in our JavaScript logic. If we use the `.number` modifier, we can be sure our calculations will work as planned. Here is an example:

```html
<input type="number" v-model.number="myNumber">
```

Although this example uses the input type `number`, **all** HTML inputs are typed as Strings when they are brought into the Vue.js component logic. If we wish for a value to be cast as a Number, we must use the `.number` modifier.

### `.trim`
We can use the `.trim` modifier to remove extra whitespace from the beginning and end of a user's data. This is often used on login forms when we wish to discount any leading or trailing spaces that might result from a user's copy/paste. We can apply this modifier just like the others:

```html
<input type="text" v-model.trim="username">
```



