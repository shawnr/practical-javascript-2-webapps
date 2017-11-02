# Core Concept: Visual Feedback

## Interface Design

## Messaging
In web applications, being able to let the user know about changes to the system they are using is a critical aspect of designing a responsive, friendly system. In order to communicate changes that may not be possible to represent more clearly to the user through any other means, we often use "messages". Messages come in many shapes and sizes. The "loading throbber" that we see when loading data in software is a form of message. There are global messages, local messages, and all different styles and conventions of displaying messages. 

Sometimes messages are called "alerts" or "notifications." Sometimes they are called "toast" or "flash" messages. All of these words indicate a slightly different take on the use and approach to displaying messages. There are many ways to accomplish the goal of explicitly informing our user about the state of the system, and in Vue.js we have many different available methods to approach this problem. Before we get too deep into a specific implementation of messages on our website, let's consider some general characteristics of how we use messages in software.

There are many ways to use messaging in websites and apps, and developers are always coming up with clever new ways to indicate changes in content and system status. But a few conventions have grown up around messaging, and it's worthwhile to be aware of these guiding principles.

When generally thinking about messaging, the different varieties can be usefully categorized as one of two types: global and local. These are useful labels, and most software makes use of both types of messages at different times. Understanding when to use which type is important for using messages effectively in our application.

### Global messages
Global messages apply to everything the user is seeing. On Twitter, for example, as we read tweets in our timeline we may notice an alert that shows up at the top of the timeline telling us that there are a number of new tweets available to read. In many email clients, when we receive a new message, or when ew file a message away, we will see an alert at the top of the screen. 

![New tweets!](img/new_tweets.png)
<br>New tweets!

Global messages are great for letting us know that things are happening that generally apply to what we're doing. Depending on how they are presented, they can be more or less effective. For example, the alert pictured above is only visible when we scroll to the top of the page. If we are lower on the page, we will never know how many tweets you have.

### Local messages
Local messages appear closer to "where the action is". This is commonly seen in form field validation, especially when we're filling out more complex forms. In order to indicate where we have gone wrong, messages may be shown very close to the field (or in some way even styled as part of the form field).

Here is an example from Twitter's signup form:

![Twitter signup with error notifications](img/twitter_signup.png)
<br>Twitter signup with error notifications

As we can see in the image above, as we fill in the form the Twitter website is checking to see if our information is valid. It indicates to us clearly if we have successfully filled in the field or if we must change our information. Twitter even goes so far as to suggest alternate usernames based on the data we've filled in when our chosen name is unavailable.

Local messages are also often used in locations where data is being loaded. We often see loading "throbbers" (those spinning or pulsing animated icons that are used to indicates something is happening) in the location where a specific set of data will be loaded. We see these loading indicators in sidebars where related articles will be listed, and we see them in image or video viewers as the media files are loaded. Since our applications tend more and more to be assembled from small components, each of which might make its own request to a remote API server, these location-based loading messages are likely to remain common.

## Meaningful Animations

One of the side-effects of writing highly performant Javascript applications is that when we change the data on the screen it can be difficult for users to notice the alterations. It's not at all uncommon when working with an unstyled app for even developers, bleary eyed from looking closely at code, may miss that a value has changed in a corner of the screen.

In order to make it more evident that changes are happening on the page, we often turn to animation. Humans are very good at noticing even small movements, especially if everything else on a page is generally stationary. We can animate position, size, color, and shape to help us draw attention to whatever we have changed.