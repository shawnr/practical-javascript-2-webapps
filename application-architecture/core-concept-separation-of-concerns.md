# Core Concept: Separation of Concerns
Much of our refactoring work will boil down to upholding the ["separation of concerns"](https://en.wikipedia.org/wiki/Separation_of_concerns)&mdash;the belief that software should be organized into distinct components, each of which handles a single "concern". The goal is to create a "single source" or "authority" on any given feature or data point in our application. This allows us to more easily understand how the application works, and it allows us to isolate changes, which helps prevent us from introducing unexpected bugs in the system.

When we first begin building a project, we cannot be totally sure of what things we will build: We have an idea of the main features we need to build and how we want to build them. But along the way we discover all sorts of smaller elements we must build, configurations that must be available to multiple parts of the application, and data that must be properly stored and managed within the system. 

The more time we spend building on a project, the more we realize opportunities to improve the structure of our application. We might realize that we can regroup components, re-label methods, functions, and variables, or re-organize our files so that everything just makes more sense and works better together. By making sure to separate our concerns, we create single locations for specific functionality or data to live within the system.

Imagine that we have a system that allows us to create blog posts. This might involve managing users of the system, the content of the posts, the media used in posts (such as images, videos, etc.), and much more. Each of these big areas would break apart into major components: users, blog posts, media. Within each of those major components, we can often break things down even further to create subdivisions until will have a nicely organized set of features and data that is organized in a sensible way.

For example, if we wanted to add a new piece of metadata to a user's profile, we would intuitively start looking at the user management components in our software. It would be unexpected to find a user's profile stored as part of the blog post management components. Similarly, it would be more difficult to maintain consistent data or functionality in the system if information about the user were duplicated within the blog post management components. 

Upholding the separation of concerns in our applications earns us several benefits: We can more easily maintain our application because any changes can be isolated to the specific components they affect. We can more easily enhance our project because we know exactly which components are responsible for which functions and we can, again, minimize the opportunity to create unexpected errors in the system. We can also more easily bring on additional collaborators to work with us on projects because our application has a better, more straightforward organization.

Of course, we have been thinking about this topic in very abstract terms so far. Let's take a look at some specific things we can do to enhance the separation of concerns within our applications.

## Re-Grouping Components or Data
When we begin developing a piece of software, we care most about getting things working. We will use one-off variables, write convoluted conditionals, line after line of logical statements, and generally bend over backwards to get things going. That is absolutely the correct approach when we begin a project and we should not hesitate to prioritize progress over elegance. However, at some point we accumulate a lot of messy code, and this is when refactoring can help.

One thing we often notice when looking at the code we wrote to get a project up and running is how much we repeat ourselves and how often we create data as separate objects that would be better connected. When we notice these tendencies in our code, that is a great indicator that we have an opportunity to re-group, better organize, and possibly create more meaningful abstractions in our code.

### Consolidate Data
It's common to begin with a specific variable named for each data point we use in our code. We might use `username`, `userEmail`, `userFirstName`, and `userLastName` as individual variables when we first create our project. As we evolve our code, it often makes sense to define each of these as properties of a larger object:

```js
let user = {
    'username': 'jdoe',
    'email': 'jdoe@example.com',
    'firstName': 'Jane',
    'lastName': 'Doe'
}
```
In this revised data structure it's easier to see all of the different properties of the `user` that are required in the system. When referring to data about the user, we can know that all the information is contained in this single object.

This process of moving data or functionality to more structured objects is often known as "abstraction". Abstraction allows us to create a "model" or "template" of how the data and functions for a given object or concept relate. In this case, we have "abstracted" all of the user data into the `user` object, which now provides a better way to group and show that these data points are all related. Anytime we have the `user` object, we can easily discover where to find all of the data about the user, and that data can be easily used as a package.

During the process of refactoring, we will often perform this consolidation and abstraction of data and features several times. When applied to the functionality of the system, abstraction often results in new or altered logical structures, such as functions, classes, and methods.

### Convert Repetitive Logic into Functions/Methods
Sometimes we find ourselves writing the same lines of code in multiple places within our application. Even when this is only a few lines of code, it can add up dramatically over time. This is problematic because we spend time writing code that is really not needed, and we also create the potential to make more significant mistakes when we change something later.

As an example, imagine that we have a system that outputs dates in several locations. We might define a couple of constants at the beginning of our app to store the month and day names, but then we would use them wherever we need to output a date:

```js
const months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'];
const weekdays = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
```
Wherever we want to output a date, we might have these lines repeated:

```js
let weekday = date.getDay();
let daynum = date.getDate();
let month = date.getMonth();
let year = date.getFullYear();

let fullDate = `${ weekdays[weekday] } ${ months[month] } ${ daynum }, ${ year }`;
```
This could work, and there's no shame in writing this when first starting on a project, but eventually we want to clean up the repetition and create a single, authoritative mechanism for formatting dates in our application. To this end, we could create a helpful function like this:

```js
function formatDate(date){
    const months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'];
    const weekdays = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];

    let weekday = date.getDay();
    let daynum = date.getDate();
    let month = date.getMonth();
    let year = date.getFullYear();

    return `${ weekdays[weekday] } ${ months[month] } ${ daynum }, ${ year }`;
}
```
In this example, we have isolated all of the logic and data used to format a date within the `formatDate` function. This function will execute the same way each time we call it, so we can replace the several lines of formatting the date with a single line:

```js
let fullDate = formatDate(date);
```
This saves us from repetitive typing, and it also gathers everything we would use to format dates. There is no chance that if we change the way we want our dates formatted we will miss one case that results in a bad experience for the user. This also opens the door for making more complex date formats in the future because we can focus on writing the best logic for date formatting in this single location within our system.

## Encapsulating Logic or Data
Make sure to pull out specific logic into sensible components.

## Breaking Apart Logic
Large methods/functions are difficult to understand. Break them into smaller, specific structures.

## Combining Logic
Too many objects/methods/functions can also be bad. We don't want to lose track of what is related and we do not want to duplicate functionality in different components.













