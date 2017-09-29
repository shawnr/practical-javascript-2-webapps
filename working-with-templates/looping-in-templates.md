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
<ul>
  <li v-for="message in messages">{{ message }}</li>
</ul>
```

**rendered template**
```html
<ul>
  <li>Hello, world!</li>
  <li>42 is the meaning of life.</li>
  <li>Question authority.</li>
</ul>
```
In this example, we can see that an Array called `messages` is being looped through. The loop is attached to the `<li>` tag, so that tag is duplicated. As with other directives, the loop would actually duplicate the tag and any content that is inside the tag, including other HTML elements. It is common practice to use the "singular in plural" naming pattern for loops, but we could use whatever names we wish.

Sometimes it's beneficial to know what iteration of the loop we are on. We could modify this example slightly to demonstrate that:

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
<ul>
  <li v-for="(message, index) in messages">{{ index }}: {{ message }}</li>
</ul>
```

**rendered template**
```html
<ul>
  <li>1: Hello, world!</li>
  <li>2: 42 is the meaning of life.</li>
  <li>3: Question authority.</li>
</ul>
```





## Looping Through Arrays