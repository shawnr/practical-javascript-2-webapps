# Quiz: Handling User Input

Please enjoy this self-check quiz to help you identify key concepts, points, and techniques discussed in this section.

<quiz name="">
    <question>
        <p>What is the <code>action</code> property of a form provide?</p>
        <answer>the name of the method used to handle the form</answer>
        <answer correct>the URL where the form should be submitted (and browser redirected)</answer>
        <answer>the name of the variable used</answer>
        <answer>the time the form was generated</answer>
        <explanation>The <code>action</code> property refers to the URL where the form should be submitted (and browser redirected).</explanation>
    </question>
    <question multiple>
        <p>What <code>methods</code> can be used to submit a form online?</p>
        <answer>snailmail</answer>
        <answer correct>post</answer>
        <answer correct>get</answer>
        <answer>receive</answer>
        <explanation>The <code>post</code> and <code>get</code> methods are used to submit forms online.</explanation>
    </question>
    <question>
        <p>Which directive do we use to connect an input field and a value in the component's data?</p>
        <answer><code>v-bind</code></answer>
        <answer correct><code>v-model</code></answer>
        <answer><code>v-if</code></answer>
        <answer><code>v-on</code></answer>
        <explanation>The <code>v-model</code> directive is used to bind an input field and the value in the component's data.</explanation>
    </question>
    <question multiple>
        <p>Which of the following modifiers are provided to help handle data in form fields?</p>
        <answer><code>.active</code></answer>
        <answer correct><code>.lazy</code></answer>
        <answer correct><code>.number</code></answer>
        <answer correct><code>.trim</code></answer>
        <explanation>The <code>.lazy</code>, <code>.number</code>, and <code>.trim</code> modifiers are provided to help handle data in form fields.</explanation>
    </question>
    <question>
        <p>What should we always include in at the beginning of set of <code><option></code> elements in a <code><select></code> tag?</p>
        <answer>A welcome statement.</answer>
        <answer>A comment explaining what we're selecting.</answer>
        <answer correct>A dummy choice that is disabled so the user is forced to select a different option.</answer>
        <answer>The default option.</answer>
        <explanation>Providing a dummy choice as the default option in a <code><select></code> element insures data will be bound and synced properly.</explanation>
    </question>
    <question>
        <p>Which directive defines an event listener in Vue.js templates?</p>
        <answer><code>v-if</code></answer>
        <answer><code>v-for</code></answer>
        <answer correct><code>v-on</code></answer>
        <answer><code>v-model</code></answer>
        <explanation>The <code>v-on</code> directive is used to define an event listener in a Vue.js template.</explanation>
    </question>
    <question multiple>
        <p>What events can be listened for in a Vue.js application?</p>
        <answer correct><code>click</code> and <code>submit</code></answer>
        <answer correct>Events emitted by an HTML element</answer>
        <answer correct>Custom events defined by the developer</answer>
        <answer>Cool concerts nearby</answer>
        <explanation>The <code>v-on</code> directive can listen for any event emitted by an HTML element or custom events created by developers.</explanation>
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
