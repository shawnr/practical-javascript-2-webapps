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


## Data in HTML Attributes

## Binding Data















