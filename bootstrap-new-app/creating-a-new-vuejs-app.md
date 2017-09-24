# Creating a New Vue.js Application

Creating a new Vue.js application is a fairly straightforward process, and it is something that will become very easy once we understand the basics. It's often worthwhile to bootstrap a brand new project in order to try out some technique or idea outside of the complexity of a larger software system. Sometimes when debugging it's good to make a fresh project and then move parts of our code into that project in a methodical way in order to find the pieces that break. There are many other reasons why being able to quickly get up and running with a project is valuable. 

## Install Vue-CLI

In order to use the [Vue-CLI](https://github.com/vuejs/vue-cli) tool, we must first install it. This software requires Node.js to work, and it can be installed using NPM. To install Vue-CLI in our development environment, run this command:

```
npm install -g vue-cli
```

This will install Vue-CLI globally so we can use it anywhere. Once the installation is complete, we can check the version that was installed by running `vue --version`. If everything went smoothly, we should see the version number displayed. We can also run `vue --help` to see a list of commands we can use, or to get more information about specific commands.

<div class="tip-box">
    <h3>Installing "local" Versus "global" Dependencies</h3>
    <p>When we set up our development environments, we want to keep in mind that we may be working on many different projects throughout our career as developers. This means we need to keep a development environment that is robust enough to work for us, but not so specific that it won't work on the next project we undertake. Because of this, we usually install "local" versions of the dependencies our project requires.</p>
    <p>Consider the way we installed all of those dependencies into the <code>node_modules/</code> directory in our project in the last section. All of those dependencies were "local" to the project because they were installed in a directory within the project repository.</p>
    <p>However, there are some tools we might need to use across multiple projects. This often happens with tools like Vue-CLI, which can be used to bootstrap and work with many different projects. In these cases, we want to install the tools "globally" so that we can use them in any project.</p>
    <p>When installing applications with Node Package Manager (NPM), we use the <code>-g</code> flag to install any Node module "globally" so that it can be used in any project. When we install Vue-CLI we use the <code>-g</code> flag so that we can run the <code>vue</code> command from anywhere.</p>
</div>

## Using Vue-CLI

The Vue-CLI tool allows us to quickly bootstrap projects using project templates. These templates can be created by anyone, so if we find ourselves needing a very specific or exotic template, we can create that and use it with Vue-CLI. Since we are just beginning, we don't really have any exotic or highly specific needs. Instead, we can use one of the included "official templates" maintained by the Vue.js community.

Throughout this book it is recommended to use the `webpack` template, which defines a project with all the features we will explore throughout the rest of this book. Webpack is a popular application bundling and build tool, and it is used with many technologies (including React and Angular). Webpack handles dependency management (making sure all our third-party modules are available to our application when we deploy) and build process (all the tasks that must happen to package our application for deployment). Webpack is advantageous because it handles things that other tools (such as Browserify) rely on external helpers (like Gulp or Grunt) to handle. 

In short, Webpack keeps the burden on us, as developers, very low, and the way that the official Vue.js template for a Webpack-based application is configured is comfortable to use.








