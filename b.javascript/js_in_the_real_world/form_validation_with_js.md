# Form Validation with JavaScript
Before submitting data to the server, it is important to ensure all required form controls are filled out, in the correct format. This is called client-side form validation, and helps ensure data submitted matches the requirements set forth in the various form controls.

Client-side validation is an initial check and an important feature of good user experience; by catching invalid data on the client-side, the user can fix it straight away. If it gets to the server and is then rejected, a noticeable delay is caused by a round trip to the server and then back to the client-side to tell the user to fix their data.

However, client-side validation should not be considered an exhaustive security measure! Your apps should always perform security checks on any form-submitted data on the server-side as well as the client-side, because client-side validation is too easy to bypass, so malicious users can still easily send bad data through to your server.

### What is form validation?
When you enter data, the browser and/or the web server will check to see that the data is in the correct format and within the constraints set by the application. Validation done in the browser is called client-side validation, while validation done on the server is called server-side validation. In this chapter we are focusing on client-side validation.

If the information is correctly formatted, the application allows the data to be submitted to the server and (usually) saved in a database; if the information isn't correctly formatted, it gives the user an error message explaining what needs to be corrected, and lets them try again.

### Different types of client-side validation
There are two different types of client-side validation that you'll encounter on the web:

+ **Built-in form validation** uses HTML form validation features, which were discussed in the previous "Intermediate HTML and CSS" module. This validation generally doesn't require much JavaScript. Built-in form validation has better performance than JavaScript, but it is not as customizable as JavaScript validation.

+ **JavaScript validation** is coded using JavaScript. This validation is completely customizable, but you need to create it all (or use a library).

### A- Using built-in form validation
One of the most significant features of modern form controls is the ability to validate most user data without relying on JavaScript. This is done by using validation attributes on form elements. We've seen many of these earlier in the course, but to recap:

+ `required`: Specifies whether a form field needs to be filled in before the form can be submitted.
+ `minlength` and `maxlength`: Specifies the minimum and maximum length of textual data (strings).
+ `min` and `max`: Specifies the minimum and maximum values of numerical input types.
+ `type`: Specifies whether the data needs to be a number, an email address, or some other specific preset type.
+ `pattern`: Specifies a regular expression that defines a pattern the entered data needs to follow.

If the data entered in a form field follows all of the rules specified by the above attributes, it is considered valid. If not, it is considered invalid.

When an element is valid, the following things are `true`:

+ The element matches the `:valid` CSS pseudo-class, which lets you apply a specific style to valid elements.
+ If the user tries to send the data, the browser will submit the form, provided there is nothing else stopping it from doing so (e.g., JavaScript).

When an element is invalid, the following things are `true`:

+ The element matches the ``:invalid`` CSS pseudo-class, and sometimes other UI pseudo-classes (e.g., `:out-of-range`) depending on the error, which lets you apply a specific style to invalid elements.
+ If the user tries to send the data, the browser will block the form and display an error message.

## B- Validating forms using Javascript
### The Constraint Validation API
The Constraint Validation API consists of a set of methods and properties available on the following form element DOM interfaces:

+ `HTMLButtonElement` (represents a \<button> element)

+ `HTMLFieldSetElement` (represents a \<fieldset> element)

+ `HTMLInputElement` (represents an \<input> element)

+ `HTMLOutputElement` (represents an \<output> element)

+ `HTMLSelectElement` (represents a \<select> element)

+ `HTMLTextAreaElement` (represents a \<textarea> element)

The Constraint Validation API makes the following properties available on the above elements.

+ `validationMessage`: Returns a localized message describing the validation constraints that the control doesn't satisfy (if any). If the control is not a candidate for constraint validation (willValidate is `false`) or the element's value satisfies its constraints (is valid), this will return an empty string.

