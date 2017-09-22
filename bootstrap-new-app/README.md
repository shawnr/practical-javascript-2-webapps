# Bootstrapping a New App

In this section we will discuss the concept of the "application framework" and how we use tools to create basic structures that we can then fill up with functionality. It's important to realize that we usually stand on the shoulders of developers who have come before us, and for most of us it's better to learn to use the amazing tools that other developers create than for us to create those tools from scratch.

There's an old axiom among software developers that [the best line of code](https://blog.codinghorror.com/the-best-code-is-no-code-at-all/) we could write is the one we didn't write. This is because any time we are writing code we are creating the possibility of making a mistake. When we approach large, complex tasks, the likelihood of doing something wrong becomes even more significant. It's best to tackle really big software as a group, and it make sure we adhere to some good review and feedback processes so we can be sure to deliver high quality, bug-free code.

Since most of us, especially when we're just starting out, are working solo or in small teams, it's difficult to take on those great big challenges that produce things like reusable application frameworks. It's often tempting for developers to just begin writing code with what they know, but if the goal is to build a modern web application things will quickly get out of hand if we don't have a clear plan and approach. It turns out that it's usually too difficult to write our own frameworks, and it's too difficult to write apps without a framework.

So what do we do? We use someone else's solution.

Application frameworks, styling frameworks, and other large, generic components are created (usually) by groups of people working together to solve the problem. Even in the cases where a project is primarily spearheaded and stewarded by a single individual (such as with Vue.js, which only has one full-time project member, it's creator, [Evan You](https://medium.freecodecamp.org/between-the-wires-an-interview-with-vue-js-creator-evan-you-e383cbf57cc4)), larger frameworks are used by a community of people who participate in testing and development of the codebase. 

In this book we will use the work of developers who have come before us in order to hit new heights of production. We will use [Vue.js](https://vuejs.org) as the primary example of an application framework, and we will combine many other tools (including Node.js, NPM, Webpack, and more) to build our apps. Rather than inventing our own approach to solve the problems of how to build a great application, we will strive to learn and understand the ways that others have solved these problems. 

