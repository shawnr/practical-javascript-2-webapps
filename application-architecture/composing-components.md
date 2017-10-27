# Composing Components
Vue.js is organized around the [Web Components Standard](https://www.w3.org/standards/techs/components#w3c_all), which is an idea that has gained momentum over the past few years. The idea of web components has been popularized primarily by another single page application framework, React. React and Vue.js share a many common approaches and concepts, most of which stem from their mutual interest in web components.

The idea of web components is straightforward and powerful: Allow developers to create reusable, custom HTML elements that handle whatever tasks are needed in an application or site. By creating small, specific components, we can use several components together to achieve a more complex interface or experience. In the jargon of Vue.js, this process of combining components to build our interfaces is known as "composing components." 

In Vue.js we write components that handle specific parts of our application. Most of these components should be small and dedicated completely to their role in the application: A "favorite" button, a search result, or the content of an article. Other components might handle larger pieces of the application, such as a component to control an entire "About Us" view, or a component that would build up a gallery of images or video.

Those larger components will most likely reference smaller components within their templates. This allows us to create more complex interfaces, but we can still keep our individual components as lean as possible. In each component, we want to keep our template, logic, and stylesheet as small as possible. Fewer lines makes our files more readable, more easily and immediately understandable, and eliminates many opportunities for error.

The process of determining how we should organize our applications is similar to the methods for refactoring that we discussed earlier: We want to create a solid separation of concerns, and that can be achieved by encapsulating functionality into specific components. We can also use our choices about what components we create to provide a more friendly interface for developers of our application. 

Because all of this can be difficult to imagine in the abstract, let's explore some concrete examples of how we use components together within a Vue.js project.

## Using Child Components in Templates

## Setting Properties on Child Components

## Using Events and Listeners

## Syncing Properties