+ `validity`: Returns a `ValidityState` object that contains several properties describing the validity state of the element. You can find full details of all the available properties in the MDN ValidityState reference page; below is listed a few of the more common ones:

  - `patternMismatch`: Returns `true` if the value does not match the specified pattern, and `false` if it does match. If `true`, the element matches the `:invalid` CSS pseudo-class.

  - `tooLong`: Returns `true` if the value is longer than the maximum length specified by the maxlength attribute, or `false` if it is shorter than or equal to the maximum. If `true`, the element matches the `:invalid` CSS pseudo-class.

  - `tooShort`: Returns `true` if the value is shorter than the minimum length specified by the minlength attribute, or `false` if it is greater than or equal to the minimum. If `true`, the element matches the `:invalid` CSS pseudo-class.

  - `rangeOverflow`: Returns `true` if the value is greater than the maximum specified by the max attribute, or `false` if it is less than or equal to the maximum. If `true`, the element matches the `:invalid` and :out-of-range CSS pseudo-classes.

  - `rangeUnderflow`: Returns `true` if the value is less than the minimum specified by the min attribute, or `false` if it is greater than or equal to the minimum. If `true`, the element matches the `:invalid` and :out-of-range CSS pseudo-classes.

  - `typeMismatch`: Returns `true` if the value is not in the required syntax (when type is email or url), or `false` if the syntax is correct. If `true`, the element matches the `:invalid` CSS pseudo-class.

  - `valid`: Returns `true` if the element meets all its validation constraints, and is therefore considered to be valid, or `false` if it fails any constraint. If `true`, the element matches the :valid CSS pseudo-class; the `:invalid` CSS pseudo-class otherwise.

  - `valueMissing`: Returns `true` if the element has a required attribute, but no value, or `false` otherwise. If `true`, the element matches the `:invalid` CSS pseudo-class.

+ `willValidate`: Returns `true` if the element will be validated when the form is submitted; `false` otherwise.

The Constraint Validation API also makes the following methods available on the above elements and the `form` element.

+ `checkValidity()`: Returns `true` if the element's value has no validity problems; `false` otherwise. If the element is invalid, this method also fires an `invalid event` on the element.

+ `reportValidity()`: Reports invalid field(s) using events. This method is useful in combination with `preventDefault()` in an `onSubmit` event handler.

+ `setCustomValidity(message)`: Adds a custom error message to the element; if you set a custom error message, the element is considered to be invalid, and the specified error is displayed. This lets you use JavaScript code to establish a validation failure other than those offered by the standard HTML validation constraints. The message is shown to the user when reporting the problem.
The idea is to trigger JavaScript on some form field event (like onchange) to calculate whether the constraint is violated, and then to use the method `field.setCustomValidity()` to set the result of the validation: an empty string means the constraint is satisfied, and any other string means there is an error and this string is the error message to display to the user.

### Implementing a customized error message
Each time a user tries to submit an invalid form, the browser displays an error message. The way this message is displayed depends on the browser.

These automated messages have two drawbacks:

+ There is no standard way to change their look and feel with CSS.
+ They depend on the browser locale, which means that you can have a page in one language but an error message displayed in another language.

Customizing these error messages is one of the most common use cases of the Constraint Validation API.

Here is an example implementation:

```html
<form novalidate>
  <p>
    <label for="mail">
      <span>Please enter an email address:</span>
      <input type="email" id="mail" name="mail" required minlength="8" />
      <span class="error" aria-live="polite"></span>
    </label>
  </p>
  <button>Submit</button>
</form>
```

This simple form uses the novalidate attribute to turn off the browser's automatic validation; this lets our script take control over validation. However, this doesn't disable support for the constraint validation API nor the application of CSS pseudo-classes like :valid, etc. That means that even though the browser doesn't automatically check the validity of the form before sending its data, you can still do it yourself and style the form accordingly.

Our input to validate is an `<input type="email">`, which is required, and has a minlength of 8 characters. Let's check these using our own code, and show a custom error message for each one.

We are aiming to show the error messages inside a `<span>` element. The aria-live attribute is set on that `<span>` to make sure that our custom error message will be presented to everyone, including it being read out to screen reader users.

Note: A key point here is that setting the novalidate attribute on the form is what stops the form from showing its own error message bubbles, and allows us to instead display the custom error messages in the DOM in some manner of our own choosing.

Now onto some basic CSS to improve the look of the form slightly, and provide some visual feedback when the input data is invalid:

```css
body {
  font: 1em sans-serif;
  width: 200px;
  padding: 0;
  margin: 0 auto;
}

p * {
  display: block;
}

input[type="email"] {
  appearance: none;

  width: 100%;
  border: 1px solid #333;
  margin: 0;

  font-family: inherit;
  font-size: 90%;

  box-sizing: border-box;
}

/* This is our style for the invalid fields */
input:invalid {
  border-color: #900;
  background-color: #fdd;
}

input:focus:invalid {
  outline: none;
}

/* This is the style of our error messages */
.error {
  width: 100%;
  padding: 0;

  font-size: 80%;
  color: white;
  background-color: #900;
  border-radius: 0 0 5px 5px;

  box-sizing: border-box;
}

.error.active {
  padding: 0.3em;
}
```

