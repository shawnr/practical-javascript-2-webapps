# Quiz: Visual Feedback and Enhancement

Please enjoy this self-check quiz to help you identify key concepts, points, and techniques discussed in this section.

<quiz name="">
    <question>
        <p>The first step towards presenting a compelling visual experience for a user is what?</p>
        <answer>refactoring</answer>
        <answer>custom fonts</answer>
        <answer correct>solid interface design</answer>
        <answer>lots of effects</answer>
        <explanation>All good user experiences rely on solid interface design: proper grouping of information, solid organization, reduced clutter, etc.</explanation>
    </question>
    <question multiple>
        <p>What are two types of messages or notifications that can be used in an application?</p>
        <answer>postal</answer>
        <answer>animated</answer>
        <answer correct>local</answer>
        <answer correct>global</answer>
        <explanation>Messages used in an application are either "local" (attached to a specific element in the DOM) or "global" (generally referencing the entire page content).</explanation>
    </question>
    <question>
        <p>What kind of message is a load throbber?</p>
        <answer>global</answer>
        <answer correct>local</answer>
        <explanation>Load throbbers are usually local messages.</explanation>
    </question>
    <question>
        <p>Errors are not counted as messages in web applications.</p>
        <answer>True</answer>
        <answer correct>False</answer>
        <explanation>False: Errors are just another kind of message, and they can be either local or global.</explanation>
    </question>
    <question multiple>
        <p>What are some reasons for using animations and transitions in our interfaces?</p>
        <answer correct>They are cool</answer>
        <answer correct>Draw attention to changes on the screen</answer>
        <answer correct>Draw attention to data leaving the screen</answer>
        <answer correct>Illustrate the change in category or status of some information</answer>
        <explanation>All of these are reasons why we should use animations and transitions to enhance our interfaces.</explanation>
    </question>
    <question multiple>
        <p>Why would we use bound classes or styles in our interfaces?</p>
        <answer>Animate page transitions</answer>
        <answer correct>Provide a visual response to a change in data</answer>
        <answer correct>Apply different styles depending on data values</answer>
        <answer correct>Apply dynamic data to style properties (such as background images)</answer>
        <answer>Show/hide content</answer>
        <explanation>There are many reasons to use bound classes and styles, but those do not include animating page transitions or showing/hiding content.</explanation>
    </question>
    <question>
        <p>What component do we use in Vue.js to transition a single element?</p>
        <answer><code>App</code></answer>
        <answer><code>router-link</code></answer>
        <answer correct><code>transition</code></answer>
        <answer><code>transition-group</code></answer>
        <explanation>In Vue.js we use the <code>transition</code> component to transition single elements shown with <code>v-if</code>, <code>v-show</code>, or components.</explanation>
    </question>
    <question multiple>
        <p>What extra attributes do <code>transition-group</code> components require to function?</p>
        <answer><code>data</code></answer>
        <answer><code>params</code></answer>
        <answer correct><code>tag</code></answer>
        <answer correct><code>key</code></answer>
        <explanation>The <code>transition-group</code> component requires a <code>tag</code> attribute and each item included for transitioning must have a unique <code>key</code> attribute.</explanation>
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
