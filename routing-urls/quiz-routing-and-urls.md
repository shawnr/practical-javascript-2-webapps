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
    <question>
        <p>What do we often use to handle an event in our Vue.js components?</p>
        <answer>component function</answer>
        <answer correct>component method</answer>
        <answer>JavaScript statements</answer>
        <answer>HTML forms</answer>
        <explanation>We often handle events using component methods we have defined as part of our Vue.js component.</explanation>
    </question>
    <question multiple>
        <p>Which directives are useful for controlling which handlers execute when an event is triggered?</p>
        <answer correct><code>.stop</code></answer>
        <answer><code>.go</code></answer>
        <answer correct><code>.prevent</code></answer>
        <answer correct><code>.once</code></answer>
        <explanation>The <code>.stop</code>, <code>.prevent</code> and <code>.once</code> directives can be used to control which handlers execute when an event is triggered.</explanation>
    </question>
    <question>
        <p>What do the modifiers <code>.enter</code>, <code>.ctrl</code>, and <code>.tab</code> do?</p>
        <answer correct>They filter keyboard events so the handler executes only when the corresponding key is pressed</answer>
        <answer>They indicate the method used to handle an event</answer>
        <answer>They exclude the key from any event listener</answer>
        <explanation>Those modifiers filter keyboard events so the handler executes only when the corresponding key is pressed.</explanation>
    </question> 
    <question>
        <p>Which keyboard event would we use if we wanted to make a "new file" keyboard shortcut?</p>
        <answer><code>keydown</code></answer>
        <answer correct><code>keypress</code></answer>
        <answer><code>keyup</code></answer>
        <explanation>The <code>keypress</code> event would be best for making a keyboard shortcut.</explanation>
    </question>
    <question>
        <p>Which keyboard event would we use if we were adding hotkeys to an app?</p>
        <answer><code>keydown</code></answer>
        <answer><code>keypress</code></answer>
        <answer correct><code>keyup</code></answer>
        <explanation>The <code>keyup</code> event would be best for adding hotkeys to an app.</explanation>
    </question>
    <question>
        <p>Which keyboard event would we use if we were building a virtual game direction pad?</p>
        <answer correct><code>keydown</code></answer>
        <answer><code>keypress</code></answer>
        <answer><code>keyup</code></answer>
        <explanation>The <code>keydown</code> event would be best for making a responsive virtual game direction pad.</explanation>
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
