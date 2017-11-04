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
        <answer correct>They are cool.</answer>
        <answer correct>Draw attention to changes on the screen.</answer>
        <answer correct>Draw attention to data leaving the screen.</answer>
        <answer correct>Illustrate the change in category or status of some information.</answer>
        <explanation>All of these are reasons why we should use animations and transitions to enhance our interfaces.</explanation>
    </question>
    <question multiple>
        <p>What are additional methods of improving the structure of our code when refactoring?</p>
        <answer correct>Remove unused and temporary files in the project repository</answer>
        <answer>Improving conditionals so they execute more quickly</answer>
        <answer>Switching to a better library that offers more features for a given component</answer>
        <answer correct>Improving names used to identify elements in the system</answer>
        <answer correct>Removing any commented code or TODO notes</answer>
        <explanation>Remember that refactoring focuses on improving the organization and readability of the code, not improving performance or enhancing features.</explanation>
    </question>
    <question>
        <p>When we "compose" components in Vue.js, what relationship do we create?</p>
        <answer>master/slave</answer>
        <answer correct>parent/child</answer>
        <answer>siblings</answer>
        <answer>worker/agent</answer>
        <explanation>In Vue.js components are "composed" using parent/child relationships.</explanation>
    </question>
    <question>
        <p>In Vue.js, a child component defines the data it needs from the parent component using the _______________ array.</p>
        <answer><code>data</code></answer>
        <answer><code>params</code></answer>
        <answer correct><code>props</code></answer>
        <answer><code>args</code></answer>
        <explanation>Child components define the data they need through the <code>props</code> ("properties") object.</explanation>
    </question>
    <question>
        <p>How can a child component signal to the parent component that some action has taken place?</p>
        <answer>Data syncing</answer>
        <answer>Promises</answer>
        <answer correct>Trigger a custom event</answer>
        <answer>Reactivity</answer>
        <explanation>Child components can trigger a custom event, which can be picked up and handled by the parent component.</explanation>
    </question> 
    <question>
        <p>How can we consolidate common data or functionality used in multiple components in a Vue.js application?</p>
        <answer>Use code snippets in our IDE</answer>
        <answer correct>Abstract data objects and functionality to common files and import those in components where they are needed</answer>
        <answer>Define as a part of the core Vue.js instance</answer>
        <answer>Use Angular</answer>
        <explanation>Common data objects and functionality can be abstracted into common files and imported into components where required.</explanation>
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
