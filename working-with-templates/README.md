# Working with Templates

As we learned when we were first exposed to JavaScript, we can use JS to add, remove, and modify elements from the DOM. This is a very powerful capability, but it quickly becomes tedious to write all of those `document.createElement()` statements and properly combine multiple levels of HTML tag hierarchy. In addition to the repetitive strain of creating elements individually, it's possible to hurt the performance of our applications with DOM manipulation.

Changing elements in the DOM is an intense process for our computing devices. If we change elements often, or if we change many elements on the screen, then we can slow down the functioning of our site and the web browser (and possibly our entire computer). The reason for this performance issue is that many DOM manipulations cause the web browser to re-render the entire page. When that happens there is a (potential) risk of serious impacts on your device performance while the rendering is taking place. Because of the performance risk coupled with the tedious nature of manually manipulating the DOM, we have created templating systems that can help with both of these problems.

Using a template allows us to define an HTML structure and use placeholder "template tags" to represent data we want to output. The template can be processed by our chosen application framework and handled in a way that is somewhat more intelligent than how we might otherwise write our DOM manipulations. In the case of Vue.js, the templating system uses a "virtual DOM" that allows the JavaScript system to calculate all the changes that would happen in the DOM and then apply them in one chunk. That process minimizes the number of times the page must be re-rendered, which makes for a more performant experience. The user will perceive the site as being faster, and it is less likely to cause slowdown issues on our user's computer.

<div class="tip-box">
    <h3>Virtual Dom vs. Shadow Dom</h3>
    <p>There are a lot of things evolving in web technology today, and one area of development is the continued evolution of the DOM. There is a web standard growing around a concept called the "Shadow DOM", and that concept is often confused with the idea of the "Virtual DOM", which is used by application frameworks such as Vue.js and React.</p>
    <p>Do not be confused: Virtual DOM and Shadow DOM are two different things.</p>
    <p>To fully describe the way that either the Virtual DOM or the Shadow DOM work would take an entire book in itself. They are both powerful concepts that benefit web developers in different ways. The simplified explanation of the difference between Virtual DOM and Shadow DOM is this:</p>
    <p>The Virtual DOM is a software design pattern that uses a secondary representation of the DOM in order to collect a batch of DOM changes that can be applied at, essentially, the same time. The goal behind this pattern is to <b>increase performance</b> by consolidating DOM changes and reducing the number of times the page must be re-rendered in the browser.</p>
    <p>The Shadow DOM is a web standard that defines the way any individual HTML element can implement its own DOM structure encapsulated within itself. This is a complex idea, but the bottom line is that the Shadow DOM is concerned with allowing us to define attributes (such as visual styles) on DOM elements without having those attributes spillover and affect other DOM elements. The Shadow DOM is about <b>encapsulation of information</b>.</p>
    <p>The bottom line difference is that the Virtual DOM is a tool for increasing performance of our websites, while the Shadow DOM is about encapsulating logic within components of our website software.</p>
</div>

In addition to the performance benefits and convenience of using templates, these systems usually give us access to a set of tools that can be used to control the presentation of information to the user. Not only can we display dynamic data from our system, but we can also use conditionals and loops to control that display, easily set up event handlers on HTML elements, and perform other functions that help our websites look and work better.

We will explore templates in-depth in this section of the book and practice working with them in the project.









