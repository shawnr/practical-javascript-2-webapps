# Glossary

The terms listed here will be highlighted throughout the text. Hover over them to see the definition as you are reading.

## abstraction
The process of moving or organizing segments of program logic or data into modular components that can be referenced from multiple locations in the code.

## API (Application Programming Interface)
A feature that allows for functions and data within one system to be accessed programmatically by another system. For example, we can use the Open Weather Map API to request weather data for thousands of cities around the world, and we can use that data within our own applications.

## API end point
The URL used by an API to indicate where a specific feature or data set exists. For example, `http://api.example.com/v1/users` could indicate the `users/` endpoint of the `example.com` API.

## backend
Having to do with the server-side of a web-based project. Often used in phrases such as "backend programming languages", which would be languages that are executed on the server (Python, Java, Ruby, PHP, etc.). The opposite of *frontend*.

## breakpoint
An intentional stopping or pausing place in a program used for debugging purposes.

## directive
A function used in a template to invoke some special behavior (e.g. setting an event listener, invoking a loop, or creating a conditional) used to process the template. Custom directives may be created by developers, and frameworks often provide a selection of default directives.

## encapsulation
The process of hiding information or complex logic behind a developer-friendly interface.

## DOM
The [Document Object Model ](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)(DOM) is the JavaScript representation of the HTML structure and status in the browser software.

## frontend
Having to do with the web browser. Frontend technologies include HTML, CSS, and JavaScript. The opposite of *backend*.

## modifier
An extra command that can be appended to a directive to alter its behavior. For example, the `.prevent` modifier can be used with the `v-on` directive to "prevent defaults" on event handlers.

## mustache syntax
The name for the Vue.js default template syntax, which uses double curly braces (`{{ }}`) to denote variable interpolation in the template. Mustache syntax is only used to output the value of a variable in a template, and never used with directives.

## query string parameters
Values appended to the URL using the `?` to denote the beginning of the parameters, and the `&` to denote each individual key/value pair. These values are often used with `GET` requests to an API endpoint. For example, in the URL `http://api.example.com/search?q=test&order_by=rating` the values `q` and `order_by` are the parameters.

## refactor
To re-organize and re-structure code for an improved developer experience without altering functionality.

## router
The component of an application that determines what view the user should see based on the URL they request.

## single page application
A JavaScript application that does not refresh the browser in order to show different "pages" of information. This avoids use of the browser's navigation and history mechanism, which requires those features to be implemented in JavaScript. Thus, many single page applications use a robust JavaScript framework.

## software architecture
According to [Wikipedia](https://en.wikipedia.org/wiki/Software_architecture): Software architecture is "the high level structures of a software system, the discipline of creating such structures, and the documentation of these structures."

## syntax
The "grammar" of a programming language: A set of rules that dictate the way symbols are used to construct the logic that will be interpreted to run a program.

## template context
The "context" of a template refers to the set of information (Objects, Arrays, methods, etc.) that is used to process the template into the final output.

## template engine
The software component responsible for processing templates and outputting the results. The engine typically defines rules about syntax and features of the templates, and frameworks can often swap out templating engines to suit the needs and preferences of developers.

## template rendering
The process of computing the final output of a template. This involves combining data in the template context using the template instructions and HTML structures written in the template itself.

## website architecture
When considering the way a website is built and functions, we often use the term "website architecture" to describe the way these structures go together.