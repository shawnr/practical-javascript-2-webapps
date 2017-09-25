# Project: Bootstrap an App

To practice with making an application using the Vue-CLI tool, let's bootstrap an app that we can work with in sections 5 (Debugging the App) and 6 (Deploying the App) to practice working with the project skeletons we can create.

## Check for Vue-CLI
If we have Vue-CLI installed properly, then we can run the command `vue --version` from anywhere on our command line and see the version of the Vue-CLI that we have installed. We should see a number above `2.8`. If we see an error (something about the `vue` command not existing), then we should install Vue-CLI by running this command:

```
npm install -g vue-cli
```

## Bootstrap the Application
Once we have Vue-CLI properly installed, we can bootstrap our project skeleton. This will create all the files we need to get started writing our application. Create a new app using the `webpack` template:

```
vue init webpack test-project
```

Answer the questions like we see in the screenshot below:

![vue init results](/img/vue-init.png)
<br>The results of the `vue init` command.

Once the project skeleton is available, `cd` into the directory where your project was created.

## Install Dependencies
After creating the project skeleton, we still need to install the Node modules that the project depends upon. We do this with the command:

```
npm install
```

Once the installation is complete, we can test the project by running:

```
npm run dev
```

We should see the development server start up and a new tab should open in the default web browser with our project loaded.

![Default screen from webpack project template](/img/vue-default-web.png) 
<br>Default screen from Webpack project template

If we see a screen that looks like the one above, then we have successfully installed our dependencies and our project is up and running.














