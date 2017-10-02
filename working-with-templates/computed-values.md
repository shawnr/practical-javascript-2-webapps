# Computed Values

So far we have supplied essentially static data to our components and templates. The data defined in the template context can be changed through user interaction or other actions in our application. But we do not have a way to provide proper, reactive data that is based on a computation.

There are often situations where we want to compute a value based on the other data in the system: Calculating subtotal, tax, and total, providing additional annotation to information based on data values, or combining multiple data points into a more descriptive label, to name a few possible cases. The computed data in each of these examples would be valuable to users, so it's useful to calculate the information on the fly.

It's also possible that we need to reveal some other information that should be calculated at the time the user accesses the application, such as the date/time a function was initiated, the viewport size, or the scroll position of the window. In these cases, it is worthwhile to compute the data and use the computed value to display the information to the user.

## Creating Computed Values

To create a computed value, we will add a `computed` property to our component object. Here is an example imagining a weather component.

