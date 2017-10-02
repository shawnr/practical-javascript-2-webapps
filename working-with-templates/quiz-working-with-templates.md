# Quiz: Working with Templates

Please enjoy this self-check quiz to help you identify key concepts, points, and techniques discussed in this section.

<quiz name="">
    <question>
        <p>A tool used for processing and rendering templates is called what?</p>
        <answer>template processor</answer>
        <answer>HTML factory</answer>
        <answer correct>template engine</answer>
        <answer>code generator</answer>
        <explanation>We use template engines to process and render template files in application frameworks.</explanation>
    </question>
    <question>
        <p>What do we call the set of variables, objects, methods, and other information available to a template when it is being rendered?</p>
        <answer>template data</answer>
        <answer correct>template context</answer>
        <answer>template scope</answer>
        <answer>template worldview</answer>
        <explanation>The "template context" describes all of the information available to a template when it is being rendered.</explanation>
    </question>
    <question>
        <p>What do we call the double curly brace syntax used to output data in the Vue.js templating engine?</p>
        <answer>handlebars syntax</answer>
        <answer>ripple syntax</answer>
        <answer correct>mustache syntax</answer>
        <answer>braces syntax</answer>
        <explanation>The double curly brace syntax is also known as "mustache syntax."</explanation>
    </question>
    <question multiple>
        <p>Which of the following are features commonly found in templating engines?</p>
        <answer correct>looping</answer>
        <answer correct>data interpolation</answer>
        <answer>automatic accessibility checking</answer>
        <answer correct>conditionals</answer>
        <explanation>Looping, data interpolation, and conditionals are three core technologies provided by virtually all templating engines.</explanation>
    </question>
    <question>
        <p>Which directive should we use to output HTML from a variable in our template context?</p>
        <answer><code>v-if</code></answer>
        <answer><code>v-for</code></answer>
        <answer><code>v-bind</code></answer>
        <answer correct><code>v-html</code></answer>
        <explanation>The <code>v-html</code> directive will output safe HTML tags in a template maintaining the HTML formatting of the data.</explanation>
    </question>
    <question>
        <p>What is the result of "two-way data binding" in Vue.js templates?</p>
        <answer>The data is constrained into a small area.</answer>
        <answer correct>The data is updated in the template when it is updated by the logic of the system.</answer>
        <answer>The data must be manually updated to update the template display.</answer>
        <answer>The data cannot go anywhere after it is output to the template.</answer>
        <explanation>Two-way data binding refers to the way the data is updated in the template when it is updated by the logic of the system.</explanation>
    </question>
    <question>
        <p>Which directive would be used to bind an HTML attribute to a variable in the template context?</p>
        <answer><code>v-if</code></answer>
        <answer><code>v-for</code></answer>
        <answer correct><code>v-bind</code></answer>
        <answer><code>v-html</code></answer>
        <explanation>The <code>v-bind</code> directive is used to bind an HTML attribute to a variable in the template context.</explanation>
    </question>
    <question>
        <p>What do Vue.js Directives look like when used in a template?</p>
        <answer correct>HTML attributes</answer>
        <answer>data output</answer>
        <answer>form fields</answer>
        <answer>bunnies</answer>
        <explanation>Vue.js Directives look like HTML attributes when used in a template.</explanation>
    </question>
    <question multiple>
        <p>Which directives would be useful if we needed to show/hide content on a page?</p>
        <answer correct><code>v-if</code></answer>
        <answer><code>v-hide</code></answer>
        <answer><code>v-bind</code></answer>
        <answer correct><code>v-show</code></answer>
        <explanation>The <code>v-if</code> and <code>v-show</code> directives can be used to show/hide content in a template.</explanation>
    </question>
    <question multiple>
        <p>Which of the following are reasons why we might use a computed value in our templates?</p>
        <answer correct>Annotate data with additional information.</answer>
        <answer correct>Format data to match our requirements.</answer>
        <answer correct>Combine data points into more useful labels</answer>
        <explanation>All of the above are reasons we might use a computed value in our template.</explanation>
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
