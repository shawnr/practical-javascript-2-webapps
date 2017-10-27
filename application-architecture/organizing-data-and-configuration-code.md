# Organizing Data and Configuration Code
As we work on different parts of our applications, we often find that we have similar needs in different places. We might have specific formatting we want to remain consistent across templates, or system data that needs to be available to different components. We might find that we are making API requests to the same API in different components and we want to minimize the amount of repetitive code we are using. In each of these cases, what we absolutely want to avoid is duplicating the same data or logic in multiple locations.

As we saw in previous sections, we will make our applications easier to maintain, build, and enhance if we can adhere to a clean separation of concerns and utilize some common strategies for managing components that need to be reused throughout the application. In this section we will look at some techniques for organizing reusable pieces of our system.

## Common Data Techniques
A common case that often comes up is the need to store system-specific data that can be accessed from any component. This is often used for sets of static metadata that are specific to the project and which are not subject to change. These are usually considered "constants" in the system: They are not meant to be altered by the user or to change during the use of the application or site.

Since we can easily import objects into our components, all we need to do is make sure we have properly structured our data file to export an object. We can store these files wherever makes sense: a `/common/` directory in our `/src/` directory, a well-named file, or somewhere else within the project.

Here is an example of a data file that can be imported into a Vue.js component. Assume this code is in the file `/src/common/constants.js`.

```js
export default {
    'metadataProperty': 'Some value',
    'someChoices': [
        { name: 'Choice One', value: 1 },
        { name: 'Choice Two', value: 2 },
        { name: 'Choice Three', value: 3 }
    ]
}
```
We could make use of this data object by importing it into a Vue.js component:

```html
<script>
import SystemData from `@/common/constants.js`;

export default {
  name: 'demoComponent',
  data () {
    return {
      formOptions: SystemData.someChoices
    }
  }
}
</script>
```

As we've seen in previous projects and examples, we can import the content of `constants.js` with the name `SystemData` inside our component. We can then use that data however we would like within our component logic. In this case, we have set the component's `formOptions` value to the `SystemData.someChoices` array. This could be used to provide a form input with consistent choices and formatting across the entire application.

This technique also shows the fundamental principle at play in the following examples. First we create a `.js` file that contains some object. We must make sure that object is properly "exported" with the `export` command. Then, we can import that object wherever we need it. This is fundamentally the same process we use to accomplish the other techniques for organizing information in our Vue.js applications.

## Common Configuration Techniques
Making common configs for axios etc.

## Common Filters and Methods











