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
            <a href="/item/{{item.id}}/">{{ item.name }}</a>
        <li>
    {% endfor %}
</ul>
```

**Vue.js Template**
```html
<ul id="search-results">
    <li class="result" v-for="item in items">
        <a href="/item/{{item.id}}/">{{ item.name }}</a>
    </li>
</ul>
```

In these two examples, we can see that although these frameworks are quite different their templating languages use the same fundamental concepts and very similar approach. The syntax varies a little bit: Django templates use "template tags" instead of directives to invoke features like a loop. The Django template will loop all content between the `{% for %}` and `{% endfor %}` template tags.

The Vue.js template uses directives instead of template tags. The `v-for` attribute on the `<li>` element is the directive that establishes the `for` loop. It will create a copy of the HTML element the directive is attached to, and anything inside that element will be part of the looped HTML generation.

The output of both of these template snippets would be something like this:

```html
<ul id="search-results>
    <li class="result">
        <a href="/item/12/">Betty Holberton</a>
    </li>
    <li class="result">
        <a href="/item/9/">Anita Borg</a>
    </li>
    <li class="result">
        <a href="/item/17/">Frances Spence</a>
    </li>
    <li class="result">
        <a href="/item/51/">Grace Hopper</a>
    </li>
    <li class="result">
        <a href="/item/42/">Leah Culver</a>
    </li>
</ul>
```

The specific content of the list would depend on the data in the system, but assuming we were searching for famous female software developers, this is a possible set of returned results.

When we process the data in the template context against the template, we call that "template rendering," or just "rendering" for short. We render a template that is injected into the browser (or, in the case of Django templates, which is then served to the user as an entire HTML page).

It is important to learn the syntax of the specific templating engine we are using, but most engines allow for the same basic kinds of features.

## Data in Templates

The data used to render a template is called the "template context" or "context" for short. This is basically the scope of the template: All the things in the software application that the template knows about. Usually, our templates do not need to know about most of the parts of our systems. We only want to render a comparatively small set of data that is used within a specific page or component. By keeping our template context small and free of superfluous data we speed up the processing of the template.

Data can be referred to in templates in any location to provide dynamic HTML generation. These can be used to add classes to elements, construct URLs, loop through data structures, or create virtually any HTML structure we need. Standard dot-notation referencing can be used within most templating engines to refer to properties of data in the context.

Here is an example where we have a few different values in the context. (This example, and the rest of the examples on this page, use Vue.js template engine syntax.)

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

## Displaying Data

## Conditionals

## Looping

## Computed Values

## Filters