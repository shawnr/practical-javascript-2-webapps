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

If we are working in an object oriented environment, we should also consider whether we have defined the proper class objects. Classes are templates for relating data and functionality together. We often create classes to model objects within the system, and we use the methods on the class to perform specific functions. If we're working with classes, then our refactoring will more likely lead to changes in which methods we specify than global functions. Nonetheless, the same concepts of grouping and re-organizing our logic still apply.

### Breaking Apart Logic
Although we have mostly discussed combining logic or data objects to create self-contained data objects or functions, sometimes it is just as important to break apart logic or separate data objects. It becomes much more difficult to understand very long sequences of logical instructions. When reading a lengthy blocks of code, it is easy to lose track of all the names and relationships being created. 

It is preferred to break sequences of logical instructions into their smallest pieces. It's easy to read a function or method with 5-15 lines of code. Beyond that, things become less clear and it's much more difficult to actually parse each line as a reader. However, we often make methods or functions that start out as high-level instructions and refer to more and more detailed methods or functions.

For example, it is possible to imagine writing a game where we need to initialize a game board for the players. If we imagine we have a `game` class defined, we might begin with a lengthy `setUpGame` method:

```js
setUpGame: function(){
    // Clear existing board/content
    // Reset score
    // Gather player input for player names & tokens
    // Create a new board
    // Place pieces on board
    // Randomly select which player goes first
    // Initiate first move
}
```
In the example above, we see a list of comments representing each of the major tasks that needs to be completed. But for each of these tasks there might be several lines of code required to accomplish the goal. This method could easily balloon to 50 or more lines of code, which would make it difficult to read through and understand. 

Rather than writing each line of code, it would be better to write a series of statements that call other methods to perform each specific task:

```js
setUpGame: function(){
    // Clear existing board/content
    this.clearBoard();
    // Reset score
    this.resetScore();
    // Gather player input for player names & tokens
    this.setUpPlayers();
    // Create a new board
    this.createBoard();
    // Place pieces on board
    this.placePieces();
    // Randomly select which player goes first
    this.coinToss();
    // Initiate first move
    this.firstMove();
}
```
In this updated version, we can see that this method has become a list of other methods that must be invoked. In each one of these other methods, there can be some combination of specific instructions and calls to other methods. A developer might need to trace functionality through several other components to really get the full sense of the application.

It might seem difficult and unnecessary to separate the actual lines of code that do the work out of this method. However, there are some clear advantages. We've already discussed the fact that reading lengthy sequences of code is difficult. But there are other advantages, too.

When we move functionality out into discrete components, we can more easily modify the application. In this case, if we altered the way the score worked we would only need to update those methods directly responsible for managing scores. Likewise, if we altered the way boards are drawn (perhaps to allow user-generated game boards), then we would only need to modify lines of code in the `createBoard` method. This allows us to make those changes with minimal risk of inadvertently altering the way the `setUpGame` method works. If we find a bug in the coin toss, we do not need to wonder if it is caused by code surrounding it in the `setUpGame` method; instead, we can focus our investigation in the `coinToss` method.

We also create a modularity that allows the use of features in all the situations where we need to use them. For example, there may be other times when we need to perform a virtual coin toss. If we have separated that logic out into a standalone method, then we can use the coin toss feature whenever we wish. The ability to combine game logic in unique and interesting ways is a hallmark of what makes software games engaging.

## Encapsulating Logic or Data
We might remember from previous experience with object oriented programming that "encapsulation" is often described as "information hiding." This seems like an odd concept: Why would we want to hide information from developers or users? But the reason this is done is to create a better "interface." All of our logic and data constitutes the interface of our system, and as developers we are often more concerned with the interface a system presents than the actual inner workings of the code. 

There is an old analogy of driving an automobile: We can get into a car and learn to use the steering wheel, gas, brake, gear shift, etc. We do not need to be able to build a vehicle of our own, and we do not need to know exactly how our car works. Understanding the interface allows us to gain the value of using a car while the inner workings of the vehicle remain hidden from us.

The information hiding concept extends to managing how we access the deep functions of a system. Encapsulation allows us to control access to data properties or features that might not be "safe" to access directly. This often is used to allow developers to provide validation checks to make sure nothing is going to break the system.

In the vehicle analogy, this would be like systems to automatically slow us down or sound an alarm when an obstacle is detected. Although it feels like pushing the gas is directly engaging the vehicle to go forward, this input is actually being interpreted and applied through a buffer of features that are designed to prevent us from making a catastrophic mistake.

In the coding world, this is often much more mundane. We use "getters" and "setters" to allow a developer to access and save data with the benefit of data validation, clean-up, and coordination. We also use private methods and properties to make features work "behind the scenes" to provide a better developer and/or user experience.

Here is an example using a `Course` class that might exist in a learning management system:

```js
class Course {
    constructor (subjectCode, number, name, description) {
        this.subjectCode = subjectCode;
        this.number = number;
        this.name = name;
        this.description = description;
    }
    get title () {
        return `${ this.subjectCode } ${ this.number }&mdash;${ this.name }`;
    }
}
```
Given this class definition for a `Course`, we could use it in this way:

```js
let myCourse = new Course('WATS', 4000, 'Building JS Web Apps', 'Some longer description');
console.log( myCourse.title );
// Prints in console: WATS 4000: Building JS Web Apps
```
In this case, rather than asking developers to constantly string together the subject code, course number, and course name to create the full display title, this functionality is provided as a getter and the developer is able to use the `Course` object without risking as many errors. This is a somewhat mundane example, but additional logic can be provided on getters and setters to enforce data validation rules, process requirements, and other necessary logic.

<div class="tip-box">
    <h3>Avoiding Complications</h3>
    <p>There is a difference between "complex" and "complicated." Many of the systems we deal with when creating software become _complex_ because they require the coordination of many data points or the use of very specific software tools or design patterns. We live in a complex world, so making software that is useful to us will necessarily be complex. Whenever we must deal with many details or components, the task will be complex.</p>
    <p>Complication, however, arises from interactions with things that are non-essential (even if they are unavoidable). When recovering from a medical procedure, for example, we talk about "complications" as thing that will make it more difficult to achieve the goal of healing. Complications are things that prevent us from proceeding as we intend, and we generally hope to avoid them. If we find it difficult to explain the changes we've made then we might have gone too far in revising the structure of our application.</p>
</div>

## Concerning Separations
It's important to remember that we do not so much "create" abstractions or separations of concerns in our applications. Rather, we recognize when we have opportunities to enhance the separation of concerns in our software, or to enhance our system by introducing an abstraction. Any of the techniques mentioned above can be used to do harm to a project as well as doing good. The process of refactoring is not without its own risks. By thinking rationally about our projects and always keeping vigilant for ways to improve the organization of our logic and data we can move towards continuous enhancements.













