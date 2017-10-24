# Core Concept: Separation of Concerns
Much of our refactoring work will boil down to upholding the ["separation of concerns"](https://en.wikipedia.org/wiki/Separation_of_concerns)&mdash;the belief that software should be organized into distinct components, each of which handles a single "concern". The goal is to create a "single source" or "authority" on any given feature or data point in our application. This allows us to more easily understand how the application works, and it allows us to isolate changes, which helps prevent us from introducing unexpected bugs in the system.

When we first begin building a project, we cannot be totally sure of what things we will build: We have an idea of the main features we need to build and how we want to build them. But along the way we discover all sorts of smaller elements we must build, configurations that must be available to multiple parts of the application, and data that must be properly stored and managed within the system. 

The more time we spend building on a project, the more we realize opportunities to improve the structure of our application. We might realize that we can regroup components, re-label 

## Encapsulating Logic or Data
Make sure to pull out specific logic into sensible components.

## Breaking Apart Logic
Large methods/functions are difficult to understand. Break them into smaller, specific structures.

## Combining Logic
Too many objects/methods/functions can also be bad. We don't want to lose track of what is related and we do not want to duplicate functionality in different components.