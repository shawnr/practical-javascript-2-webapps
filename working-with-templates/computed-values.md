# Computed Values

So far we have supplied essentially static data to our components and templates. The data defined in the template context can be changed through user interaction or other actions in our application. But we do not have a way to provide proper, reactive data that is based on a computation.

There are often situations where we want to compute a value based on the other data in the system: Calculating subtotal, tax, and total, providing additional annotation to information based on data values, or combining multiple data points into a more descriptive label, to name a few possible cases. The computed data in each of these examples would be valuable to users, so it's useful to calculate the information on the fly.

It's also possible that we need to reveal some other information that should be calculated at the time the user accesses the application, such as the date/time a function was initiated, the viewport size, or the scroll position of the window. In these cases, it is worthwhile to compute the data and use the computed value to display the information to the user.

## Using Computed Values

To create a computed value, we will add a `computed` property to our component object. Here is an example imagining a weather component.

```html
<script>
export default {
  name: 'weather',
  data () {
    return {
      forecast: {
        high: "65",
        low: "48", 
        rainChance: "67"
    }
  },
  computed: {
    umbrellaTip: function(){
      if (this.forecast.rainChance >= 70) {
        return "Bring an umbrella for sure!";
      } else if ((this.forecast.rainChance > 40) && (this.forecast.rainChance < 70)){
        return "Probably a good idea to bring an umbrella, just in case.";
      } else {
        return "No umbrella needed today.";
      }
    }
  }
}
</script>
```
In this example, the data includes a `forecast` object, which has some weather information in it. The information includes a property called `rainChance`, which is the percentage chance of rain (67% in this example).

We can compute the `umbrellaTip` using the `this.forecast.rainChance` value. We provide three levels of `umbrellaTip`, and we can output this value to the template using the normal data reference syntax:

```html
<p>{{ umbrellaTip }}</p>
```

This line in the template would output the following HTML:

```html
<p>Probably a good idea to bring an umbrella, just in case.</p>
```

If the value of `forecast.rainChance` were to change, the value of `umbrellaTip` would automatically be updated because the `forecast` object is part of the data used in this template, and it is reactive. We could define multiple computed properties, and each would involve defining a function to calculate the computed value.

Here is another example where we use computed values to calculate the tax and total for a customer:

**logic**
```html
<script>
export default {
  name: 'checkout',
  data () {
    return {
      subtotal: 45,
      taxRate: 0.04
    },
  computed: {
    tax: function(){
      return (this.subtotal * this.taxRate).toFixed(2);
    },
    total: function(){
      return this.subtotal + this.tax;
    },
    timestamp: function(){
      return Date.now();
    }
  }
}
</script>
```

**template**
```html
<ul>
  <li>Time: {{ timestamp }}</li>
  <li>Subtotal: ${{ subtotal }}</li>
  <li>Tax: ${{ tax }}</li>
  <li>Total: ${{ total }}</li>
</ul>
```

**rendered template**
```html
<ul>
  <li>Time: 1506979771129</li>
  <li>Subtotal: $45</li>
  <li>Tax: $1.80</li>
  <li>Total: $46.80</li>
</ul>
```

In this example, we have several computed values. The first is the `tax` value, which calculates the amount of tax using `this.subtotal` and `this.taxRate`. The second computed value is `total`, which adds the `this.tax` amount to the `this.subtotal`. Finally, we have the `timestamp`, which is based on the built-in JavaScript function `Date.now()`. 

Since `tax` and `total` are based on reactive values, when the `subtotal` and/or `taxRate` values change the computed `tax` and `total` values would also be updated. However, since the `timestamp` value is based on the non-reactive `Date.now()` value, the value of `timestamp` would not be updated when data is changed.

## Computed Strategies
Computed values are powerful tools we can use to help our templates be more easily readable and to give us exactly the output we want. Here are some common use cases for when computed values might be a good idea:

* Annotating data with additional information (such as an "umbrella tip" or other advisory)
* Formatting data to match specific HTML or textual patterns (such as adding a "&deg;F" to the temperature)
* Combining data points into more useful labels (such as showing names in a "Last Name, First Name" display)

There are probably lots of other use cases we will discover as we work through the challenges of building applications. We will continue to learn more ways to affect the data we display to the user in upcoming sections, too. But for now, computed values gives us a way to do a lot of interesting data manipulation.













