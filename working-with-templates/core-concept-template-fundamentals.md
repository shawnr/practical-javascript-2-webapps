# Core Concept: Template Fundamentals

There is a need in any web-based project to output HTML that can be rendered by the browser. Whatever functionality we write in JavaScript must be exposed to the user through HTML elements. We can do this in native JavaScript using methods like `document.createElement()` to manually create each HTML element and then append it to the proper parent so it appears in the page. But this approach is tedious and prone to error.

In order to solve the problem of "how do we generate HTML for the user?" we have come up with the concept of "template engines." A template engine is a software tool that allows us to make patterns of HTML. Those patterns can define whatever HTML structure we need in our website or application, and as we define the patterns we note areas where data should be output. By processing the template against a set of data, the template engine can fill in all of those placeholders. The result is the final HTML with all of the dynamic data our application has generated.

The concept of template engines, templating HTML (or other markup), and processing templates against a set of data is not isolated to the world of JavaScript application frameworks. Template engines are used in virtually every web-based application framework, whether that framework uses JS, Python, Ruby, PHP, or other languages. Template engines usually allow for basic features that make it possible to output common data structures (Objects and Arrays, primarily) with tools like loops, conditionals, and the ability to add some form of customized functionality (called "directives" in some JavaScript framework template engines). 

Like every other component we use to build websites, template engines are particular and specific. Different developers, different developer communities, and different projects tend to prefer certain approaches or philosophies of design. Although there are many variations in the details of how different templating engines work, this section tries to focus on some of the generally consistent aspects of these engines. All of the examples in this section are written with the Vue.js template syntax in mind.

## Template Syntax and Vocabulary
Each templating engine uses a slightly different syntax. This syntax is necessary because we must be able to determine the difference between the code meant to define the behavior of the template rendering, and the HTML code meant to be output as part of the final HTML result. 

To get an idea of how template syntax might vary, here are examples from Vue.js and the Django framework (which is a server-side Python framework). Each of these examples shows a template snippet that will result in a list of search results showing the result name as a link. We assume there is an Array called `items` available in the template context. The `items` Array contains a list of Objects that each have `id` and `name` properties. Each of these templates demonstrates basic data output inside a `for` loop.

**Django Template**
```html
<ul id="search-results">
    {% for item in items %}
        <li class="result">
            <a>{{ item.name }} - ID: {{ item.id }}</a>
        <li>
    {% endfor %}
</ul>
```

**Vue.js Template**
```html
<ul id="search-results">
    <li class="result" v-for="item in items">
        <a>{{ item.name }} - ID: {{ item.id }}</a>
    </li>
</ul>
```

In these two examples, we can see that although these frameworks are quite different their templating languages use the same fundamental concepts and very similar approach. The syntax varies a little bit: Django templates use "template tags" instead of directives to invoke features like a loop. The Django template will loop all content between the `{% for %}` and `{% endfor %}` template tags.

The Vue.js template uses directives instead of template tags. The `v-for` attribute on the `<li>` element is the directive that establishes the `for` loop. It will create a copy of the HTML element the directive is attached to, and anything inside that element will be part of the looped HTML generation.

The output of both of these template snippets would be something like this:

```html
<ul id="search-results>
    <li class="result">
        <a>Betty Holberton - ID 12</a>
    </li>
    <li class="result">
        <a>Anita Borg - ID 9</a>
    </li>
    <li class="result">
        <a>Frances Spence - ID 17</a>
    </li>
    <li class="result">
        <a>Grace Hopper - ID 51</a>
    </li>
    <li class="result">
        <a>Leah Culver - ID 42</a>
    </li>
</ul>
```

The specific content of the list would depend on the data in the system, but assuming we were searching for famous female software developers, this is a possible set of returned results.

Each time we wish to output the value of a variable in the template context, we use the double curly braces syntax:

```
<a>{{ item.name }} - ID: {{ item.id }}</a>
```

This syntax indicates that the value of variable named between the double curly braces should be output into the template. This double curly braces syntax is often called "mustache" syntax because the curly braces look like mustaches. Some templating languages use other syntax to output individual variables, but this syntax is very common in templating engines today.

When we process the data in the template context against the template, we call that "template rendering," or just "rendering" for short. We render a template that is injected into the browser (or, in the case of Django templates, which is then served to the user as an entire HTML page).

It is important to learn the syntax of the specific templating engine we are using, but most engines allow for the same basic kinds of features.

## Data in Templates

The data used to render a template is called the "template context" or "context" for short. This is basically the scope of the template: All the things in the software application that the template knows about. Usually, our templates do not need to know about most of the parts of our systems. We only want to render a comparatively small set of data that is used within a specific page or component. By keeping our template context small and free of superfluous data we speed up the processing of the template.

Data can be referred to in templates in any location to provide dynamic HTML generation. These can be used to add classes to elements, construct URLs, loop through data structures, or create virtually any HTML structure we need. Standard dot-notation referencing can be used within most templating engines to refer to properties of data in the context.

Here is an example where we have a few different values in the context. (This example, and the rest of the examples on this page, use Vue.js template engine syntax.) This example imagines a page listing weather and events for Seattle, WA.

**Data in the Template Context**
```js
{
    city: "Seattle",
    state: "WA"
    forecast: {
        temps: {
            high: 83,
            low: 58
        },
        summary: "Mostly sunny."
    },
    events: [
        {
            name: "Film Festival",
            start: "8:00pm",
            end: "10:00pm",
            location: "12th Ave Arts"
        },
        {
            name: "Art Opening",
            start: "7:00pm",
            end: "10:00pm",
            location: "Seattle Art Museum"
        },
        {
            name: "Community Town Hall",
            start: "6:00pm",
            end: "7:30pm",
            location: "City Hall"
        }
    ]
}
```

