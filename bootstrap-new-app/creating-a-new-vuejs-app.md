# Creating a New Vue.js Application



<div class="tip-box">
    <h3>Installing "local" Versus "global" Dependencies</h3>
    <p>When we set up our development environments, we want to keep in mind that we may be working on many different projects throughout our career as developers. This means we need to keep a development environment that is robust enough to work for us, but not so specific that it won't work on the next project we undertake. Because of this, we usually install "local" versions of the dependencies our project requires.</p>
    <p>Consider the way we installed all of those dependencies into the <code>node_modules/</code> directory in our project in the last section. All of those dependencies were "local" to the project because they were installed in a directory within the project repository.</p>
    <p>However, there are some tools we might need to use across multiple projects. This often happens with tools like <code>Vue-CLI</code>, which can be used to bootstrap and work with many different projects. In these cases, we want to install the tools "globally" so that we can use them in any project.</p>
    <p>When installing applications with Node Package Manager (NPM), we use the <code>-g</code> flag to install any Node module "globally" so that it can be used in any project. When we install <code>Vue-CLI</code> we use the <code>-g</code> flag so that we can run the <code>vue</code> command from anywhere.</p>
</div>