# Core Concept: Separation of Concerns
Much of our refactoring work will boil down to upholding the ["separation of concerns"](https://en.wikipedia.org/wiki/Separation_of_concerns)&mdash;the belief that software should be organized into distinct components, each of which handles a single "concern".

## Encapsulating Logic or Data
Make sure to pull out specific logic into sensible components.

## Breaking Apart Logic
Large methods/functions are difficult to understand. Break them into smaller, specific structures.

## Combining Logic
Too many objects/methods/functions can also be bad. We don't want to lose track of what is related and we do not want to duplicate functionality in different components.