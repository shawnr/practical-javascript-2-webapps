# Application Architecture and Logical Flow
Modern web development typically uses tools to provide convenient features for developers and to package and deploy code in a way that is optimized for end users. This means there are several components at work when we are developing web applications. These components go together in specific ways.

In this section we will outline some of the components that are going to be involved in the applications we will be building. These applications will use the Vue.js framework, but the general approach could apply to many of the SPAFs that we read about in the previous section.

For the rest of this section, we will discuss this sample application architecture.

![Example Vue.js Application Architecture](/img/vue-app-architecture.png)

## Development Tooling
We will explore the image above from the bottom up. There are several components that are listed in the grey area labeled "Development Tooling". At the base of our development tools is the operating system. This could be Windows, Mac, or Linux, and it provides access to things we use for developing a site such as Git, filesystems, and the ability to read our code editors (to name a few). 

On top of the operating system, it's common to use a fairly broad platform that enables more complex tooling. In our case, we will be using Node.js, which is a platform that allows for execution of JavaScript applications outside the browser. Many web developers have been attracted to Node.js, so they have written tools that work on the Node.js platform. Having Node.js installed on your development system is akin to having Java installed on your computer: You might choose to write programs in Java (or for Node.js), but you are more likely to be just running programs that require those platforms.

Once Node.js is available to us, we can use a whole array of tools for helping us build, package, and deploy our web projects. In our case, we will be using `vue-cli`, which is a Node.js module created by the Vue.js team that will help us start our projects. We will also use Webpack to manage dependencies and process/package our files for delivery to end users. Webpack makes use of many things itself, and our projects will use tools such as ESLint and Babel to check our code or provide additional functionality for our development needs.

Since we are building apps that can be delivered using a static web server, we can deploy our apps using [Github Pages](https://pages.github.com/). Because this form of deployment is so simple, we do not require robust deployment tools. But if we needed, we could also install Node.js modules that would help us deploy to whatever server we wish.

## Application Components
On top of the Development Tooling box in the image above is the Application box (the blue box). This area shows the components involved in a sample web application.

The primary component is the Vue module, which allows us to declare a new application and begin working with code. For the most simple Vue apps, this might be the only component we have at the application level. However, in our example we imagine that we are using a few commonly-used third-party components: `vue-router`, `vue-resource`, and `vuex`. These components each provide features we will explore in more detail later. The important thing to remember now is that we will often use third-party components in our apps, meaning that we will use functionality that we did not create ourselves, but which we want to leverage in our applications.

On the right side of the Application box is a list of three "custom components." These components are not named, but they would correspond to features in our webapp. They might be "profile", "favorite", "post", "article", "video", "image" or whatever other content/function our webapp provides. 

Although we have not specified exactly what features the custom components would add in this example, what is important to know is that these items represent components that we would write ourselves, and which would be unique to our application and its features. This is the heart of the code that we write.

## File Processing/Packaging and Deployment
As mentioned above, our development tooling is concerned with processing files and packaging them for deployment, then actually getting the files to a deployed location. In the case of the most basic projects, this might simply mean pushing your repository to a specific remote server or merging a specific branch. In more complex projects, this could involve a lengthy sequence of events spanning multiple servers and services.

The needs for file processing and deployment will also change significantly depending on the technologies we are using in our web applications. It is often worthwhile to begin with a more simple approach to deploying our apps, but it's crucial to deploy as soon as possible so we can continuously test our applications in their real-world environment.


