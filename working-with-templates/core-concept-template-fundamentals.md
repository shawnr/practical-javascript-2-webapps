# Core Concept: Template Fundamentals

There is a need in any web-based project to output HTML that can be rendered by the browser. Whatever functionality we write in JavaScript must be exposed to the user through HTML elements. We can do this in native JavaScript using methods like `document.createElement()` to manually create each HTML element and then append it to the proper parent so it appears in the page. But this approach is tedious and prone to error.

In order to solve the problem of "how do we generate HTML for the user?" we have come up with the concept of "template engines." A template engine is a software tool that allows us to make patterns of HTML. Those patterns can define whatever HTML structure we need in our website or application, and as we define the patterns we note areas where data should be output. By processing the template against a set of data, the template engine can fill in all of those placeholders. The result is the final HTML with all of the dynamic data our application has generated.

The concept of template engines, templating HTML (or other markup), and processing templates against a set of data is not isolated to the world of JavaScript application frameworks. Template engines are used in virtually every web-based application framework, whether that framework uses JS, Python, Ruby, PHP, or other languages. Template engines usually allow for basic features that make it possible to output common data structures (Objects and Arrays, primarily) with tools like loops, conditionals, and the ability to add some form of customized functionality (called "directives" in some JavaScript framework template engines). 

Like every other component we use to build websites, template engines are particular and specific. Different developers, different developer communities, and different projects tend to prefer certain approaches or philosophies of design. Although there are many variations in the details of how different templating engines work, this section tries to focus on some of the generally consistent aspects of these engines. All of the examples in this section are written with the Vue.js template syntax in mind.

## Template Syntax and Vocabulary
Each templating engine uses a slightly different syntax. This syntax is necessary because we must be able to determine the difference between the code meant to define the behavior of the template rendering, and the HTML code meant to be output as part of the final HTML result. 

## Data in Templates



## Displaying Data

## Conditionals

## Looping

## Computed Values

## Filters