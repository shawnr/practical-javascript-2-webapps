# Core Concept: Application Frameworks

An [application framework](https://en.wikipedia.org/wiki/Software_framework) is a body of code designed to make it easier to create applications. Frameworks are usually language-specific and purpose-driven. For example, [Django](https://djangoproject.com) is a web application framework for Python, and [.Net](https://en.wikipedia.org/wiki/.NET_Framework) is a framework for writing Windows applications in C#. Frameworks also  tend to be driven by some sort of design philosophy. This means that the framework usually represents a way of thinking about writing code and organizing applications.

These factors combine to give a framework its "feel" and features. For example, in a game development framework, it would not be odd to focus on an event-driven architecture, since that might better suit writing certain kinds of games. We would also expect that a game framework would give us the ability to manage things like character animations and adding/removing entities on the screen. 

In a web application framework, we expect to have features that allow us to create URLs that have specific functionality, process templates to generate pages that contain user-specific data, and manage the basics of security, speed, and general best practices. Whether we are working with Ruby or Django, we expect the same core features (and both of those frameworks deliver many desirable features). 

## Difference Between a Framework and a Library

Sometimes it becomes murky to see the difference between a library (like jQUery) and a framework (like Vue.js). It often feels like libraries are "smaller" than frameworks, although some libraries (again, like jQuery) are extremely large, and some frameworks (like Backbone.js) are tiny. In fact, there are three primary characteristics that make a body of code a framework as opposed to a library. Quoting from [Wikipedia](https://en.wikipedia.org/wiki/Software_framework), these characteristics are:

* **inversion of control:** In a framework, unlike in libraries or in standard user applications, the overall program's flow of control is not dictated by the caller, but by the framework.
* **extensibility:** A user can extend the framework - usually by selective overriding; or programmers can add specialized user code to provide specific functionality.
* **non-modifiable framework code:** The framework code, in general, is not supposed to be modified, while accepting user-implemented extensions. In other words, users can extend the framework, but should not modify its code.

So when we use a framework, we give up some of the control over how our application is organized and which parts get invoked first. We must adapt to the methods of the framework itself in order to make a functional piece of software. When we use a framework, it doesn't make sense to try to undermine the basic logic of the framework. We generally do not touch the core code of the framework itself. We want to keep our underlying frameworks as clean and unmodified as possible in order to enable better future maintenance and expansion of our applications.

Of course, the framework is supposed to enable a reasonable variety of projects, so the point about extensibility is important. Rather than modify the core code of the framework, we add our own components and configure the details of how features work in order to extend the functionality of the framework to fit our needs. A framework should give us an easy way to write our application logic and to bring in additional features unique to our requirements.

## Easing the Pain of Getting Started

When we use frameworks, one of the benefits we get is that we can usually start a project more quickly. There are many things all web applications do, and setting up the basic foundations for those core features is repetitive and time-consuming. With a framework, we can often run a simple "bootstrap" script and get directly into writing our own code. 

In the case of Vue.js, there is a command line application called [Vue-CLI](https://github.com/vuejs/vue-cli) (the "CLI" stands for Command Line Interface) that we can use to manage our projects. The Vue-CLI comes with several "official" project templates (and it allows developers to write their own project templates, too), so we can quickly bootstrap a "project skeleton" based on one of the project templates. That's a lot of jargon, so let's unpack it.

A "project template" is a set of files that represent the beginning state of a generic Vue.js project. Templates might vary depending on the type of project they are trying to represent, and it's possible to create our own custom templates that we could use for our unique requirements.

A "project skeleton" is what we have after we "run" or "bootstrap" a project template. We are given a bare bones application that has the core features the framework gives us, and which we can then extend to build out our unique functionality.

<div class="tip-box">
    <h3>Bootstrap vs. "bootstrap"</h3>
    <p>Many new developers become confused by the use of the word "bootstrap" in web development circles. This is because we have <a href="https://getbootstrap">Bootstrap</a>, which is a popular style framework for use on projects. But the word "bootstrap" has been used by developers for ages to refer to all sorts of "getting things started" situations.</p>
    <p>We often refer to "bootstrapping" a project, in the sense described earlier on this page. We also refer to "bootstrapping" a server, meaning powering up and configuring a server, or "bootstrapping" an application, meaning setting up the environment and dependencies for an application that already exists. In a generic sense, "bootstrapping" can refer to any technical process of getting something going.</p>
    <p>That's why the team that created the Bootstrap style framework chose that name: Their goal was to create a framework that would help developers get going more quickly with a visual style that, although a little generic, would look better than no styling at all and which would put developers in a good position to write high quality styles in their projects. The name Bootstrap was inspired by the fondness we developers have for the term "bootstrap" in general.</p>
</div>











