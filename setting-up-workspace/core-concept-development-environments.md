# Core Concept: Development Environments

As developers, we may work on many different kinds of software projects. Each one will require us to use different components and tools to build out. This combination of components and tools, and the various utilities, scripts and apps that are required to run them all together, make up a "development environment". 

It is best to maintain a fluid notion of what a "development environment" is, or what tools are in that environment, because it is likely to change for every project you work on. It will even evolve in long-term projects over time as new techniques become available. 

Some developers are keen to push their development environments further and further, which is great for the rest of us. Invariably, those developers invent new ways of doing things that become so convenient that everyone wants to adopt their methods. But it's not crucial that you become highly skilled in conceiving and constructing complex development environments.

For many other developers, the development environment is something that should fade away to the background of their work process. They don't want to think about all the things that are going into making sites build and run: Rather, they wish to focus entirely on the project of building a great site or application. For these developers, it can never be too simple or too convenient.

It's good to know a little bit about what sort of developer you think you are: Do you like to fiddle with the pieces? Or do you want to focus on the code? This is related to another decision we must make very quickly: Do you want to work in a hosted environment? Or would you prefer to work "local"?

Regardless of what the answer to that question is, there are a few things we usually look for in a development environment:

* **Development Server** We generally need to use a server to see the site we're working on. Since we don't want to trigger JavaScript security restrictions, we need to serve our files properly (as opposed to using the "file>open" dialog in the web browser). We also often want a development server to refresh when it detects a change. Modern development servers like [Browser Sync](https://www.browsersync.io/) do much more than just serving and refreshing.
* **Dynamic Compilation of Files** We usually want to edit smaller, shorter files that are then combined when served. The development environment should make that happen for us so we don't have to do it manually.
* **Providing Guard Rails** We often use tools like linters, validators, and test suites to make sure that we have not created any bugs or broken any features. We usually like to have these tools wired into our development environments so we can be sure to deliver higher quality code.

## Hosted vs. Local

When setting up your development environment, you first have to choose whether you wish to work on your local machine (your laptop or desktop computer) or in a hosted environment (usually accessed through a web browser).

For many years, when we wanted to edit websites we logged in to a server and made changes using command line text editors like Vi and Emacs. Once desktop Linux became popular (which coincided largely with Macs converting to OS X, which is also a Unix-based operating system), it was possible for developers to begin working "local" -- on their own computers. 

Working in a "local development environment" has a number of advantages: It allows for the fastest possible response from your test server (since that server is running on the same computer you are using), and it allows you to configure every small aspect of your environment. This is the way most developers work today.

The down side of local development is that it can often be complex, and, especially when working on a large project in a team setting, it can lead to wasted hours spent fixing development environments and keeping everyone running together. There are many tools and techniques that have been developed to mitigate those issues, so you may hear about things like "virtualization" and "containers" in relation to local development environments.

The alternative to local development environments is the hosted development environment. These services (like [CodeAnywhere.com](http://codeanywhere.com), [Nitrous.io](http://nitrous.io), and [Cloud 9](https://c9.io/)) offer hosted development environments that you can bring up with a few clicks of the mouse. They all offer some level of interface built on top of the development environment to allow you to make easier choices when provisioning your development environment.

On these systems, you typically create a "devbox" (or whatever creative term they use) with a base configuration. Those base configurations range from "HTML5" and "Python" to "Drupal" or "MEAN Stack". These configurations often have all the tools installed that we are installing during this first project.

## How to Use This Book
This book assumes you are working in a local development environment. It provides most of the information you need to get various components up and running. 

If you are using a hosted development environment, then you can probably bring up a "Node.js stack" or "HTML5 stack" and have access to the core components that we need here. For most of the hosted development environments, you can also run installation commands if, for example, you can bring up a Node.js devbox, but it doesn't have Yeoman and related apps installed. The instructions provided here for installing those components should also work on your hosted development environment.

One area where there may be differences about how to set things up is when it comes to setting up Git and connecting your hosted development environment to your Github repository. You will likely need to consult the documentation for whatever hosted development environment provider you are using. (Almost all of them support connecting dev environments to Github.)