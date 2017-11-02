# Core Concept: Visual Feedback

## Interface Design

## Messaging
In web applications, being able to let the user know about changes to the system they are using is a critical aspect of designing a responsive, friendly system. In order to communicate changes that may not be possible to represent more clearly to the user through any other means, we often use "messages". Messages come in many shapes and sizes. The "loading throbber" that we see when loading data in software is a form of message. There are global messages, local messages, and all different styles and conventions of displaying messages. 

Sometimes messages are called "alerts" or "notifications." Sometimes they are called "toast" or "flash" messages. All of these words indicate a slightly different take on the use and approach to displaying messages. There are many ways to accomplish the goal of explicitly informing our user about the state of the system, and in Vue.js we have many different available methods to approach this problem. Before we get too deep into a specific implementation of messages on our website, let's consider some general characteristics of how we use messages in software.

## The basics of messaging in websites and apps
There are many ways to use messaging in websites and apps, and developers are always coming up with clever new ways to indicate changes in content and system status. But a few conventions have grown up around messaging, and for our purposes here we are not going to "reinvent" messages.

When generally thinking about messaging, there are two major types of messages: global and local. These are both useful types of messages and most apps and sites make use of both of them. Understanding when to use which type of message is important to getting messaging right in your application.

### Global messages
Global messages apply to everything the user is seeing. On Twitter, for example, as you read tweets in your timeline you may notice an alert that shows up at the top of your timeline telling you that there are a number of new tweets available to read. In many email clients, when you receive a new message, or when you file a message away, you will see an alert at the top of the screen. 

![New tweets!](img/new_tweets.png)

Global messages are great for letting us know that things are happening that generally apply to what we're doing. Depending on how they are presented, they can be more or less effective. For example, the alert pictured above is only visible when you scroll to the top of the page. If you are lower on the page you will never know how many tweets you have.

### Local messages
Local messages appear closer to "where the action is". This is commonly seen in form field validation, especially when we're filling out more complex forms. In order to indicate where we have gone wrong, messages may be shown very close to the field (or in some way even styled as part of the form field).

Here is an example from Twitter's signup form:

![Twitter signup with error notifications](img/twitter_signup.png)

As you can see in the image above, as you fill in the form the Twitter website is checking to see if your information is valid. It indicates to you clearly if you have successfully filled in the field or if you must change your information. Twitter even goes so far as to suggest alternate usernames based on the data you've filled in when your chosen name is unavailable.

## Meaningful Animations

One of the side-effects of writing highly performant Javascript applications is that when we change the data on the screen it can be difficult for users to notice the alterations. It's not at all uncommon when working with an unstyled app for even developers, bleary eyed from looking closely at code, may miss that a value has changed in a corner of the screen.

In order to make it more evident that changes are happening on the page, we often turn to animation. Humans are very good at noticing even small movements, especially if everything else on a page is generally stationary. We can animate position, size, color, and shape to help us draw attention to whatever we have changed.