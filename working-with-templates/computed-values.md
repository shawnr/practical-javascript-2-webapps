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
  <li>Subtotal: {{ subtotal }}</li>
  <li>Tax: {{ tax }}</li>
  <li>Total: {{ total }}</li>
</ul>
```

**rendered template**
```html
<ul>
  <li>Hello, world!</li>
  <li>42 is the meaning of life.</li>
  <li>Question authority.</li>
</ul>
```














