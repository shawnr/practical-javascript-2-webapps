# Composing Components
Vue.js is organized around the [Web Components Standard](https://www.w3.org/standards/techs/components#w3c_all), which is an idea that has gained momentum over the past few years. The idea of web components has been popularized primarily by another single page application framework, React. React and Vue.js share a many common approaches and concepts, most of which stem from their mutual interest in web components.

[The idea of web components](https://developer.mozilla.org/en-US/docs/Web/Web_Components) is straightforward and powerful: Allow developers to create reusable, custom HTML elements that handle whatever tasks are needed in an application or site. By creating small, specific components, we can use several components together to achieve a more complex interface or experience. In the jargon of Vue.js, this process of combining components to build our interfaces is known as "composing components." 

[In Vue.js we write components](https://vuejs.org/v2/guide/components.html) that handle specific parts of our application. Most of these components should be small and dedicated completely to their role in the application: A "favorite" button, a search result, or the content of an article. Other components might handle larger pieces of the application, such as a component to control an entire "About Us" view, or a component that would build up a gallery of images or video.

Those larger components will most likely reference smaller components within their templates. This allows us to create more complex interfaces, but we can still keep our individual components as lean as possible. In each component, we want to keep our template, logic, and stylesheet as small as possible. Fewer lines makes our files more readable, more easily and immediately understandable, and eliminates many opportunities for error.

The process of determining how we should organize our applications is similar to the methods for refactoring that we discussed earlier: We want to create a solid separation of concerns, and that can be achieved by encapsulating functionality into specific components. We can also use our choices about what components we create to provide a more friendly interface for developers of our application. 

Because all of this can be difficult to imagine in the abstract, let's explore some concrete examples of how we use components together within a Vue.js project.

## Using Child Components in Templates
In any given component template, we can reference "child" components. These child components are revealed to the template as a custom HTML element, and they are defined in the `components` property. Borrowing inspiration from [the Vue.js documentation about Components](https://vuejs.org/v2/guide/components.html#Local-Registration), here is an example of how we could implement a simple `<counter>` element as a child component:

**The `Home.vue` file**
```html
<template>
  <div class="home">
    <h1>Child Components Demo</h1>
    <counter></counter> | <counter></counter> | <counter></counter>
  </div>
</template>

<script>
import Counter from '@/components/Counter';

export default {
  name: 'Home',
  data () {
    return {

    }
  },
  components: {
    counter: Counter
  }
}
</script>
```

**The `Counter.vue` file**
```html
<template>
  <button class="fave" v-on:click="incrementCounter">
    {{ counter }}
  </button>
</template>

<script>
export default {
  name: 'favorite',
  data () {
    return {
      counter: 0
    }
  },
  methods: {
    incrementCounter: function () {
      this.counter++;
    }
  }
}
</script>
```

We can see that in these two files we have two components. The `Counter.vue` file defines a component with a very simple template: It is just a `<button>`. It uses a single data value (`counter`), and it has an event listener defined to increment the counter on each click using the `incrementCounter` method. This component could be used on its own at a specific URL route, but it would not be a very interesting view. Instead, we have defined this component with the intention of using it in another component.

In the `Home.vue` file, we can see that there is a new property in the component logic called `components`. We can also see that the `Counter` component has been imported at the beginning of the logic. It is required to import each child component before using it in our component logic. The `components` property is an object, and each property of the `components` object defines a relationship between a child component and the name that will be used for the custom HTML element in the component template.

In the template of the `Home` component, we can see that we have the child component tag (`<counter></counter>`) used three times. Each of these uses will result in a button that we can click to increment the number it displays. When we view the `Home` component in the web browser, we can click the buttons and see a result that looks like this:

![Counter Buttons](/img/child_component1.gif)
<br>Counter Buttons

As we can see in the image above, when we click each button it keeps its own tally using its own counter. Although these buttons are each a _copy_ of the `Counter` component, they are individual instances. The ability to isolate functionality and data into a child component can be useful in itself, but it's often necessary to pass some information to the child component in order to do something with it.

## Setting Properties on Child Components

Components can define a property called `props` (properties), which is an object listing the names (and, possibly, additional details) of any values that should be passed into the component. These properties can be referenced in the templates using the normal mustache syntax (`{{ propName }}`) or within the component logic like normal (`this.propName`). Properties passed to a child component are bound to the parent component logic, so if the value of the property changes in the parent component, that will refresh the value within the child component, too.

This is very useful for writing child components to handle things like show/hide of individual items. Here is an example using an imaginary FAQ page:

**Parent Component: `FAQ.vue`**
```html
<template>
  <div>
    <h1>FAQ</h1>
    <ul class="faqs">
      <li v-for="faq in faqs">
        <question v-bind:question="faq.question" v-bind:answer="faq.answer"></question>
      </li>
    </ul>
  </div>
</template>

<script>
import Question from '@/components/Question';

export default {
  name: 'FAQ',
  data () {
    return {
      faqs: [
        {
          question: 'Why does the sun shine?',
          answer: 'The sun is a miasma of incandescent plasma.'
        },
        {
          question: 'What is the meaning of life?',
          answer: '42.'
        },
        {
          question: 'How to become a web developer?',
          answer: "Never gonna give you up, never gonna let you down"
        },

      ]
    }
  },
  components: {
    question: Question
  }
}
</script>
```
Notice that this parent component controls the "Frequently Asked Questions" view. There is an array called `faqs` that contains the questions and answer we wish to show the user. We want to have these listed by questions, and then reveal the answer when the user clicks on the question. If we were to try to do this directly inside the `FAQ` component, we would need to coordinate a lot of information and add a data property to each of the question/answer sets in order to know which one should be shown or hidden when a user clicks. This logic would get overly complex and it is not necessary.

Instead, we handle this component like we would handle any content presentation to the user, except we use a child component called `Question` to display the content. The `Question` component is imported at the top of the `FAQ` component logic, and then the `Question` component is listed under the `components` property.

We can see that in the template for the `FAQ` component, we loop through each `faq` in the `faqs` array. Within the loop, we insert a `<question>` element and we bind the `question` and `answer` attributes to their corresponding values `faq.question` and `faq.answer`. These attributes will be translated into the properties that the `Question` component expects.

Let's take a look at the child component to see how these are used to display the content to the user.

**Child Component: `Question.vue`**
```html
<template>
  <div class="question">
    <h2><a v-on:click="toggleAnswer">{{ question }}</a></h2>
    <p v-show="showAnswer" class="answer">{{ answer }}</p>
  </div>
</template>

<script>
export default {
  name: 'FAQ',
  data () {
    return {
      showAnswer: false
    }
  },
  props: {
    question: String,
    answer: String
  },
  methods: {
    toggleAnswer: function () {
      this.showAnswer = !this.showAnswer;
    }
  }
}
</script>
```
In the `Question` component, we have a simple template defined: We output the `question` and `answer` properties in the template. In the component logic we define those two values in the `props` object, and we also define a simple `toggleAnswer` method that toggles the `showAnswer` value between `false` and `true`. The `showAnswer` value is used to control the `v-show` directive on the answer content.

Here is an example of what this looks like in action:

![FAQ Example in Action](/img/faq_example.gif)
<br>FAQ Example in Action

In this case, what would have taken several extra lines of JavaScript, and a significant increase in complexity, without composing components has been accomplished in a much more straightforward way. It's easy to understand how the components work together when reading through the code, and we have successfully encapsulated the functionality of the show/hide answers inside the `Question` component. We could even use the `Question` component outside the scope of the FAQ page if we had the need. Essentially we have created a component that will accept content of a certain structure and handle displaying it according to our rules. This is a modular piece of our application that could be used anywhere.

## Using Events and Listeners
The data flow in Vue.js is "one-way," which means that data is only allowed to be passed from parent component to child component. This works great for child components that are purely display-oriented, but we often need to trigger some kind of action in the parent component when an action takes place in the child element.

In this situation, we can use custom events to trigger the action in the parent component. This is how the Vue.js information flow was designed to work:

![Vue.js information flow](/img/vuejs-info-flow.png)
<br>[Vue.js information flow](https://vuejs.org/v2/guide/components.html#Composing-Components)

As we can see from the diagram, information is put into a child component via "properties" and the child component can signal back to the parent component when an event has occurred. Let's look at a simplified catalog and shopping cart setup to get a clearer picture of how this works.

**Parent Component: `Catalog.vue`**
```html
<template>
  <div>
    <h1>Store</h1>
    <p>Number of items in your cart: {{ numItems }}</p>
    <ul class="items">
      <li v-for="item in catalog">
        <item v-on:addedItem="incrementItemCount" v-bind:name="item.name" v-bind:price="item.price"></item>
      </li>
    </ul>
  </div>
</template>

<script>
import Item from '@/components/Item';

export default {
  name: 'FAQ',
  data () {
    return {
      catalog: [
        {
          name: 'Widget',
          price: '12.43'
        },
        {
          name: 'Gidget',
          price: '74.98'
        },
        {
          name: 'Fidget',
          price: '3.47'
        },

      ],
      numItems: 0
    }
  },
  components: {
    item: Item
  },
  methods: {
    incrementItemCount: function () {
      this.numItems++;
    }
  }
}
</script>
```
We can see that in the `Catalog` component, we have a `catalog` array defined and a `numItems` value. The `catalog` array provides the items for us to loop through and display. The `numItems` value shows how many items we have already added to our shopping cart. We can also see that the `Catalog` component uses the `Item` component in its template. This is defined in the `components` property, and it corresponds to the `<item>` element used in the template. Finally, there is an `incrementItemCount` method that is used to increase the item count whenever a new item is added to the shopping cart.

The one thing that really makes this example different than the previous one is that we have added an event listener to that custom `<item>` element:

```html
v-on:addedItem="incrementItemCount"
```
That listener is waiting for the `addedItem` event to be triggered. When an `addedItem` event is detected, the `Catalog` component will execute the `incrementItemCount` method, which will increase the value of `numItems` and update the display for the user. Let's take a look at the `Item` component to see how that works.

**Child Component: `Item.vue`**
```html
<template>
  <div class="item">
    <h2>{{ name }}</h2>
    <p>Price: ${{ price }}</p>
    <button v-on:click="addToShoppingCart">Add to Cart</button>
  </div>
</template>

<script>

export default {
  name: 'item',
  data () {
    return {

    }
  },
  props: {
    name: String,
    price: Number
  },
  methods: {
    addToShoppingCart: function () {
      console.log(`Adding ${ this.name } to cart.`);
      this.$emit('addedItem');
    }
  }
}
</script>
```
In the `Item` component, we have a simple template defined that shows some information and provides an "Add to cart" button. The button has a `v-on` directive applied to it, and it's looking for a `click` event. When the user clicks the button, it executes the `addToShoppingCart` function. In a real-world implementation, this method would probably perform an API request to record the user's data in a persistent database. For the sake of this example, it merely logs a message in the browser console. It also emits a custom event trigger, `addedItem`. 

When all of this is put together, the result is a working counter that increments regardless of which item we add to the shopping cart:

![Custom Event Example](/img/custom-event-example.gif)
<br>Custom Event Example

The parent `Catalog` component is managing the display of the number of items the user has added to their shopping cart. Each instance of the `Item` child component is only concerned with watching itself and triggering the `addedItem` event when the user clicks the "add to cart" button. Using the one-way data flow in Vue.js, we have been able to send data to the child component and then receive a signal back from the child component. In a real-world example, that event would probably trigger the parent component to refresh an API call or perform some other action to update the information about the shopping cart being shown to the user.

By creatively combining these two abilities, there are very few cases that cannot be handled. (And when those rare cases arise, Vue.js does provide some ways for us to create exceptions to these rules.) Following solid principles of composing components makes our Vue.js applications easier to build, easier to maintain, and easier to improve.








