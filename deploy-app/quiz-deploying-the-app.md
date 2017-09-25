# Quiz: Deploying the App

Please enjoy this self-check quiz to help you identify key concepts, points, and techniques discussed in this section.

<quiz name="">
    <question>
        <p>What tool are we using to build and process our source files for deployment?</p>
        <answer>Browserify</answer>
        <answer>Gulp</answer>
        <answer>NPM</answer>
        <answer correct>Webpack</answer>
        <explanation>We are using Webpack to configure the build and processing of our site files.</explanation>
    </question>
    <question multiple>
        <p>Which are processes that CSS and JS undergo to become smaller?</p>
        <answer>shrinkage</answer>
        <answer correct>minification</answer>
        <answer correct>uglification</answer>
        <answer>compacting</answer>
        <explanation>Minification and ugilification are two processes used to shrink JS and CSS.</explanation>
    </question>
    <question>
        <p>File versioning (adding a timestamp to the filename) helps with what problem?</p>
        <answer correct>User's browsers caching files that we've changed.</answer>
        <answer>Servers having old data.</answer>
        <answer>Math errors.</answer>
        <answer>Syncing API calls.</answer>
        <explanation>File versioning keeps filenames unique when they are changed in order to prevent user's browsers from caching files that we have altered.</explanation>
    </question>
    <question multiple>
        <p>Which of the following are deployment-related technologies?</p>
        <answer correct>Salt Stack</answer>
        <answer correct>Ansible</answer>
        <answer>BoxingDay</answer>
        <answer correct>Docker</answer>
        <explanation>Only "BoxingDay" is made up. The others are all popular deployment-related tools.</explanation>
    </question>
    <question>
        <p>What command do we use to build our Vue.js applications for deployment?</p>
        <answer><code>build site</code></answer>
        <answer correct><code>npm run build</code></answer>
        <answer><code>npm run dev</code></answer>
        <answer><code>webpack go</code></answer>
        <explanation>We use the <code>npm run build</code> command to build our Vue.js applications for deployment.</explanation>
    </question>
    <question>
        <p>How do we actually deploy our code?</p>
        <answer>Run <code>npm run deploy</code>.</answer>
        <answer correct>Commit the <code>docs/</code> directory and push to <code>origin</code>.</answer>
        <answer>Copy to a flash drive and mail to server.</answer>
        <answer>Run <code>webpack go</code>.</answer>
        <explanation>To deploy our project to Github Pages we only need to commit the updated <code>docs/</code> directory and then push the changes to Github.</explanation>
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
