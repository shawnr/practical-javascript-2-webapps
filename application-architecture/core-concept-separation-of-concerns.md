# Core Concept: Separation of Concerns
Much of our refactoring work will boil down to upholding the ["separation of concerns"](https://en.wikipedia.org/wiki/Separation_of_concerns)&mdash;the belief that software should be organized into distinct components, each of which handles a single "concern". The goal is to create a "single source" or "authority" on any given feature or data point in our application. This allows us to more easily understand how the application works, and it allows us to isolate changes, which helps prevent us from introducing unexpected bugs in the system.

When we first begin building a project, we cannot be totally sure of what things we will build: We have an idea of the main features we need to build and how we want to build them. But along the way we discover all sorts of smaller elements we must build, configurations that must be available to multiple parts of the application, and data that must be properly stored and managed within the system. 

The more time we spend building on a project, the more we realize opportunities to improve the structure of our application. We might realize that we can regroup components, re-label methods, functions, and variables, or re-organize our files so that everything just makes more sense and works better together. By making sure to separate our concerns, we create single locations for specific functionality or data to live within the system.

Imagine that we have a system that allows us to create blog posts. This might involve managing users of the system, the content of the posts, the media used in posts (such as images, videos, etc.), and much more. Each of these big areas would break apart into major components: users, blog posts, media. Within each of those major components, we can often break things down even further to create subdivisions until will have a nicely organized set of features and data that is organized in a sensible way.

For example, if we wanted to add a new piece of metadata to a user's profile, we would intuitively start looking at the user management components in our software. It would be unexpected to find a user's profile stored as part of the blog post management components. Similarly, it would be more difficult to maintain consistent data or functionality in the system if information about the user were duplicated within the blog post management components. 

Upholding the separation of concerns in our applications earns us several benefits: We can more easily maintain our application because any changes can be isolated to the specific components they affect. We can more easily enhance our project because we know exactly which components are responsible for which functions and we can, again, minimize the opportunity to create unexpected errors in the system. We can also more easily bring on additional collaborators to work with us on projects because our application has a better, more straightforward organization.

Of course, we have been thinking about this topic in very abstract terms so far. Let's take a look at some specific things we can do to enhance the separation of concerns within our applications.

## Encapsulating Logic or Data
Make sure to pull out specific logic into sensible components.

## Breaking Apart Logic
Large methods/functions are difficult to understand. Break them into smaller, specific structures.

## Combining Logic
Too many objects/methods/functions can also be bad. We don't want to lose track of what is related and we do not want to duplicate functionality in different components.