Now let's look at the JavaScript that implements the custom error validation.

```js
const form = document.querySelector("form");
const email = document.getElementById("mail");
const emailError = document.querySelector("#mail + span.error");

email.addEventListener("input", (event) => {
  // Each time the user types something, we check if the
  // form fields are valid.

  if (email.validity.valid) {
    // In case there is an error message visible, if the field
    // is valid, we remove the error message.
    emailError.textContent = ""; // Reset the content of the message
    emailError.className = "error"; // Reset the visual state of the message
  } else {
    // If there is still an error, show the correct error
    showError();
  }
});

form.addEventListener("submit", (event) => {
  // if the email field is valid, we let the form submit
  if (!email.validity.valid) {
    // If it isn't, we display an appropriate error message
    showError();
    // Then we prevent the form from being sent by canceling the event
    event.preventDefault();
  }
});

function showError() {
  if (email.validity.valueMissing) {
    // If the field is empty,
    // display the following error message.
    emailError.textContent = "You need to enter an email address.";
  } else if (email.validity.typeMismatch) {
    // If the field doesn't contain an email address,
    // display the following error message.
    emailError.textContent = "Entered value needs to be an email address.";
  } else if (email.validity.tooShort) {
    // If the data is too short,
    // display the following error message.
    emailError.textContent = `Email should be at least ${email.minLength} characters; you entered ${email.value.length}.`;
  }

  // Set the styling appropriately
  emailError.className = "error active";
}
```

The constraint validation API gives you a powerful tool to handle form validation, letting you have enormous control over the user interface above and beyond what you can do with HTML and CSS alone.

### Validating forms without a built-in API
In some cases, such as `custom controls`, you won't be able to or won't want to use the Constraint Validation API. You're still able to use JavaScript to validate your form, but you'll just have to write your own.

#### An example that doesn't use the constraint validation API:
In order to illustrate this, the following is a simplified version of the previous example without the Constraint Validation API.

The HTML is almost the same; we just removed the HTML validation features.

```html
<form>
  <p>
    <label for="mail">
      <span>Please enter an email address:</span>
      <input type="text" id="mail" name="mail" />
      <span class="error" aria-live="polite"></span>
    </label>
  </p>
  <button>Submit</button>
</form>
```

Similarly, the CSS doesn't need to change very much; we've just turned the :invalid CSS pseudo-class into a real class and avoided using the attribute selector.

```css
body {
  font: 1em sans-serif;
  width: 200px;
  padding: 0;
  margin: 0 auto;
}

form {
  max-width: 200px;
}

p * {
  display: block;
}

input#mail {
  appearance: none;
  width: 100%;
  border: 1px solid #333;
  margin: 0;

  font-family: inherit;
  font-size: 90%;

  box-sizing: border-box;
}

/* This is our style for the invalid fields */
input.invalid {
  border-color: #900;
  background-color: #fdd;
}

input:focus:invalid {
  outline: none;
}

/* This is the style of our error messages */
.error {
  width: 100%;
  padding: 0;

  font-size: 80%;
  color: white;
  background-color: #900;
  border-radius: 0 0 5px 5px;
  box-sizing: border-box;
}

.error.active {
  padding: 0.3em;
}
```

The big changes are in the JavaScript code, which needs to do much more heavy lifting.

```js
const form = document.querySelector("form");
const email = document.getElementById("mail");
const error = email.nextElementSibling;

// As per the HTML Specification
const emailRegExp =
  /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/;

// Now we can rebuild our validation constraint
// Because we do not rely on CSS pseudo-class, we have to
// explicitly set the valid/invalid class on our email field
window.addEventListener("load", () => {
  // Here, we test if the field is empty (remember, the field is not required)
  // If it is not, we check if its content is a well-formed email address.
  const isValid = email.value.length === 0 || emailRegExp.test(email.value);
  email.className = isValid ? "valid" : "invalid";
});

// This defines what happens when the user types in the field
email.addEventListener("input", () => {
  const isValid = email.value.length === 0 || emailRegExp.test(email.value);
  if (isValid) {
    email.className = "valid";
    error.textContent = "";
    error.className = "error";
  } else {
    email.className = "invalid";
  }
});

// This defines what happens when the user tries to submit the data
form.addEventListener("submit", (event) => {
  event.preventDefault();

  const isValid = email.value.length === 0 || emailRegExp.test(email.value);
  if (!isValid) {
    email.className = "invalid";
    error.textContent = "I expect an email, darling!";
    error.className = "error active";
  } else {
    email.className = "valid";
    error.textContent = "";
    error.className = "error";
  }
});
```

