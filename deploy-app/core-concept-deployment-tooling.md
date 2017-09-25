# Core Concept: Deployment Tooling

There are many ways to get a website or application online and available for view by the public. Depending on the complexity of our project and the resources at our disposal, our deployment strategy could be very different. Regardless of how we get the code online, we also need to think about exactly what code is going to be delivered to our users. Although the simple methods we begin learning work OK for educational purposes, it's generally important to adopt more robust methods of deploying our work for professional products.

## Before Deployment: Building and Packaging

Before we deploy our sites, we must first "build" and "package" the code. Sometimes this might be referred to "compiling" the code. All of these terms describe the process of putting together the source files we use in development and processing those files to be optimized for the user. 

This means that each individual `.vue` file in the project is going to be broken apart and turned into JS, HTML, and CSS. These files will also be "minified" and possibly "uglified", processes that remove all of the extra whitespace and even replace names with one-letter abbreviations. These processes are performed to get the file size of the combined files as small as possible.

In addition to processing all of the code we've written for our projects, our build process must also gather and combine all of our dependencies. Those dozens of modules in the `node_modules` directory are combined into a tiny package to deliver to our users. It is often larger than the code we write ourselves, as the build report may show.

Once all these files are combined and minified, they must be renamed with version numbers so we can better control the caching of our files by our users' browsers. We don't ever want to have to tell a user to "clear the cache" and try again. That process of renaming is applied to all of the generated JS and CSS files, as well as any static media used in the site (images, etc.). When all the files have been renamed, then another pass must be made through the HTML so references to files can be properly updated.

This whole process is quite complex. It is often handled with a combination of several different tools, each of which specializes in a specific processing or optimization. Depending on our needs and goals, we may decide to include or exclude specific steps in the process. But in the world of modern development, it's unlikely that we would forgo these pre-processing, build, and packaging steps entirely.

## Deployment

Once all of our files are processed and packaged, we need to actually get the files to the server. This can happen in many different ways. In the old days we might use `scp` or `rsync` or even `sftp` to upload files manually. These days we prefer to use systems that are more integrated into the development process as a whole.

It is very common to set up our version control systems to handle deployments in certain cases. It could be that merging changes into the `develop` branch of a project automatically triggers a build to the `development` server. Or we might still manually manage things by logging into the `staging` server and pulling the latest changes to the `master` branch for testing.

There is no way to properly summarize all of the ways in which deployment can be managed. The world of web operations and infrastructure management continues to grow rapidly, so it would not be unusual to have other systems such as containers, [Docker](https://www.docker.com/), or [Kubernetes](https://kubernetes.io/) involved in deployments. Tools ranging from [Ansible](https://www.ansible.com/) to [Salt Stack](https://saltstack.com/) to [Fabric](http://www.fabfile.org/), [Chef](https://www.chef.io/chef/), and [Puppet](https://puppet.com/) have all been popular options for controlling the movement of files to a server (and the provisioning of those servers). 

The rule of thumb that we will cleave to in this book is that we want to keep deployment simple and reliable so we can deploy our code repeatedly through the development process. We should be able to set up deployment of our static websites (that's what we're building in this book) as easily as possible, and we want to be able to deploy anytime we make changes.

## Aprés Deployment

Many systems have tools that kick off after deployment. It's not unusual to have a continuous integration that will run tests against the newly deployed code. It might be desirable to have a system that will notify team members that a deployment has happened. Some organizations want to gather a full set of performance benchmarks every time new changes hit production. 

There are many reasons why we would need to run something after deployment, and it is common to do so. In our case here, we will be deploying to Github Pages, which is a popular static website hosting service. (It is also free, so it's a great place for new developers to build a portfolio.) Github Pages will provide us with a status message on our project's settings page where we can see if there is an error deploying our code and how our site is configured. We could easily leverage Github's tools to add even more post-deployment tests or functions.