**Template Code**
```html
<h1>Events for {{ city }}, {{ state }}</h1>
<aside class="weather">
    <p class="summary">{{ forecast.summary }}</p>
    <ul class="temps">
        <li class="high">{{ forecast.temps.high }}</li>
        <li class="low">{{ forecast.temps.low }}</li>
    </ul>
</aside>
<ul class="events">
    <li v-for="event in events">
        <h2>{{ event.name }}</h2>
        <p class="times"><span class="start">{{ event.start }}</span><span class="end">{{ event.end }}</span></p>
        <p class="location">{{ event.location }}</p>
    </li>
</ul>
```

The results of this code would be the output of all of the data in the data context described above. We can see that the data object is revealed to the template, and the root properties of the object (`city`, `state`, `forecast`, and `events`) are accessible using their names. To access the properties of those objects, we use the same dot-notation references that we use in our JavaScript: `forecast.temps.high` or `forecast.summary`.

Because `events` is an Array, we can loop through it. We should discuss loops in more detail.

## Looping
Looping is a core feature in pretty much any templating language. Part of the huge benefit of templates is that we can loop through our data and output many copies of the same HTML structure. This allows us to save time not writing all of that code by hand, and it also allows us to make sure we are consistent with how each item in an Array is presented to the user.

Creating loops in templates is usually syntactically sparse: We usually don't have to write a lot to make a loop happen. From the example above, assuming we have an Array called `events` in the template context, we could write this:

```html
<ul class="events">
    <li v-for="event in events">
        <h2>{{ event.name }}</h2>
        <p class="times"><span class="start">{{ event.start }}</span><span class="end">{{ event.end }}</span></p>
        <p class="location">{{ event.location }}</p>
    </li>
</ul>
```

In this example we see a `<ul>` element with a class attribute. The "events" class does not affect anything in the template and would be used by the CSS to style the element. The for loop is attached to the `<li>` element because that is the element that we actually want to copy for each item in the `events` Array. The loop is invoked with the `v-for` directive, which is written like an attribute on the HTML element that we want to duplicate for each item in the loop. 

Loops in templates generally repeat a specific set of HTML for each item in the Array they are looping through. The elements that are children of the HTML element with the loop attached will also be duplicated. So in this example, the result would be an unordered list with three list items:

```html
<ul class="events">
    <li>
        <h2>Film Festival</h2>
        <p class="times"><span class="start">8:00pm</span><span class="end">10:00pm</span></p>
        <p class="location">12th Ave Arts</p>
    </li>
    <li>
        <h2>Art Opening</h2>
        <p class="times"><span class="start">7:00pm</span><span class="end">10:00pm</span></p>
        <p class="location">Seattle Art Museum</p>
    </li>
    <li>
        <h2>Community Town Hall</h2>
        <p class="times"><span class="start">6:00pm</span><span class="end">7:30pm</span></p>
        <p class="location">City Hall</p>
    </li>
</ul>
```

We can see that all of the elements that were within the `<li>` elements are also duplicated. This allows us to do much more work fine-tuning the presentation of an individual instance of our repetitive HTML structures, so we are able to write better code that can be more useful to our users.

Within the loop it's important to realize how we are accessing the data in each item. As the template engine iterates through the loop, each item in the Array is handled. On each iteration one item from the Array is assigned the name we have specified in our code. 

In this example, we have used a common convention. We have an Array named with a plural noun (`events`), so we set up our loop to use the singular form of that noun to reference each item as it comes through the loop:

```html
<li v-for="event in events">
```

This name is determined by us. We could write `v-for="item in items"` or `v-for="posts in blogPosts"` or any other combination of terms that makes sense in the context of our application. What is important is that we consistently use whatever name we assign to the item as it moves through the loop code. If we call it `event` then we must reference `event.name` and `event.location`. If we wrote `<li v-for="oneEvent in Events">` then we would need to reference `oneEvent.name` and `oneEvent.location`.

## Conditionals

Conditionals are used within templates to "turn on and off" elements. We often use them to modulate between states, or to show/hide things like administrative or editing controls. Consider, for example, the common situation where we wish to show a user a login link when they are not logged in and an account link when they are logged in. It is not unusual to have a template snippet like this in a web application:

```html
<ul id="identity">
    <li v-if="username">
        <a href="/account/">{{ username }}</a>
    </li>
    <li v=if="!username">
        <a href="/login/">Login</a> or <a href="/signup/">Sign Up</a>
    </li>
</ul>
```

In this example, we assume that when a user logs in to our site the variable `username` is made available to the template context. This is a common approach for many websites, and it allows us to use conditional directives to determine whether we should show a personalized link to the account management page, or if we should show links to login or make an account. 

We can also use conditional elements to accomplish show/hide features, to help manage tabbed information displays, and all sorts of other interface customizations. The speed of template rendering in JavaScript application frameworks tends to be very fast, so it is usually reliable to use these conditionals in combination with visual effects and other processing to create highly interactive and responsive interfaces.

## And More

Templating engines are each unique, and most of them give developers a way to extend their functionality. In Vue.js, developers are given easy ways to implement template filters, which allow us to create reusable data formatting or presentation functions that can easily be applied within the template. In other templating engines the methods might be different but there is usually a way to add more to the abilities of the engine.

It's worthwhile to dig into the features of our templating engine to be sure we are using all of the power in our tools. These simple features provide a huge range of capability and once we master these concepts we can accomplish a lot through our use of templates.