As you can see, it's not that hard to build a validation system on your own. The difficult part is to make it generic enough to use both cross-platform and on any form you might create. There are many libraries available to perform form validation, such as `Validate.js`.

---
### Knowledge Check

**Q1.** Explain the importance of validating HTML forms before submitting them to a server.

**A1.** Before submitting data to the server, it is important to ensure all required form controls are filled out, in the correct format. This is called client-side form validation, and helps ensure data submitted matches the requirements set forth in the various form controls.

Client-side validation is an initial check and an important feature of good user experience; by catching invalid data on the client-side, the user can fix it straight away. If it gets to the server and is then rejected, a noticeable delay is caused by a round trip to the server and then back to the client-side to tell the user to fix their data.

We want to make filling out web forms as easy as possible. So why do we insist on validating our forms? There are three main reasons:

+ **We want to get the right data, in the right format.** Our applications won't work properly if our users' data is stored in the wrong format, is incorrect, or is omitted altogether.
+ **We want to protect our users' data.** Forcing our users to enter secure passwords makes it easier to protect their account information.
+ **We want to protect ourselves.** There are many ways that malicious users can misuse unprotected forms to damage the application.

Having said that, never trust data passed to your server from the client. Even if your form is validating correctly and preventing malformed input on the client-side, a malicious user can still alter the network request.

**Q2.** Describe the two types of client-side form validation.

**A2.** There are two different types of client-side validation that you'll encounter on the web:

+ Built-in form validation uses HTML form validation features. This validation generally doesn't require much JavaScript. Built-in form validation has better performance than JavaScript, but it is not as customizable as JavaScript validation.
+ JavaScript validation is coded using JavaScript. This validation is completely customizable, but you need to create it all (or use a library).

**Using built-in form validation:**<br>
One of the most significant features of modern `form controls` is the ability to validate most user data without relying on JavaScript. This is done by using validation attributes on form elements. We've seen many of these earlier in the course, but to recap: required, minlength, maxlength, min, max, type, pattern are the validation attributes.

If the data entered in a form field follows all of the rules specified by the above attributes, it is considered valid. If not, it is considered invalid.

**Validating forms using JavaScript:**<br>
You must use JavaScript if you want to take control over the look and feel of native error messages. In this section we will look at the different ways to do this.

*The Constraint Validation API*<br>
The Constraint Validation API consists of a set of methods and properties available on the following form element DOM interfaces:

+ `HTMLButtonElement` (represents a \<button> element)

+ `HTMLFieldSetElement` (represents a \<fieldset> element)

+ `HTMLInputElement` (represents an \<input> element)

+ `HTMLOutputElement` (represents an \<output> element)

+ `HTMLSelectElement` (represents a \<select> element)

+ `HTMLTextAreaElement` (represents a \<textarea> element)

The Constraint Validation API makes the following properties available on the above elements.

+ `validationMessage`: Returns a localized message describing the validation constraints that the control doesn't satisfy (if any). If the control is not a candidate for constraint validation (willValidate is `false`) or the element's value satisfies its constraints (is valid), this will return an empty string.

+ `validity`: Returns a `ValidityState` object that contains several properties describing the validity state of the element. You can find full details of all the available properties in the MDN ValidityState reference page; below is listed a few of the more common ones:

  - `patternMismatch`: Returns `true` if the value does not match the specified pattern, and `false` if it does match. If `true`, the element matches the `:invalid` CSS pseudo-class.

  - `tooLong`: Returns `true` if the value is longer than the maximum length specified by the maxlength attribute, or `false` if it is shorter than or equal to the maximum. If `true`, the element matches the `:invalid` CSS pseudo-class.

  - `tooShort`: Returns `true` if the value is shorter than the minimum length specified by the minlength attribute, or `false` if it is greater than or equal to the minimum. If `true`, the element matches the `:invalid` CSS pseudo-class.

  - `rangeOverflow`: Returns `true` if the value is greater than the maximum specified by the max attribute, or `false` if it is less than or equal to the maximum. If `true`, the element matches the `:invalid` and :out-of-range CSS pseudo-classes.

  - `rangeUnderflow`: Returns `true` if the value is less than the minimum specified by the min attribute, or `false` if it is greater than or equal to the minimum. If `true`, the element matches the `:invalid` and :out-of-range CSS pseudo-classes.

  - `typeMismatch`: Returns `true` if the value is not in the required syntax (when type is email or url), or `false` if the syntax is correct. If `true`, the element matches the `:invalid` CSS pseudo-class.

  - `valid`: Returns `true` if the element meets all its validation constraints, and is therefore considered to be valid, or `false` if it fails any constraint. If `true`, the element matches the :valid CSS pseudo-class; the `:invalid` CSS pseudo-class otherwise.

  - `valueMissing`: Returns `true` if the element has a required attribute, but no value, or `false` otherwise. If `true`, the element matches the `:invalid` CSS pseudo-class.

