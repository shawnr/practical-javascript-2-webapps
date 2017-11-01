# Quiz: Application Architecture

Please enjoy this self-check quiz to help you identify key concepts, points, and techniques discussed in this section.

<quiz name="">
    <question>
        <p>What do we call the process of re-structuring code without altering functionality?</p>
        <answer>revisions</answer>
        <answer>code review</answer>
        <answer correct>refactoring</answer>
        <answer>abstraction</answer>
        <explanation>Refactoring is the process of re-structuring code without altering functionality.</explanation>
    </question>
    <question multiple>
        <p>Which of the following are goals for refactoring?</p>
        <answer correct>improve code readability for developers</answer>
        <answer correct>consolidate repetitive code blocks</answer>
        <answer>improve performance</answer>
        <answer correct>maintain a separation of concerns</answer>
        <explanation>All of these are goals for refactoring except improving performance (which would be considered an enhancement of the codebase).</explanation>
    </question>
    <question>
        <p>What can we do to organize related data values in our software?</p>
        <answer>Name each variable with the same prefix (<code>prefix_valueName</code>).</answer>
        <answer correct>Combine variables into a single object.</answer>
        <answer>Put values in a Node module.</answer>
        <answer>Fetch values from an API.</answer>
        <explanation>JS Objects are well-suited for relating multiple data values.</explanation>
    </question>
    <question>
        <p>Longer blocks of code are prone to more errors and make it more difficult for developers to understand what is happening in a program.</p>
        <answer correct>True</answer>
        <answer>False</answer>
        <explanation>True: We prefer shorter blocks of code that can be more easily understood and debugged.</explanation>
    </question>
    <question multiple>
        <p>What are two structures that can be used to break apart lengthy code sequences into smaller components?</p>
        <answer>Array</answer>
        <answer correct>Function</answer>
        <answer correct>Method</answer>
        <answer>Conditional</answer>
        <explanation>Break apart lengthy code sequences by breaking them into functions and/or methods that can be referenced instead.</explanation>
    </question>
    <question multiple>
        <p>What are some of the advantages of encapsulation?</p>
        <answer>Easier to swallow the code.</answer>
        <answer correct>Information hiding allows us to present a more friendly interface to the developer</answer>
        <answer correct>We gain the ability to enforce validation or optimization processes when getting or setting information</answer>
        <answer>Other developers will think we are more professional</answer>
        <explanation>Encapsulation affords us the ability to hide information in order to present a more friendly interface for the developer, and it gives us points where we can more easily insert processes for validation and optimization of data.</explanation>
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
