# Project: Testing the Workspace
In order to determine whether our development environment is set up properly, it's useful to try cloning and running an existing project. Work along with the following directions to test your workspace.

This project uses the [WATS 4000: Up and Running](https://github.com/suwebdev/wats4000-up-and-running) repository.

## Fork and Clone
You will need a Github account to fork the repository. Visit the [repository homepage](https://github.com/suwebdev/wats4000-up-and-running) and click the "fork" button. Once you have completed forking the repository, you can clone it to your local development environment. This will copy all the files from the repository to your workspace.

## Install Dependencies
In order to get this project to work, we need to install the dependencies. To do so, run the `npm install` command in the project repository. You should see output indicating that NPM has installed quite a few packages (this may take several minutes to complete).

Once you have finished installing dependencies, take a look at the project itself.

## Project Files

![Project Folders](/img/project-folders.png)
<br>Project Folders after cloning and installation of dependencies.

You will notice several key parts of the project here. Let's take a quick trip through what we see in this list and identify some of the key parts of the application. We will go quickly through this for now because we will revisit almost all of these pieces as we work through more details of building applications.

* `build` &ndash; This directory contains files that instruct Webpack how to build and compile the site.
* `config` &ndash; This directory contains files that configure details about the project for use by Webpack and (possibly) other components.
* `node_modules` &ndash; This is where all of the dependencies the site uses are stored during development. (Check it out; there are lots of these!)
* `src` &ndash; This is where the custom code we write for this unique project goes. Look inside and you'll see the components that make this site work.
* `static` &ndash; This is where files that are needed but which should not be manipulated by build tools other than copying them into the project's compiled code directory.
* config files &ndash; The files that begin with dots contain configurations for how different dev tools should work. For example, `.gitignore` lists a bunch of file and directory names that should not be included in the Git repository (such as the `node_modules` directory, which we do NOT include in our version control). 
* `index.html` &ndash; This is the base HTML container for our project.
* `package.json` &ndash; This is what Node and `npm` use to track dependencies in our project. Inside this file is a list of all the dependencies we are using.

## Run the Dev Server
As we work, we want to run the development server. When you do, you should see the app running. You can check it out in your web browser and test out the simple functionality.

While we have the dev server running, we can open up our editor and modify some of the files. If we open `src/App.vue` we will see the template that includes the `<h1>` tag for the page. We can modify the contents of that tag and save the file to see the live reload capability of this development server. (We can also play with the CSS in this file if we wish.)

Note: We have not gone over how a Vue.js app works yet, but it's still worthwhile to poke around and see. If things break, we can always reset your clone of the repository.

Once we done experimenting with the development server, we can quit the server using the `ctrl-c` keyboard combination in the terminal.

## Build the Site
As we mentioned earlier, the goal of using development environments is that we can work with source code that is more friendly and still deliver highly optimized code to our users. To get a feel for how this works, run the following command:

`npm run build --report`

This command builds and compiles all the code in our project and puts it in a directory called `dist` in the root of the project. The `--report` flag also produces a report about what parts of our project take up the most space for downloading/serving to our users.

![Webpack Build Report Web View](/img/build-report-web.png)
<br>Web View of the Webpack Build Report

Webpack provides us with a handy visual representation of the parts of our deployment package. We can see that the bulk of the package is actually the core dependencies we have in `node_modules`, and the tiny purple bar on the side represents the code we have in our custom app.

Click around and check out this view, then go back to your terminal to read the text report.

![Webpack Build Report in Terminal](/img/build-report-terminal.png)
<br>Webpack Build Report in Terminal

In the terminal view of the Webpack Build Report we can more easily see that webpack has combined files and organized them by "chunks". We can see the file size and the file name that has resulted from the processing of these files.

If we look inside the `dist/` folder, which was created inside our repository by the build process, we can see that those files have been saved under `dist/static/` (as well as the other files that make up our site.

![Files in dist folder](/img/dist-folder.png)
<br>Files in the `dist/` Folder

These files are the results of combining many source files into just a few files for delivery to our users. This cuts down on the number of request a user makes to the server in order to download our application. We also see that the files have been "versioned" with the addition of "hashes" that represent a unique version of that file. These hashes are updated when the contents of the files that are being combined changes. Changing the names of these files when the contents change helps us avoid issues of browsers and networks caching files and serving users old code. (We never want to tell a user to "clear the cache" in their browser again!)

## Continue Exploring
It's worthwhile to continue exploring the code to get a better understanding of what parts we're dealing with. Think of this as moving into a new neighborhood: There are already buildings and streets here, so we don't need to build everything from scratch. But we do need to find our ways and get comfortable in this new environment.

Much of the rest of this book will serve like a GPS as we learn about building applications. We will get details that should make all of this doable at a fundamental level. But please take detours and try things outside what is prescribed in this book.

If we don't take some ambling walks around our new neighborhood we will never find the better paths, interesting scenery, or potential for enjoyment that exists.