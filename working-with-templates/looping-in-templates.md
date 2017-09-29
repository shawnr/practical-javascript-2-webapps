# Looping in Templates

It is very common when building applications to have the need to loop through sets of objects. In JavaScript frameworks, we often work with data that contains Arrays, which are iterable lists that we can process in a loop, or we want to loop through the properties of an Object in order to enumerate the data for the user. Looping in templates allows us to create consistent repetition of HTML structures in order to output better-formatted information to the user.

## Basic Syntax
The loop that we have in Vue.js to work with is a `for` loop. It is invoked with the `v-for` directive. The `v-for` directive is applied much like the other directives we've looked at in this section. The directive can be applied like so:

**data**
```html
<script>
export default {
  name: 'hello',
  data () {
    return {
      messages: [
        "Hello, world!",
        "42 is the meaning of life.",
        "Question authority."
      ]
  }
}
</script>
```

**template**
```html
<div v-if="item.type === 'ticket'">
  <p>Ticket added to cart.</p>
</div>
<div v-else-if="item.type === 'album'">
  <p>Album added to cart.</p>
</div>
<div v-else>
  <p>Item was neither a ticket nor an album.</p>
</div>
```

**rendered template**
```html
<div>
  <p>Ticket added to cart.</p>
</div>
```





## Looping Through Arrays