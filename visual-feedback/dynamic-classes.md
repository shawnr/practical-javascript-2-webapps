# Dynamic Classes
In Vue.js it is possible to bind the `class` attribute on an element to data values. This can allow us to more easily toggle class assignments from within our component logic. By altering the classes on components we can cause visual changes to happen when the user interacts with our application, or call the user's attention to some part of the interface that has been updated.

These techniques are not unique to Vue.js; many frameworks allow similar kinds of class toggling and binding.

## Binding Data to `class` attributes
We often have a situation where we wish to apply a class when a specific condition is true. For example, when showing a list of items with "Favorite" buttons, it would be useful to be able to apply a class when the user clicked to add an item to their "Favorites." We see this kind of interface all the time.

To bind data to class attributes we can use the `v-bind` directive. The binding of values works the same when using it with a class/style attribute as with other attributes, but Vue.js can interpret specific object structures to fill in the proper class/style changes. Here is an example of how a favorite button might indicate whether or not it has been clicked:

```html
<button v-bind:class="{ favorited: isFavorite }" v-on:click="toggleFavorite">Favorite</button>
```
We can see in this example that we have used `v-bind` to bind the `class` attribute to a JavaScript object. The object defines a `favorited` property, and the value of the property is `isFavorite`. (The `isFavorite` value is defined as part of the component's data object, and it is toggled via the `toggleFavorite` method.) Whenever `isFavorite` equals `true`, the `favorited` class will be applied to this element. Whenever `isFavorite` is `false`, the `favorited` class will be removed.

We can use objects with multiple properties to add/remove multiple classes to an object in the same way. Each property should point to a boolean value that will either be `true` or `false`. This value can be altered through any normal means in our code.

For the vast majority of cases, being able to add/remove specific classes is a useful way of altering the visual appearance of an element. However, sometimes we encounter situations where binding the `style` attribute itself is required in order to achieve our desired effect. 

## Binding Data to `style` attributes
In some cases, we want to use some dynamic data to actually alter the style of an element. This is often required when writing complex applications such as data dashboards or browser-based games. But there is a more simple case that often requires us to directly insert a style definition: Placing the user's avatar in the background of an element. This method can be advantageous because we can more easily crop and control the display of avatars that might have differing dimensions.

Here is an example using `v-bind` to bind the data value for a user profile image to the background of a style:

```html
<template>
  <div>
    <div class="avatar" v-bind:style="{ backgroundImage: 'url('+ user.image +')' }">
      {{ user.username }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProfileImage',
  data () {
    return {
      user: {
        username: 'shawnr',
        image: 'http://lorempixel.com/400/400/animals/'
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.avatar {
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center center;
  background-color: #666;
  color: white;
  text-align: center;
  padding: 10px;
  width: 200px;
  height: 200px;
  border-radius: 50%;
}
</style>
```
We can see that this component displays a profile image. It uses a data object called `user` to provide the username and the URL for the user avatar image. We have defined the styles to shape the avatar image and control its size, but we cannot write a style definition that includes the user's specific image URL. Instead, we must apply the image URL to the `background-image` style property for the `div.avatar` element.

To accomplish this, we bind another data object to the `style` property. This time, Vue.js knows to read the properties of the data object looking for terms that correspond to CSS properties. **Please note:** We can use either "kebab case" (with dashes, like `background-image`) or "camel case" (with capital letters, like `backgroundImage`) to reference CSS properties. Vue.js will map these properties and their values to CSS properties and insert them into the `style` attribute. The end result in our example looks like this:

![User Avatar with Dynamic Background](/img/user-profile-avatar.png)
<br>User Avatar with Dynamic Background

Using this technique, we gain a lot of flexibility. We can define the data object in our template, or we can define a data object in our component logic and then reference the name of that object in the template. We can set up event listeners to dynamically change values based on user interactions, which can then be translated into visual effects on the screen. This opens the door for all sorts of interesting interface concepts and designs.


