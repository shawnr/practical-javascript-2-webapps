# Quiz: Routing and URLs

Please enjoy this self-check quiz to help you identify key concepts, points, and techniques discussed in this section.

<quiz name="">
    <question>
        <p>What does "routing" refer to?</p>
        <answer correct>Associating URLs with the corresponding components in an application.</answer>
        <answer>Determining the fastest path from point A to point B.</answer>
        <answer>Navigating around the web.</answer>
        <answer>Assigning IP addresses.</answer>
        <explanation>Routing refers to associating URLs with the corresponding components in an application.</explanation>
    </question>
    <question multiple>
        <p>What modes can be used to manage URLs in a Vue.js app?</p>
        <answer>quirksmode</answer>
        <answer>standard</answer>
        <answer correct>history</answer>
        <answer correct>hash</answer>
        <explanation>The two modes for routing supported in Vue.js are "history" and "hash" modes.</explanation>
    </question>
    <question>
        <p>Where are the route definitions found in a standard Vue.js project created with the Vue CLI webpack template?</p>
        <answer><code>/src/routes.js</code></answer>
        <answer correct><code>/src/router/index.js</code></answer>
        <answer><code>/src/App.vue</code></answer>
        <answer><code>/router.js</code></answer>
        <explanation>The <code>/src/router/index.js</code> file contains the route definitions.</explanation>
    </question>
    <question multiple>
        <p>Which of the following properties of a route can be used with <code><router-link></code> or <code>router.push()</code>?</p>
        <answer correct><code>name</code></answer>
        <answer><code>children</code></answer>
        <answer><code>component</code></answer>
        <answer correct><code>path</code></answer>
        <explanation>The <code>path</code> and <code>name</code> properties can be used to create a link with <code><router-link></code> or <code>router.push()</code>.</explanation>
    </question>
    <question>
        <p>In a module import statement using the default webpack configuration, what does the <code>@</code> symbol stand for?</p>
        <answer><code>email</code></answer>
        <answer><code>repository</code></answer>
        <answer correct><code>src/</code></answer>
        <answer><code>components</code></answer>
        <explanation>The <code>@</code> symbol stands for <code>src/</code> in the path to a file.</explanation>
    </question>
    <question>
        <p>Nested URLs are defined using which property of the route object?</p>
        <answer><code>nested</code></answer>
        <answer><code>babies</code></answer>
        <answer correct><code>children</code></answer>
        <answer><code>siblings</code></answer>
        <explanation>The <code>children</code> property defines views nested in a parent view.</explanation>
    </question>
    <question multiple>
        <p>Which parameters are defined in the following route path: <code>'/posts/:slug/page/:pageNum'</code></p>
        <answer correct><code>slug</code></answer>
        <answer><code>page</code></answer>
        <answer correct><code>pageNum</code></answer>
        <answer><code>posts</code></answer>
        <explanation>The two route parameters defined in this path are <code>slug</code> and <code>pageNum</code>.</explanation>
    </question>
    <question multiple>
        <p>What do we need to do to add a new route to our application?</p>
        <answer correct>Create the new component file.</answer>
        <answer correct>Add the route to the routes Array.</answer>
        <answer>Update all of the other component templates.</answer>
        <answer correct>Provide links or logic to move users to the new location.</answer>
        <explanation>To add a new route to our application we must create the component that will handle the route, add it to the route definition Array, and provide links or logic to allow our users to find the new location.</explanation>
    </question>
    <question multiple>
        <p>What are the advantages of using named routes?</p>
        <answer>Routes get sad without names.</answer>
        <answer correct>We can alter the paths in our application without editing templates.</answer>
        <answer correct>It's easier to remember names than convoluted paths.</answer>
        <answer correct>It can be difficult to remember parameter ordering in the path.</answer>
        <explanation>There are many reasons to use named routes over paths. These are just a few of them.</explanation>
    </question> 
</quiz>

<div class="no-quiz">
     <h2>Visit Quiz Online</h2>
     <p> 
         The quiz on this page has been removed from your PDF 
         or ebook format. You may take the quiz by visiting
         this book online.
     </p>
</div>
