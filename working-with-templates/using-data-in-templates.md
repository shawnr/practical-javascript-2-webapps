# Using Data in Templates

One of the primary goals of using templates is to interpolate data into the template. It's critical to be able to insert data into the context of the template and to update that data when the system changes. For the most part, the process of using data in templates is just a matter of referencing the value using the mustache syntax (double curly braces). But there are some finer points that are worth knowing about.

## Basic Data Output
As we saw in the previous section, we use the mustache syntax to output data in our template HTML:

```html
<a>{{ item.name }} - ID: {{ item.id }}</a>
```

The data in the template context comes from the `data()` function defined in the Vue component itself:

```html
<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Hello, World!',
      item: {
        id: 12,
        name: "Foo"
      }
    }
  }
}
</script>
```
The object returned by the `data()` function is revealed to the template context. The "root" properties of the object are accessible as named variables. In the example above, `msg` and `item` are the "root" properties of the data object, so they can be referenced as `{{ msg }}` and `{{ item }}` in the templates. Of course, the `item` property references another object, and those properties can be accessed as `{{ item.id }}` and `{{ item.name }}` (as seen in the other example above).

Interpolating variables from the template context like this sets up a two-way binding: The data is rendered in the HTML for the user to see, and it will update if the system updates the value. So if the user performs some action our code can update the values of any data being rendered on the page and the user will see that information be updated. This process of connecting our application logic and template output is called "binding."

We can use the mustache syntax to output basic JavaScript expressions, too. The following are all valid data output:

```html
<p>The next page is: {{ page + 1 }}</p>
<p>A ternary statement: {{ ok ? 'YES' : 'NO' }}</p>
<p>We can call data type methods: {{ message.split('').reverse().join('') }}</p>
```

All of the expressions above are allowed, which offers an immense range of output options when interpolating data into a template. Although most data processing should be done inside the Vue Component, these expressions can be handy for formatting and optimizing presentation of data for the user.

These methods work fine for outputting text data between HTML tags. But there are some additional considerations when the situation gets a little more complex.

## HTML Data

We should generally avoid the output of data values that contain HTML markup. It's usually more advantageous to have, for example, the text of the headline without the heading tags rather than the headline with tags baked into the system's data. Sometimes we want to output the headline of an article as the main title of a page, and other times we want to output the headline as the title of a list item in the sidebar. In different situations, we need different HTML structures, so having HTML saved as part of the text data is problematic. This is why we use templates.

However, sometimes we have data objects such as messages, blog posts, and other components that might involve saving HTML formatting in the system data. In these cases, we need to use a slightly different technique to tell the Vue.js template engine that we wish to output HTML that should be rendered as part of the template. To do this, we will use the `v-html` directive:

**data object**
```html
<script>
export default {
  name: 'hello',
  data () {
    return {
      message: `<p>Nullam nulla eros, ultricies sit amet, nonummy id, imperdiet feugiat, pede. In dui magna, posuere eget, vestibulum et, tempor auctor, justo.</p>
                <p>Fusce commodo aliquam arcu. Fusce fermentum odio nec arcu.</p>`
    }
  }
}
</script>
```

**template code**
```html
<div v-html="message"></div>
```

**rendered template**
```html
<div>
  <p>Nullam nulla eros, ultricies sit amet, nonummy id, imperdiet feugiat, pede. In dui magna, posuere eget, vestibulum et, tempor auctor, justo.</p>
  <p>Fusce commodo aliquam arcu. Fusce fermentum odio nec arcu.</p>
</div>
```

As we can see in this example, the `message` data property contains a string with HTML formatting. In order to properly render this HTML in the template, we use the `v-html` attribute. Anytime we use a directive we use the equals sign and then put the argument in quotes, so they look like normal HTML attributes. In this case, the variable `message` will be used for the content of this HTML element.

<div class="tip-box">
  <h3>Use Caution with HTML Content</h3>
  <p>It is possible to introduce security vulnerabilities in our projects by outputting user-provided HTML with the <code>v-html</code> directive. Malicious users could insert scripts into comments or other user-generated text and those could attack our other users. This is why most commenting or review systems either disallow all HTML formatting, only allow a small set of safe tags that are validated upon submission of the content, or use an alternative markup formatting to do basic text enhancement.</p>
  <p>Using <code>v-html</code> should be reserved for content we create and verify is safe before use. And, where possible, we should avoid HTML formatting in our internal content</p>
</div>

## Data in HTML Attributes

It's often the case that we want to use data from the template context to augment HTML attributes. For example, we may want to construct a URL that includes a user's username. Or we may need to build a details link that includes the item's ID:

```html
<a href="item/12">View Details</a>
```

Since we cannot use the mustache syntax in HTML attributes, we must use the `v-bind` directive to insert the data from the template context. This creates a data binding between the information inserted in the attribute and the logic of our application, so if the values change the HTML will be updated accordingly.

Assuming we have a data object similar to the one used in the example above, we could write our link like this:

```html
<a v-bind:href="'item/' + item.id">View Details</a>
```

We can see that the `v-bind` attribute uses the Vue.js method of adding parameters to a directive. In this case, we need to tell the `v-bind` directive *which* attribute we want to bind. We are binding the `href` attribute. As with all directives, we provide arguments between quotes after an equals sign. In this case, we are using a JavaScript expression to concatenate the String `'item/'` with the value of `item.id`. 

Another common example is when we have image URLs provided in our data, and we want to put the images into an HTML structure for display:

**data**
```html
<script>
export default {
  name: 'hello',
  data () {
    return {
      image: {
        src: "images/mypicture.jpg",
        title: "Placeholder Image"
      }
    }
  }
}
</script>
```

**template**
```html
<div class="image">
  <img v-bind:src="image.src" v-bind:alt="image.title">
</div>
```

**rendered template**
```html
<div class="image">
  <img src="images/mypicture.jpg" alt="Placeholder Image">
</div>
```

In this example we can see how we can use the `v-bind` directive to populate the image `src` and `alt` attributes. These substitutions don't require any JavaScript concatenation of the text and data. This kind of manual binding is common as we work with images and other elements in our templates.

## Shorthand for `v-bind`
Although using the `v-bind` directive is fairly straightforward, we might do it often in our templates, and we might want to stop typing `v-bind` so often. Vue.js provides us with a shorthand we can use to set a manual binding on an attribute. The following code is equivalent:

```html
<img v-bind:src="image.src">

<img :src="image.src">
```

We can abbreviate `v-bind:attributeName` to simply `:attributeName` in order to save a few keystrokes. This shorthand does not change anything about how the directive functions, and there is no positive or negative effect beyond removing the need to type `v-bind`.





