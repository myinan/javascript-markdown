# Understanding Errors

In JavaScript, errors occur when the code encounters a problem or unexpected condition that prevents it from executing successfully. Understanding errors and their anatomy is essential for developers to write robust and reliable code. Let's dive into the details:


## Errors in JavaScript:

Errors in JavaScript can be categorized into three main types:

1. **Syntax Errors**: These errors occur when the code violates the language's rules for proper syntax. It means the code is not written correctly and cannot be interpreted by the JavaScript engine. Syntax errors are typically caught by the code editor or the JavaScript engine when the code is being parsed.

Example:
```javascript
let x = 10;
console.log(x  // SyntaxError: missing ) after argument list.
```

2. **Runtime Errors**: These errors occur when the code is syntactically correct, but an issue arises during execution. They are often referred to as exceptions and cause the program to halt abruptly. Runtime errors can occur due to various reasons, such as referencing undefined variables, dividing by zero, or accessing properties of null/undefined objects.

Example:
```javascript
let y = 5;
console.log(y + z);  // ReferenceError: z is not defined.
```

3. **Logic Errors**: These are the trickiest errors as they don't produce any error messages. Instead, the code executes, but the output is not what was expected. Logic errors happen when there is an issue in the algorithm or the design of the code.

Example:
```javascript
function calculateArea(width, height) {
  return width * width;  // Incorrect formula, should be width * height.
}
console.log(calculateArea(5, 10));  // Output: 25 (instead of 50).
```


## Anatomy of an Error:
An error is a type of object built into the JS language, mainly consisting of a name/type and a message. Errors contain crucial information that can assist you in locating the code responsible for the error, determining why you have this error, and resolving the error.

When an error occurs, JavaScript provides information to help developers identify and fix the problem. The error object contains several properties that offer valuable insights:

1. **Name**: The name of the error, which helps identify the type of error that occurred (e.g., "SyntaxError," "ReferenceError," "TypeError," etc.).

2. **Message**: A description of the error, providing more context about what went wrong.

3. **Stack Trace**: A trace of the function calls that led to the error, including the line numbers and files involved. The stack trace helps pinpoint where the error originated.

4. **Line Number and Column Number**: These properties indicate the location within the source code where the error occurred.

5. **Source URL**: In web browsers, if the JavaScript code is loaded from an external source (e.g., a script on a different domain), this property holds the URL of the script file.


## Common Error Types in JavaScript:

1. **ReferenceError**: This error occurs when trying to access a variable or function that doesn't exist or is out of scope.

Example:
```javascript
console.log(a);  // ReferenceError: a is not defined.
```

2. **TypeError**: This error occurs when a variable or value is not of the expected type.

Example:
```javascript
let num = 42;
num();  // TypeError: num is not a function.
```

3. **RangeError**: This error occurs when a numeric variable or parameter is not within its allowed range.

Example:
```javascript
function factorial(n) {
  if (n === 0) {
    return 1;
  } else {
    return n * factorial(n - 1); // RangeError: Maximum call stack size exceeded.
  }
}
factorial(100000);
```

4. **SyntaxError**: As mentioned earlier, this error occurs when the code has a syntax mistake.

Example:
```javascript
let x = 10;
console.log(x  // SyntaxError: missing ) after argument list.
```

5. **EvalError**: This error is thrown when using the `eval()` function and there's an issue with the evaluation.

Example:
```javascript
eval('alert("Hello, world!");');  // EvalError: alert is not defined.
```

6. **URIError**: This error occurs when using faulty URI-related functions like `decodeURI()`, `encodeURI()`, `decodeURIComponent()`, and `encodeURIComponent()`.

Example:
```javascript
decodeURIComponent('%');  // URIError: URI malformed.
```

7. **InternalError**: This error occurs when an internal error in the JavaScript engine takes place. It is rarely encountered and is usually related to engine implementation issues.

It's important for developers to understand these error types and their specific messages to diagnose and resolve issues in their JavaScript code effectively. Proper error handling and debugging practices are essential for writing robust and maintainable applications.

## How to resolve errors
+ Read the error carefully and try to understand it completely.
+ Google the error! Chances are, you can find a fix or explanation on StackOverflow or in the documentation.
+ Use the debugger! As previously mentioned, the built in debugger in DevTools is great for more involved troubleshooting, and is a critical tool for a developer.
+ Make use of the console! console.log() is a popular choice for quick debugging. For more involved troubleshooting, using the debugger might be more appropriate, but using console.log() is great for getting immediate feedback without needing to step through your functions. There are also other useful methods such as console.table(), console.trace(), and more.

## Errors vs. warnings
Errors will stop the execution of your program or whatever process you may be attempting to run and prevent further action. Warnings, on the other hand, are messages that provide you insight on potential problems that may not necessarily crash your program at runtime, or at all! While you should address these warnings if possible and as soon as possible, warnings are not as significant as errors and are more likely to be informational. Warnings are typically shown in yellow, while errors are typically shown in red. Though these colors are not a rule, frequently there will be a visual differentiation between the two, regardless of the platform you are encountering them on.

---

### Knowledge Check

**Q1.** What are three reasons why you may see a TypeError?

**A1.** "Per MDN, a `TypeError` may be thrown when:
+ an operand or argument passed to a function is incompatible with the type expected by that operator or function;
+ or when attempting to modify a value that cannot be changed;
+ or when attempting to use a value in an inappropriate way. "

**Q2.** What is the key difference between an error and a warning?

**A2.** An error stops the execution of the program. A warning is useful information provided by the javascript engine to avoid possible future errors. Warnings do not stop the execution of the program.

**Q3.** What is one method you can use to resolve an error?

**A3.**
+ Google the error! Chances are, you can find a fix or explanation on StackOverflow or in the documentation.
+ Use the debugger! As previously mentioned, the built in debugger in DevTools is great for more involved troubleshooting, and is a critical tool for a developer.
+ Make use of the console! console.log() is a popular choice for quick debugging. For more involved troubleshooting, using the debugger might be more appropriate, but using console.log() is great for getting immediate feedback without needing to step through your functions. There are also other useful methods such as console.table(), console.trace(), and more.