+ `willValidate`: Returns `true` if the element will be validated when the form is submitted; `false` otherwise.

The Constraint Validation API also makes the following methods available on the above elements and the `form` element.

+ `checkValidity()`: Returns `true` if the element's value has no validity problems; `false` otherwise. If the element is invalid, this method also fires an `invalid event` on the element.

+ `reportValidity()`: Reports invalid field(s) using events. This method is useful in combination with `preventDefault()` in an `onSubmit` event handler.

+ `setCustomValidity(message)`: Adds a custom error message to the element; if you set a custom error message, the element is considered to be invalid, and the specified error is displayed. This lets you use JavaScript code to establish a validation failure other than those offered by the standard HTML validation constraints. The message is shown to the user when reporting the problem.
The idea is to trigger JavaScript on some form field event (like onchange) to calculate whether the constraint is violated, and then to use the method `field.setCustomValidity()` to set the result of the validation: an empty string means the constraint is satisfied, and any other string means there is an error and this string is the error message to display to the user.


**Q3.** Explain how JavaScript Constraint Validation API provides more control and customization of form validation.

**A3.** Let's demonstrate how JavaScript Constraint Validation API provides more control and customization of form validation by implementing a customized error message.

**Implementing a customized error message:**<br>
Each time a user tries to submit an invalid form, the browser displays an error message. The way this message is displayed depends on the browser.

These automated messages have two drawbacks:

+ There is no standard way to change their look and feel with CSS.
+ They depend on the browser locale, which means that you can have a page in one language but an error message displayed in another language.

Customizing these error messages is one of the most common use cases of the Constraint Validation API.

Here is an example implementation:

```html
<form novalidate>
  <p>
    <label for="mail">
      <span>Please enter an email address:</span>
      <input type="email" id="mail" name="mail" required minlength="8" />
      <span class="error" aria-live="polite"></span>
    </label>
  </p>
  <button>Submit</button>
</form>
```

This simple form uses the novalidate attribute to turn off the browser's automatic validation; this lets our script take control over validation. However, this doesn't disable support for the constraint validation API nor the application of CSS pseudo-classes like :valid, etc. That means that even though the browser doesn't automatically check the validity of the form before sending its data, you can still do it yourself and style the form accordingly.

Our input to validate is an `<input type="email">`, which is required, and has a minlength of 8 characters. Let's check these using our own code, and show a custom error message for each one.

We are aiming to show the error messages inside a `<span>` element. The aria-live attribute is set on that `<span>` to make sure that our custom error message will be presented to everyone, including it being read out to screen reader users.

Note: A key point here is that setting the novalidate attribute on the form is what stops the form from showing its own error message bubbles, and allows us to instead display the custom error messages in the DOM in some manner of our own choosing.

Now onto some basic CSS to improve the look of the form slightly, and provide some visual feedback when the input data is invalid:

```css
body {
  font: 1em sans-serif;
  width: 200px;
  padding: 0;
  margin: 0 auto;
}

p * {
  display: block;
}

input[type="email"] {
  appearance: none;

  width: 100%;
  border: 1px solid #333;
  margin: 0;

  font-family: inherit;
  font-size: 90%;

  box-sizing: border-box;
}

/* This is our style for the invalid fields */
input:invalid {
  border-color: #900;
  background-color: #fdd;
}

input:focus:invalid {
  outline: none;
}

/* This is the style of our error messages */
.error {
  width: 100%;
  padding: 0;

  font-size: 80%;
  color: white;
  background-color: #900;
  border-radius: 0 0 5px 5px;

  box-sizing: border-box;
}

.error.active {
  padding: 0.3em;
}
```

Now let's look at the JavaScript that implements the custom error validation.

