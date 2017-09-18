# Development Tooling

We will work in what is known as a "Node-based" environment. That is to say, a development environment built on the [Node.js](http://nodejs.org) platform. We will use the [Vue-CLI](https://github.com/vuejs/vue-cli) to bootstrap our apps, and that will allow us to use several popular tools for frontend development, including [Webpack](https://webpack.js.org/).

We will also use [Git](http://git-scm.org) and [Github](http://github.com) to manage our code and deploy our projects.

## About Node.js
Node.js is a development platform that runs Javascript outside of the web browser. This is noteworthy because there are not other major implementations of Javascript outside of the web browser.

The specific Javascript engine Node.js uses is called V8, and it is the engine that is used in Google's Chrome browser. This is a very fast and reliable Javascript engine, and Node is known for being a very fast platform. 

Node allows developers to create tiny Javascript applications called "modules", and then to string those modules together into larger and more complex applications. There are thousands of "Node modules", as they are known. Developers manage modules with a tool called [NPM](https://www.npmjs.com/) (Node Package Manager), which is installed when you install Node.js. 

We will use a variety of extra modules to add functionality to our website, and to do so we will use NPM. NPM is akin to `apt-get`, `homebrew`, or other tools you may have encountered working on Linux or Unix systems.

## About Vue-CLI
We will use the [Vue.js](https://vuejs.org) SPAF as the example platform for this entire book. That means examples will be given in the context of Vue.js, and we will be looking at a lot of Vue.js-specific techniques and tools. This will allow us to learn both more general concepts and pragmatic skills we can use in day-to-day work.

In order to quickly get started on building a Vue.js application, we will use the [Vue-CLI](https://github.com/vuejs/vue-cli) to bootstrap our project skeletons (we will talk more about that next week). The "CLI" in "Vue-CLI" stands for "Command Line Interface." This an application that you run on your local development machine. It takes arguments like any other command line application, and it produces project skeletons which we can use to quickly get going on a new website.

Many SPAFs and other technologies include these kinds of command line interfaces, so it's good to get familiar with how it feels to use a tool like this to manage and work with our projects. 

## About Webpack

[Webpack](https://webpack.js.org/) is a multi-purpose tool primarily concerned with bundling the files of your website together for efficient delivery to the end user. In modern web applications, we don't want to force the user to download dozens of files; we don't want to have troubles with users caching old versions of CSS or JavaScript files; and, we want to make the smallest files possible so they download super fast for our users. Webpack helps us achieve all of this.

Depending on the configuration, webpack can gather all of our CSS and JavaScript, "minify" it down by removing unnecessary blank spaces and lines, and bundle it up into versioned files with a unique filename. This addresses all of the problems we listed above. Webpack can even connect into other tools for validating code or spotting bugs in code and automatically run those as it processes files. It can do a lot more, too, but for now we will keep our use of Webpack as simple as possible.

We will use Webpack to build out our files for delivery as a static website.

## About Git
Git is a source control software used by many developers for web and many other types of projects. Git is open source and free, which makes it available to everyone. 

Git is also "distributed", which means each person who has a copy possesses the entire history of the project, and each developer could serve as a Git server for any other developer. This allows for a great deal of flexibility when working on projects.

Finally, Git is well-known for the way it handles branching and merging. Although these concepts will only be lightly addressed in the content of this book, these are important features used daily by most developers.

## About Github
Github is a hosting service with enhanced tools to handle code repositories using Git. People are often confused about Git and Github. Think of the way Flickr is a hosting service for your images. Flickr is not a camera or illustration software -- it is a tool that allows people to host their images, organize them into galleries, and connect with others who are doing the same thing. Likewise, Github is a tool that allows you to host your code, work with it using helpful tools (like issue management, or wiki pages for documentation), and then connect with other people who are doing the same thing.

Github offers several services that go far beyond simple "Git repository management", and one of those features is called Github Pages. Github Pages is a static website hosting service, meaning that you can use Github to publish HTML, CSS and Javascript to the web and make it available for the general public.

