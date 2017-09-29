# Conditionals in Templates

Conditionals are a core part of any templating engine. These allow us to make decisions in the context of the template rendering, which we can use to alter the content we display. We can use conditionals in templates the same way we use them in programming languages: Vue.js templates support the standard `if`, `else if`, and `else` conditions. In this section we will take a look at how to use these in a template.

## Conditional Syntax

Writing conditionals in Vue.js templates involves using the `v-if` directive along with directives that correspond to the typical conditional clauses: `v-else` and `v-else-if`. These operate the way we would expect, and they can be nested and combined in just about any way. Here is an example:

**data**
```html
<script>
export default {
  name: 'hello',
  data () {
    return {
      item: {
        type: "ticket",
        title: "Show Ticket"
    }
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

As we can see from this example, we write the conditional statement between the quotes of the directive assignment. The conditional must begin with a `v-if` directive, which provides the initial conditional statement. If this evaluates to true, as it does in our example, then it will render the element attached to the `v-if` directive (and any child elements contained within). However, if the `v-if` conditional statement were not true, then the template processing would continue to the `v-else-if` statement.

The `v-else-if` statement would be evaluated just like the `v-if` statement was evaluated. If it is true, then that HTML element is rendered along with whatever content it contains. If it is false, then the processing would continue to the `v-else` statement. The `v-else` element is rendered whenever the preceding conditional statements are not true. The `v-else` directive does not require a conditional statement because it will only be rendered when the previous conditional statements evaluate to false.

These conditional structures can be attached to any HTML elements we need to put in our templates. We can nest them if we need to, and by combining them in clever ways we can create all kinds of interesting functionality. We often use conditional statements to modulate the content of our HTML, but if all we want to do is make an element show or hide, there is a shortcut way to do that.

## Show/Hide Content Shortcuts

Vue.js gives us the `v-show` directive, which can be applied to any element. This directive accepts a value that will evaluate to `true` or `false`. If the condition is `true`, the element is made visible. If it is `false`, then the element is hidden. Here is an example:

**data**
```html
<script>
export default {
  name: 'hello',
  data () {
    return {
      showMe: false
  }
}
</script>
```

**template**
```html
<div v-show="showMe">
  This content should be shown when showMe is true.
</div>
```

In this example, the `showMe` value is set to `false`, so the entire `<div>` will be hidden from view. It will still be rendered in the DOM, and it will exist in the HTML in the user's browser, but it is hidden with CSS. This technique is suitable for situations when you want to be able to toggle show/hide on the element very often. It is also suitable when the content of the element does not make as much of an impact on template rendering. 

In situations where we need quick show/hide functionality, the `v-show` directive can be a useful tool.

<div class="tip-box">
  <h3>Deciding Between <code>v-if</code> and <code>v-show</code></h3>
  <p>Without going into the deeper technical details of the difference between <code>v-if</code> and <code>v-show</code>, it is possible to use a rule of thumb to determine when you should use one directive over the other. The <code>v-if</code> directive is a more substantial feature. It requires more effort to render, but it also completely adds and removes the content in the template. If we are using event listeners on content items within the conditional, then the <code>v-if</code> directive allows those listeners to be completely removed from the template when they are not needed. This can improve the overall performance of our applications.</p>
  <p>When we use <code>v-show</code>, the process is not as involved: The <code>v-show</code> directive never adds or removes the content, it only makes the content visible or not. That means that <code>v-show</code> is a little more intense when we first load the page, but then it can toggle the show/hide possibly more quickly than the <code>v-if</code> directive.</p>
  <p>If we are using the show/hide to reveal simple content that does not include many event listeners, then <code>v-show</code> will probably be a better option to create a fast and responsive application. However, if we are trying to add/remove content with event listeners, or more complex template rendering impacts, then we may be better to use the <code>v-if</code> directive in order to avoid those computing costs.</p>
</div>









