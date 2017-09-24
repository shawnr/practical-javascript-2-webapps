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

In short, Webpack keeps the burden on us, as developers, very low, and the way that the official Vue.js template for a Webpack-based application is configured is comfortable to use. We will be investigating how this template is put together and how we can use it more throughout the rest of this book, but for now it might be interesting to look through [the documentation of the Vue.js Webpack Template](https://vuejs-templates.github.io/webpack/) to get an idea of all the things that are in there. Keep in mind that we don't need to understand or master all of this stuff right now. As we work through building apps and making them available to the public, we will touch on many of these things.

In order to create a new app with the Vue-CLI, change directory into your Projects area and run this command:

```
vue init webpack test-project
```

Once initiated, we will be asked some questions. At this point, it doesn't matter very much which answers we give, since we are just using this project to poke around and see what we get. Here is a screenshot of what the process looks like when completed, and we can see a set of answers that will create a minimal project with no test frameworks or extras.

![vue init results](/img/vue-init.png)
<br>The results of the `vue init` command.

This process will create a new directory called `test-project/` (we can call our projects whatever we'd like). We can also see that directions for getting going with development are printed after the command finishes. Change directory into the `test-project/` directory and we should be able to see all the files created for us. 

Inside the repository, we should see the following files and directories:

```bash
drwxr-xr-x  13 shawnr  staff   442B Sep 24 13:09 .
drwxr-xr-x  51 shawnr  staff   1.7K Sep 24 13:09 ..
-rw-r--r--   1 shawnr  staff   312B Sep 24 13:09 .babelrc
-rw-r--r--   1 shawnr  staff   147B Sep 24 13:09 .editorconfig
-rw-r--r--   1 shawnr  staff   145B Sep 24 13:09 .gitignore
-rw-r--r--   1 shawnr  staff   197B Sep 24 13:09 .postcssrc.js
-rw-r--r--   1 shawnr  staff   466B Sep 24 13:09 README.md
drwxr-xr-x  11 shawnr  staff   374B Sep 24 13:09 build
drwxr-xr-x   5 shawnr  staff   170B Sep 24 13:09 config
-rw-r--r--   1 shawnr  staff   200B Sep 24 13:09 index.html
-rw-r--r--   1 shawnr  staff   1.6K Sep 24 13:09 package.json
drwxr-xr-x   6 shawnr  staff   204B Sep 24 13:09 src
drwxr-xr-x   3 shawnr  staff   102B Sep 24 13:09 static
```

We can see that we have some configuration files, including a `.babelrc` that sets up how the Babel linter will work for us. We also have a `package.json` file that lists all the Node.js modules our application depends upon. there is a `build` directory, which contains files that control how the site is built and packaged for deployment. There is also a `config` directory, which contains several configuration files that affect how the app is built and also how the development server and other components of the system work. Inside the `src` directory is the actual content of our application. There is also a `static` directory that will contain static media files that need to be packaged with the site, but which do not require post-processing by the build tools.

Over the next several sections we will look at many parts of this project skeleton and examine the features of this project template. For now, it's important to follow the remaining steps to get the project ready for development.

Run the following command to install all of the Node.js modules our site depends upon:

```
npm install
```

Once that command finishes, we should see an additional `node_modules/` directory in the root of our project repository. This directory will contain all of the dependencies we have in our system. There will be a lot of these. Some are used for our development tools, and others are packaged up with our site and delivered to our users.

Now that we have everything installed to run our project, we can test it out by running the development server with this command:

```
npm run dev
```

We will want to keep that command handy, because that is how we will run the development server whenever we want to do work. The development server will run while we are working and will automatically refresh the page when we make changes to our files. It will also alert us to many issues that might come up in our code as we develop.

Once we have the site up and running on the development server, we can poke around and get to know our Vue.js app a little better.




