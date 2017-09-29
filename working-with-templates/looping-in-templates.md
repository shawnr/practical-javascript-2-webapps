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

By adding `index` as a value in the declaration of the loop, we can use that within the loop. We could write conditionals to test, in case we wanted to do some conditional HTML formatting. Or we could use the information to make the data more clear for the user.

It's also possible to loop through Objects, too:

**data**
```html
<script>
export default {
  name: 'hello',
  data () {
    return {
      profile: {
        username: "jdoe",
        firstname: "Jane",
        lastname: "Doe",
        email: "jdoe@example.com"
      }
  }
}
</script>
```

**template**
```html
<ul>
  <li v-for="(value, key) in profile">{{ key }}: {{ value }}</li>
</ul>
```

**rendered template**
```html
<ul>
  <li>username: jdoe</li>
  <li>firstname: Jane</li>
  <li>lastname: Doe</li>
  <li>email: jdoe@example.com</li>
</ul>
```

In this example, rather than using the `item` and the `index` naming, we are using the `value` and `key` naming. This allows us to go through all of the properties in the Object, which are referenced using named keys, and output those along with the actual data stored in each property. This is often a better way to output the data in an Object. (Note: It is possible to write `v-for="value in profile"`, too, but that would only give us the property data to work with and not the property keys.)

These basic tools open the door to a lot of possibility. We can format and present data efficiently, consistently, and we can spend a great deal of attention on the details of forming our HTML structures.

## More Complex Looping

Of course, loops can be nested. This is often the case when we are presenting information from some sort of data API. A common example might be a system where we are showing search results with the tags that have been applied to them:

**data**
```html
<script>
export default {
  name: 'hello',
  data () {
    return {
      results: [
        { title: "Computers are Fun",
          tags: ["computers", "programming"]
        },
        { title: "Bugs are Cool",
          tags: ["bugs", "nature", "activities"]
        },
        { title: "The Sun is Bright",
          tags: ["sun", "astronomy", "climate"]
        }
      ]
  }
}
</script>
```

**template**
```html
<ul>
  <li v-for="result in results">
    {{ result.title }}<br>
    Tags: <span v-for="tag in result.tags">{{ tag }}</span>
  </li>
</ul>
```

**rendered template**
```html
<ul>
  <li>
    Computers are Fun<br>
    Tags: <span>computers</span><span>programming</span>
  </li>
  <li>
    Bugs are Cool<br>
    Tags: <span>bugs</span><span>nature</span><span>activities</span>
  </li>
  <li>
    The Sun is Bright<br>
    Tags: <span>sun</span><span>astronomy</span><span>climate</span>
  </li>
</ul>
```
In this example we can see that the Array of results contains Objects. Each of those Objects has a property called `title` that is a String, and a property called `tags` that is an Array. In order to output all the results and all the tags for each result, we must use a nested loop. 

We have attached the first loop to the `<li>` element so that it contains all the information about each result. In order to display the `result.tags` data we have attached another loop to the `<span>` elements because those are inline elements that will be easier to style into our desired presentation.

This is just one example of the power of nested loops. Loops are very common in any template usage, so practicing and becoming capable with them is a crucial skill for developers to build.













