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
    <label>Username <input type="text" name="username"></label>
    <label>Password <input type="password" name="password"></label>
    <input type="submit" value="Login">
</form>
```

In the example above we can see a sample login form. The `action` property is set to a URL that will handle a login, and the method is `post` because we don't want to expose the username or password.

### Form Layout
In order to help with readability and styling of forms, there are a couple of HTML elements that are meant for organizing fields in a form.


## The `<input>` Element

## Textareas

## Select Elements

## Form Events