```js
const form = document.querySelector("form");
const email = document.getElementById("mail");
const emailError = document.querySelector("#mail + span.error");

email.addEventListener("input", (event) => {
  // Each time the user types something, we check if the
  // form fields are valid.

  if (email.validity.valid) {
    // In case there is an error message visible, if the field
    // is valid, we remove the error message.
    emailError.textContent = ""; // Reset the content of the message
    emailError.className = "error"; // Reset the visual state of the message
  } else {
    // If there is still an error, show the correct error
    showError();
  }
});

form.addEventListener("submit", (event) => {
  // if the email field is valid, we let the form submit
  if (!email.validity.valid) {
    // If it isn't, we display an appropriate error message
    showError();
    // Then we prevent the form from being sent by canceling the event
    event.preventDefault();
  }
});

function showError() {
  if (email.validity.valueMissing) {
    // If the field is empty,
    // display the following error message.
    emailError.textContent = "You need to enter an email address.";
  } else if (email.validity.typeMismatch) {
    // If the field doesn't contain an email address,
    // display the following error message.
    emailError.textContent = "Entered value needs to be an email address.";
  } else if (email.validity.tooShort) {
    // If the data is too short,
    // display the following error message.
    emailError.textContent = `Email should be at least ${email.minLength} characters; you entered ${email.value.length}.`;
  }

  // Set the styling appropriately
  emailError.className = "error active";
}
```

The constraint validation API gives you a powerful tool to handle form validation, letting you have enormous control over the user interface above and beyond what you can do with HTML and CSS alone.

**Q4.** Could forms also be validated without using Constraint Validation API?

**A4.** In some cases, such as `custom controls`, you won't be able to or won't want to use the Constraint Validation API. You're still able to use JavaScript to validate your form, but you'll just have to write your own.

**An example that doesn't use the constraint validation API:**<br>
In order to illustrate this, the following is a simplified version of the previous example without the Constraint Validation API.

The HTML is almost the same; we just removed the HTML validation features.

```html
<form>
  <p>
    <label for="mail">
      <span>Please enter an email address:</span>
      <input type="text" id="mail" name="mail" />
      <span class="error" aria-live="polite"></span>
    </label>
  </p>
  <button>Submit</button>
</form>
```

Similarly, the CSS doesn't need to change very much; we've just turned the :invalid CSS pseudo-class into a real class and avoided using the attribute selector.

```css
body {
  font: 1em sans-serif;
  width: 200px;
  padding: 0;
  margin: 0 auto;
}

form {
  max-width: 200px;
}

p * {
  display: block;
}

input#mail {
  appearance: none;
  width: 100%;
  border: 1px solid #333;
  margin: 0;

  font-family: inherit;
  font-size: 90%;

  box-sizing: border-box;
}

/* This is our style for the invalid fields */
input.invalid {
  border-color: #900;
  background-color: #fdd;
}

input:focus:invalid {
  outline: none;
}

/* This is the style of our error messages */
.error {
  width: 100%;
  padding: 0;

  font-size: 80%;
  color: white;
  background-color: #900;
  border-radius: 0 0 5px 5px;
  box-sizing: border-box;
}

.error.active {
  padding: 0.3em;
}
```

The big changes are in the JavaScript code, which needs to do much more heavy lifting.

```js
const form = document.querySelector("form");
const email = document.getElementById("mail");
const error = email.nextElementSibling;

// As per the HTML Specification
const emailRegExp =
  /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/;

// Now we can rebuild our validation constraint
// Because we do not rely on CSS pseudo-class, we have to
// explicitly set the valid/invalid class on our email field
window.addEventListener("load", () => {
  // Here, we test if the field is empty (remember, the field is not required)
  // If it is not, we check if its content is a well-formed email address.
  const isValid = email.value.length === 0 || emailRegExp.test(email.value);
  email.className = isValid ? "valid" : "invalid";
});

// This defines what happens when the user types in the field
email.addEventListener("input", () => {
  const isValid = email.value.length === 0 || emailRegExp.test(email.value);
  if (isValid) {
    email.className = "valid";
    error.textContent = "";
    error.className = "error";
  } else {
    email.className = "invalid";
  }
});

// This defines what happens when the user tries to submit the data
form.addEventListener("submit", (event) => {
  event.preventDefault();

  const isValid = email.value.length === 0 || emailRegExp.test(email.value);
  if (!isValid) {
    email.className = "invalid";
    error.textContent = "I expect an email, darling!";
    error.className = "error active";
  } else {
    email.className = "valid";
    error.textContent = "";
    error.className = "error";
  }
});
```

As you can see, it's not that hard to build a validation system on your own. The difficult part is to make it generic enough to use both cross-platform and on any form you might create. There are many libraries available to perform form validation, such as `Validate.js`.
