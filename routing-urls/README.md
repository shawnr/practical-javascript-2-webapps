# Routing and URLs

Within any website or web-based application, we use URLs to indicate different "locations" in our sites. Of course, these aren't really "locations" so much as they are "states" or "views" into our data. Still, the metaphor of the web is that things are "located" somewhere and we "go" there. This is the dominant metaphor we use when setting up URls for our single page applications.

There are many situations where we want our users to share content, or we wish to direct a user to a specific feature of our sites. Users still bookmark pages so they can return to specific content or functionality. To make all of this possible, we must have some URLs that indicate different parts of our web-based software. When we go to `/profile/` we expect to see our Profile page. When we go to `/posts/` we expect to see some posts.

Throughout this section we will learn to use the `vue-router` module to add URLs to our Vue.js applications and navigate our user through our entire website. Users will be able to bookmark specific parts of our site and share links to specific content.