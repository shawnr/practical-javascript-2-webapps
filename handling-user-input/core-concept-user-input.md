# Core Concept: Forms and User Input

In order to get the most out of the form abilities in Vue.js, it's crucial to understand what forms do and how they work in the context of a modern JavaScript application. In this section we will cover the basics of the default form elements in HTML and how they are used. We will also look briefly at how we detect user actions with events, especially events related to form submission and input changes.

## How Forms Work
As a quick review of how we use forms in HTML, let's take a quick look at the fundamentals of how forms work. It's worthwhile to consult additional resources if this is not something we have a lot of experience with at this point. The Mozilla Developers Network has a great [Introduction to Forms](https://developer.mozilla.org/en-US/docs/Learn/HTML/Forms) in their Learn Web Development series.

Forms are defined with the `<form>` element. Any HTML between the opening and closing `<form>` tags is part of the form itself, and whatever fields are defined between those tags are included as part of the data payload when the form is submitted.

### Form Attributes
On each `<form>` element we can specify certain attributes. The following attributes are the most commonly used:

* `action` &mdash; This attribute specifies a URL that the form is submitted to. When the user submits the form, the browser will pass the form data to the specified `action` URL and the user will be directed to that URL at the same time. This has the effect of moving the user to a different page where the data is usually processed and a response is generated. In JavaScript applications, we often do not use the `action` attribute because the form will be processed by the JavaScript without redirecting the user to another URL.
* `method` &mdash; The form's `method` specifies how the data will be packaged when the form is submitted. The two possible values for `method` are `post` and `get`. Values sent with the `post` method are packaged as part of the HTTP request, and they are not directly visible to the user. Values sent with the `get` method are encoded into the URL as query string variables, and they are directly visible to the user.
* `enctype` &mdash; The `enctype` determines how the data will be encoded; it is short for "encoding type." The default value if unspecified is `application/x-www-form-urlencoded`. If we are submitting files with our form (using the `input` type of `file`), we must change the `enctype` to `multipart/form-data` so that the file data can be properly packaged. 

There are [other form attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form) available, but these are the most commonly seen. A common form declaration might look like this:

```html
<form action="/login/" method="post">
    <label>Username <input type="text" name="username" tabindex="0"></label>
    <label>Password <input type="password" name="password" tabindex="0"></label>
    <input type="submit" value="Login">
</form>
```

In the example above we can see a sample login form. The `action` property is set to a URL that will handle a login, and the method is `post` because we don't want to expose the username or password.

### Form Layout
In order to help with readability and styling of forms, there are a couple of HTML elements that are meant for organizing fields in a form. These tags can be used to create visually separated sets of fields in the HTML page, and they can be styled to achieve whatever visual presentation is desired. 

The [`<fieldset>` element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset) defines an area in the form. It is meant to be wrapped around a group of fields, and it can be used to style or disable/enable those fields in bulk. Fieldsets are often augmented by the `<legend>` element. This element defines a caption that is shown as part of the fieldset and is meant to help users understand the purpose of the grouping. The legend serves a purpose similar to labels on individual fields.

Here is an example of a fieldset:

```html
<form action="/profile/update/" method="post">
    <fieldset>
        <legend>Personal Information</legend>
        <p><label>Salutation <input type="text" name="salutation" tabindex="0"></label></p>
        <p><label>First Name <input type="text" name="firstname" tabindex="0"></label></p>
        <p><label>Family Name <input type="text" name="familyname" tabindex="0"></label></p>
    </fieldset>
    <fieldset>
        <legend>Address</legend>
        <p><label>Street 1 <input type="text" name="street1" tabindex="0"></label></p>
        <p><label>Street 2 <input type="text" name="street2" tabindex="0"></label></p>
        <p><label>City <input type="text" name="city" tabindex="0"></label></p>
        <p><label>State <input type="text" name="state" tabindex="0"></label></p>
        <p><label>Postal Code <input type="text" name="postcode" tabindex="0"></label></p>
    </fieldset>
</form>
```

The HTML above produces the following form (with default HTML styles):

<form action="/profile/update/" method="post">
    <fieldset>
        <legend>Personal Information</legend>
        <p><label>Salutation <input type="text" name="salutation" tabindex="0"></label></p>
        <p><label>First Name <input type="text" name="firstname" tabindex="0"></label></p>
        <p><label>Family Name <input type="text" name="familyname" tabindex="0"></label></p>
    </fieldset>
    <fieldset>
        <legend>Address</legend>
        <p><label>Street 1 <input type="text" name="street1" tabindex="0"></label></p>
        <p><label>Street 2 <input type="text" name="street2" tabindex="0"></label></p>
        <p><label>City <input type="text" name="city" tabindex="0"></label></p>
        <p><label>State <input type="text" name="state" tabindex="0"></label></p>
        <p><label>Postal Code <input type="text" name="postcode" tabindex="0"></label></p>
    </fieldset>
</form>


As we can see, the fieldsets provide some visual definition for the form, and the legends allow the user to quickly understand what is being requested in each section of the form. We often deal with complex forms that benefit from this sort of structuring, and we can apply any styles we wish to these elements to make them match our visual design.

### Labels
As we see in the examples above, `<label>` elements are used to wrap the names of form fields. Labels serve multiple purposes in an interface, and they should never be omitted. Labels can be used to make it easier to click into a form field (clicking the label activates a form field). This feature is often very helpful, especially when used in conjunction with checkboxes in forms (which are often fiddly to click on). Labels are also used by screen readers to identify the purpose of form fields. This is why labels should never be omitted from a form: Without labels, we restrict accessibility of our forms.

There are two ways to apply labels. In the examples above, the `<label>` tag wraps the input that it is paired with:

```html
<label>Username <input type="text" name="username" tabindex="0"></label>
```

The other method for labeling a form field is to use the `for` attribute on the `<label>` tag:

```html
<label for="username">Username</label> <input type="text" name="username" tabindex="0">
```
By using the `for` attribute, we get the same effect as wrapping the `<input>` with the `<label>` tags. Users can still click the label to activate the field, and screen readers can relate the label and field properly using the `for` attribute. This is also useful if we wish to achieve a visual design that does not have labels (for example, when we use the `placeholder` attribute to indicate what data should go into a form field). With the second structure we can visually hide the label but still make it available to screen readers and other assistive technology.

<div class="tip-box">
    <h3>Accessibility Tip: <code>tabindex="0"</code></h3>
    <p>Whenever we want to make sure users can navigate our sites and apps via keyboard, we can add the attribute <code>tabindex</code> to our HTML elements. This is usually added to form fields, buttons, links, and other interactive elements. When we are coding applications in JavaScript we might use elements in unorthodox ways, which makes it more important for us to pay attention to adding <code>tabindex="0"</code> to our tags.</p>
    <p>The <code>tabindex="0"</code> attribute tells the browser that this field should be included in the list of things that the user can access using the `tab` key on their keyboard. The value <code>"0"</code> tells the browser that this field should be accessed in order of its appearance in the HTML. It is generally better to leave the ordering of elements up to the browser unless we are very familiar with how <code>tabindex</code> works.</p>
    <p>Many users who wish to interact with our sites are reliant on accessibility tools and keyboard navigation. We can serve these users much better by making sure to enable tabbing to any field, button, link, or interactive element in our pages.</p>
</div>


## The `<input>` Element
The real workhorse of form field elements in HTML is the `<input>` element. This is the element that handles most of the data input from users. The input element is relatively simple to write, but it allows for a lot of types. It's useful to know about the available types of input in order to 

## Textareas

## Select Elements

## Form Events









