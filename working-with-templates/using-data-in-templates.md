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

It's often the case that we want to 

## Binding Data















