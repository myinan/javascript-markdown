# Fundamentals Part 3

## Functions

Quite often we need to perform a similar action in many places of the script. For example, we need to show a nice-looking message when a visitor logs in, logs out and maybe somewhere else. Functions are the main “building blocks” of the program. They allow the code to be called many times without repetition. We’ve already seen examples of built-in functions, like `alert(message)`, `prompt(message, default)` and `confirm(question)`. But we can create functions of our own as well.

### Function Declaration

To create a function we can use a function declaration.

It looks like this:

```javascript
function showMessage() {
  alert('Hello everyone!');
}
```

The `function` keyword goes first, then goes the name of the function, then a list of parameters between the parentheses (comma-separated, empty in the example above, we'll see examples later) and finally the code of the function, also named "the function body", between curly braces.

```javascript
function name(parameter1, parameter2, ... parameterN) {
  // body
}
```

Our new function can be called by its name: `showMessage()`.

For instance:

```javascript
function showMessage() {
  alert('Hello everyone!');
}

showMessage();
showMessage();
```

The call `showMessage()` executes the code of the function. Here we will see the message two times.

This example clearly demonstrates one of the main purposes of functions: to avoid code duplication.

If we ever need to change the message or the way it is shown, it's enough to modify the code in one place: the function which outputs it.

### Scope
In JavaScript, "scope" refers to the context in which variables are declared and accessed during the execution of a program. It defines the visibility and lifetime of variables, functions, and objects, determining which parts of the code can access specific identifiers (variable names) and where those identifiers are valid.

JavaScript has two main types of scope:

1.**Local Scope:** 
<br>Variables declared inside a function or block have local scope. They are only accessible within the function or block in which they are declared. Once the function or block finishes executing, local variables are discarded, and they cannot be accessed from outside the function or block.

```javascript
function showMessage() {
  let message = "Hello, I'm JavaScript!"; // local variable

  alert( message );
}

showMessage(); // Hello, I'm JavaScript!

alert( message ); // <-- Error! The variable is local to the function
```

2.**Global Scope:**
<br>Variables declared outside of any function or block have global scope. They are accessible from any part of the code, including other functions and blocks. Global variables remain in memory throughout the entire lifetime of the application, which means they persist even after the function that declared them has finished executing.

```javascript
let userName = 'John';

function showMessage() {
  let message = 'Hello, ' + userName;
  alert(message);
}

showMessage(); // Hello, John
```

The function has full access to the global variable. It can modify it as well.

For instance:

```javascript
let userName = 'John';

function showMessage() {
  userName = "Bob"; // (1) changed the global variable

  let message = 'Hello, ' + userName;
  alert(message);
}

alert( userName ); // John before the function call

showMessage();

alert( userName ); // Bob, the value was modified by the function
```

The global variable is only used if there’s no local one.

If a same-named variable is declared inside the function then it shadows the global one. For instance, in the code below the function uses the local userName. The global one is ignored:

```javascript
let userName = 'John';

function showMessage() {
  let userName = "Bob"; // declare a local variable

  let message = 'Hello, ' + userName; // Bob
  alert(message);
}

// the function will create and use its own userName
showMessage();

alert( userName ); // John, unchanged, the function did not access the global variable
```

It’s a good practice to minimize the use of global variables. Modern code has few or no globals. Most variables reside in their functions. Sometimes though, they can be useful to store project-level data.

### Parameters
"We can pass arbitrary data to functions using parameters.

In the example below, the function has two parameters: `from` and `text`.

```javascript
function showMessage(from, text) { // parameters: from, text
  alert(from + ': ' + text);
}

showMessage('Ann', 'Hello!'); // Ann: Hello! (*)
showMessage('Ann', "What's up?"); // Ann: What's up? (**)
```

When the function is called in lines (*) and (**), the given values are copied to local variables `from` and `text`. Then the function uses them.

Here’s one more example: we have a variable `from` and pass it to the function. Please note: the function changes `from`, but the change is not seen outside because a function always gets a copy of the value:

```javascript
function showMessage(from, text) {

  from = '*' + from + '*'; // make "from" look nicer

  alert( from + ': ' + text );
}

let from = "Ann";

showMessage(from, "Hello"); // *Ann*: Hello

// the value of "from" is the same, the function modified a local copy
alert(from); // Ann
```

When a value is passed as a function parameter, it’s also called an argument.

In other words, to put these terms straight:

- A parameter is the variable listed inside the parentheses in the function declaration (it’s a declaration time term).
- An argument is the value that is passed to the function when it is called (it’s a call time term).

We declare functions listing their parameters, then call them passing arguments.

In the example above, one might say: "the function `showMessage` is declared with two parameters, then called with two arguments: `from` and "Hello"."."

### Default value of a function parameter
If a function is called, but an argument is not provided, then the corresponding value becomes undefined.

For instance, the aforementioned function `showMessage(from, text)` can be called with a single argument:

```javascript
showMessage("Ann");
```

That’s not an error. Such a call would output "\*Ann\*: undefined". As the value for `text` isn’t passed, it becomes `undefined`.

We can specify the so-called “default” (to use if omitted) value for a parameter in the function declaration, using `=`:

```javascript
function showMessage(from, text = "no text given") {
  alert(from + ": " + text);
}

showMessage("Ann"); // Ann: no text given
```

Now if the `text` parameter is not passed, it will get the value "no text given".

The default value also jumps in if the parameter exists but strictly equals `undefined`, like this:

```javascript
showMessage("Ann", undefined); // Ann: no text given
```

Here "no text given" is a string, but it can be a more complex expression, which is only evaluated and assigned if the parameter is missing. So, this is also possible:

```javascript
function showMessage(from, text = anotherFunction()) {
  // `anotherFunction()` only executed if no text given
  // its result becomes the value of text
}
```

### Rest parameters
In JavaScript, "rest parameters" refer to a feature that allows a function to accept an indefinite number of arguments as an array. This feature was introduced in ECMAScript 6 (ES6) and provides a convenient way to handle functions with a variable number of parameters.

The syntax for defining rest parameters is to prefix the last function parameter with three dots (...). When the function is called, any additional arguments passed to the function are collected into an array, which can be accessed inside the function using the rest parameter name.

Here's the basic syntax of a function with a rest parameter:

```javascript
function functionName(param1, param2, ...restParameters) {
  // Function body
}
```

In this example, `param1` and `param2` are regular parameters, while `...restParameters` is the rest parameter that collects any additional arguments into an array.

Let's see an example to understand how rest parameters work:

```javascript
function sumAllNumbers(...numbers) {
  let sum = 0;
  for (let num of numbers) {
    sum += num;
  }
  return sum;
}

console.log(sumAllNumbers(1, 2, 3, 4, 5)); // Output: 15
console.log(sumAllNumbers(10, 20)); // Output: 30
console.log(sumAllNumbers(2, 4, 6, 8)); // Output: 20
```

In this example, the `sumAllNumbers` function takes any number of arguments and sums them up using the rest parameter `...numbers`. The function works correctly regardless of the number of arguments passed to it.

One important thing to note is that rest parameters must always be the last parameter in the function's parameter list since they collect all remaining arguments. If you try to define a rest parameter before regular parameters, it will result in a syntax error.

#### The difference between rest parameters and the arguments object
+ The `arguments` object is **not a real array**, while rest parameters are Array instances, meaning methods like `sort()`, `map()`, `forEach()` or `pop()` can be applied on it directly.

+ The rest parameter bundles all the extra parameters into a single array, but does not contain any named argument defined before the `...restParam`. The `arguments` object contains all of the parameters — including the parameters in the `...restParam` array — bundled into one array-like object.

#### Examples using rest parameters
In this example, the first argument is mapped to `a` and the second to `b`, so these named arguments are used as normal.

However, the third argument, `manyMoreArgs`, will be an array that contains the third, fourth, fifth, sixth, ..., nth — as many arguments as the user specifies.

```javascript
function myFun(a, b, ...manyMoreArgs) {
  console.log("a", a);
  console.log("b", b);
  console.log("manyMoreArgs", manyMoreArgs);
}

myFun("one", "two", "three", "four", "five", "six");
// a, "one"
// b, "two"
// manyMoreArgs, ["three", "four", "five", "six"] <-- an array
```

Below, even though there is just one value, the last argument still gets put into an array.

```javascript
// Using the same function definition from the example above

myFun("one", "two", "three");
// a, "one"
// b, "two"
// manyMoreArgs, ["three"] <-- an array with just one value
```

Below, the third argument isn't provided, but `manyMoreArgs` is still an array (albeit an empty one).

```javascript
// Using the same function definition from the example above

myFun("one", "two");
// a, "one"
// b, "two"
// manyMoreArgs, [] <-- still an array
```

Below, only one argument is provided, so `b` gets the default value `undefined`, but `manyMoreArgs` is still an empty array.

```javascript
// Using the same function definition from the example above

myFun("one");
// a, "one"
// b, undefined
// manyMoreArgs, [] <-- still an array
```

#### Array methods can be used on rest parameters, but not on the arguments object (the arguments object is not a real array):
```js
function sortRestArgs(...theArgs) {
  const sortedArgs = theArgs.sort();
  return sortedArgs;
}

console.log(sortRestArgs(5, 3, 7, 1)); // 1, 3, 5, 7

function sortArguments() {
  const sortedArgs = arguments.sort();
  return sortedArgs; // this will never happen
}

console.log(sortArguments(5, 3, 7, 1));
// throws a TypeError (arguments.sort is not a function)
```

### Function return in JavaScript
A function returns a value back into the calling code as the result.

The simplest example would be a function that sums two values:

```javascript
function sum(a, b) {
  return a + b;
}

let result = sum(1, 2);
alert(result); // 3
```

The directive `return` can be in any place of the function. When the execution reaches it, the function stops, and the value is returned to the calling code (assigned to `result` above).

There may be many occurrences of `return` in a single function. For instance:

```javascript
function checkAge(age) {
  if (age >= 18) {
    return true;
  } else {
    return confirm('Do you have permission from your parents?');
  }
}

let age = prompt('How old are you?', 18);

if (checkAge(age)) {
  alert('Access granted');
} else {
  alert('Access denied');
}
```

It is also possible to use `return` without a value. That causes the function to exit immediately.

For example:

```javascript
function showMovie(age) {
  if (!checkAge(age)) {
    return;
  }

  alert("Showing you the movie"); // (*)
  // ...
}
```

In the code above, if `checkAge(age)` returns `false`, then `showMovie` won’t proceed to the `alert`.

**IMPORTANT: A function with an empty `return` or without it returns `undefined`**
<br>If a function does not return a value, it is the same as if it returns undefined:

```javascript
function doNothing() { /* empty */ }

alert( doNothing() === undefined ); // true
```

An empty return is also the same as return undefined:

```javascript
function doNothing() {
  return;
}

alert( doNothing() === undefined ); // true
```

### Naming a function
Functions are actions. So their name is usually a verb. It should be brief, as accurate as possible and describe what the function does, so that someone reading the code gets an indication of what the function does.

It is a widespread practice to start a function with a verbal prefix which vaguely describes the action. There must be an agreement within the team on the meaning of the prefixes.

For instance, functions that start with "show" usually show something.

Function starting with…

- "get…" – return a value,
- "calc…" – calculate something,
- "create…" – create something,
- "check…" – check something and return a boolean, etc.

Examples of such names:

```javascript
- showMessage(..)     // shows a message
- getAge(..)          // returns the age (gets it somehow)
- calcSum(..)         // calculates a sum and returns the result
- createForm(..)      // creates a form (and usually returns it)
- checkPermission(..) // checks a permission, returns true/false
```

With prefixes in place, a glance at a function name gives an understanding of what kind of work it does and what kind of value it returns.

#### One function – one action:
A function should do exactly what is suggested by its name, no more.

Two independent actions usually deserve two functions, even if they are usually called together (in that case we can make a 3rd function that calls those two).

A few examples of breaking this rule:

`getAge` – would be bad if it shows an alert with the age (should only get).<br>
`createForm` – would be bad if it modifies the document, adding a form to it (should only create it and return).<br>
`checkPermission` – would be bad if it displays the access granted/denied message (should only perform the check and return the result).

**Functions should be short and do exactly one thing.** If that thing is big, maybe it’s worth it to split the function into a few smaller functions. Sometimes following this rule may not be that easy, but it’s definitely a good thing.

### Function declarations and Function expressions
In JavaScript, functions are not only a way to organize code but also a special type of value. There are two primary ways to define a function: Function Declarations and Function Expressions.

1. **Function Declaration:**
<br>A Function Declaration is the standard way to define a function with a name. It looks like this:

```javascript
function sayHi() {
  alert("Hello");
}
```

In this case, the function `sayHi` is hoisted, which means it's available throughout the entire scope where it's declared.

2. **Function Expression:**
A Function Expression, on the other hand, allows us to create a function and assign it to a variable. It looks like this:

```javascript
let sayHi = function() {
  alert("Hello");
};
```

Here, we define an anonymous function (a function without a name) and assign it to the variable `sayHi`. The function creation happens within the context of an assignment expression, making it a Function Expression. In Function Expressions, the function can be anonymous, meaning it doesn't have a name after the `function` keyword.

Function Declarations are processed before the code block is executed, they are visible everywhere in the block(hoisted). Function Expressions however, are created and are only accessible when the execution flow reaches them.

### Function is a value
Like we said before, in JavaScript, functions are not only a way to organize code but also a special type of value. Functions created with either above method are values that can be stored in variables, passed as arguments to other functions, or returned from functions, just like any other data. We can also copy functions to other variables.

Both examples above store a function in the `sayHi` variable.

We can even print out that value using `alert`:

```javascript
function sayHi() {
  alert( "Hello" );
}

alert( sayHi ); // shows the function code
```

Please note that the last line does not run the function, because there are no parentheses after `sayHi`. There are programming languages where any mention of a function name causes its execution, but JavaScript is not like that.

In JavaScript, a function is a value, so we can deal with it as a value. The code above shows its string representation, which is the source code.

Surely, a function is a special value, in the sense that we can call it like `sayHi()`.

But it’s still a value. So we can work with it like with other kinds of values.

We can copy a function to another variable:

```javascript
function sayHi() {   // (1) create
  alert( "Hello" );
}

let func = sayHi;    // (2) copy

func(); // Hello     // (3) run the copy (it works)!
sayHi(); // Hello    //     this still works too (why wouldn't it)
```

Here’s what happens above in detail:

- The Function Declaration (1) creates the function and puts it into the variable named `sayHi`.
- Line (2) copies it into the variable `func`. Please note again: there are no parentheses after `sayHi`. If there were, then `func = sayHi()` would write the result of the call `sayHi()` into `func`, not the function `sayHi` itself.
- Now the function can be called as both `sayHi()` and `func()`.
- We could also have used a Function Expression to declare `sayHi`, in the first line:

```javascript
let sayHi = function() { // (1) create
  alert( "Hello" );
};

let func = sayHi;
// ...
```

Everything would work the same.

### Callback functions
A callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine or action.

As an example, we’ll write a function ask(question, yes, no) with three parameters:

`question`
<br>Text of the question

`yes`
<br>Function to run if the answer is “Yes”

`no`
<br>Function to run if the answer is “No”

The function should ask the question and, depending on the user’s answer, call `yes()` or `no()`:

```javascript
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}

function showOk() {
  alert( "You agreed." );
}

function showCancel() {
  alert( "You canceled the execution." );
}

// usage: functions showOk, showCancel are passed as arguments to ask
ask("Do you agree?", showOk, showCancel);
```

**The arguments `showOk` and `showCancel` of ask are called `callback functions` or just `callbacks`.**

The idea is that we pass a function and expect it to be “called back” later if necessary. In our case, showOk becomes the callback for “yes” answer, and showCancel for “no” answer.

Note that when we pass a function as an argument, we do not use parenthesis. Its because we want to pass the function as an argument and not yet execute it.

We can use Function Expressions to write an equivalent, shorter function:

```javascript
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}

ask(
  "Do you agree?",
  function() { alert("You agreed."); },
  function() { alert("You canceled the execution."); }
```

Here, functions are declared right inside the ask(...) call. They have no name, and so are called anonymous. Such functions are not accessible outside of ask (because they are not assigned to variables), but that’s just what we want here.

Such code appears in our scripts very naturally, it’s in the spirit of JavaScript.

#### When to choose Function Declaration versus Function Expression?

As a rule of thumb, when we need to declare a function, the first thing to consider is Function Declaration syntax. It gives more freedom in how to organize our code, because we can call such functions before they are declared.

That’s also better for readability, as it’s easier to look up function f(…) {…} in the code than let f = function(…) {…};. Function Declarations are more “eye-catching”.

…But if a Function Declaration does not suit us for some reason (when you need a function that isn’t hoisted, when the function should only be used when it is defined, or when the function is anonymous, or doesn’t need a name for later use), then Function Expression should be used.

#### Function Expression vs Function Declaration Summary
+ Functions are values. They can be assigned, copied or declared in any place of the code.
+ If the function is declared as a separate statement in the main code flow, that’s called a “Function Declaration”.
+ If the function is created as a part of an expression, it’s called a “Function Expression”.
+ Function Declarations are processed before the code block is executed. They are visible everywhere in the block.
+ Function Expressions are created when the execution flow reaches them.

In most cases when we need to declare a function, a Function Declaration is preferable, because it is visible prior to the declaration itself. That gives us more flexibility in code organization, and is usually more readable.

So, our main preference when we need to declare a function should be Function Declaration and we should use a Function Expression only when a Function Declaration is not fit for the task.

### Arrow functions, the basics
There’s another very simple and concise syntax for creating functions, that’s often better than Function Expressions.

It’s called “arrow functions”, because it looks like this:

```js
let func = (arg1, arg2, ..., argN) => expression;
```

This creates a function `func` that accepts arguments `arg1`..`argN`, then evaluates the expression on the right side with their use and returns its result.

In other words, it’s the shorter version of:

```js
let func = function(arg1, arg2, ..., argN) {
  return expression;
};
```

Let’s see a concrete example:

```js
let sum = (a, b) => a + b;

/* This arrow function is a shorter form of:

let sum = function(a, b) {
  return a + b;
};
*/

alert(sum(1, 2)); // 3
```

As you can see, `(a, b) => a + b` means a function that accepts two arguments named `a` and `b`. Upon the execution, it evaluates the expression `a + b` and returns the result.

If we have only one argument, then parentheses around parameters can be omitted, making that even shorter.

For example:

```js
let double = n => n * 2;
// roughly the same as: let double = function(n) { return n * 2 }
```

```js
alert(double(3)); // 6
```

If there are no arguments, parentheses are empty, but they must be present:

```js
let sayHi = () => alert("Hello!");

sayHi();
```

Arrow functions can be used in the same way as Function Expressions.

For instance, to dynamically create a function:

```js
let age = prompt("What is your age?", 18);

let welcome = (age < 18) ?
  () => alert('Hello!') :
  () => alert("Greetings!");

welcome();
```

Arrow functions may appear unfamiliar and not very readable at first, but that quickly changes as the eyes get used to the structure.

They are very convenient for simple one-line actions when we’re just too lazy to write many words.

#### Multiline arrow functions
Sometimes we need a more complex function, with multiple expressions and statements. In that case, we can enclose them in curly braces. The major difference is that curly braces require a return within them to return a value (just like a regular function does).

Like this:

```js
let sum = (a, b) => {  // the curly brace opens a multiline function
  let result = a + b;
  return result; // if we use curly braces, then we need an explicit "return"
};

alert( sum(1, 2) ); // 3
```

#### Arrow functions summary
Arrow functions are handy for simple actions, especially for one-liners. They come in two flavors:

+ Without curly braces: `(...args) => expression` – the right side is an expression: the function evaluates it and returns the result. Parentheses can be omitted, if there’s only a single argument, e.g. `n => n*2`.

+ With curly braces: `(...args) => { body }` – brackets allow us to write multiple statements inside the function, but we need an explicit `return` to return something.

## JavaScript Execution Context
Let's look at how JavaScript code gets executed.

Let’s start with the following example:

```js
let x = 10;

function timesTen(a){
    return a * 10;
}

let y = timesTen(x);

console.log(y); // 100
```

In this example:

+ First, declare the x variable and initialize its value with 10.
+ Second, declare the timesTen() function that accepts an argument and returns a value that is the result of multiplication of the argument with 10.
+ Third, call the timesTen() function with the argument as the value of the x variable and store result in the variable y.
+ Finally, output the variable y to the Console.

Behind the scene, JavaScript does many things. On the following, we will focus on execution contexts.

When the JavaScript engine executes the JavaScript code, it creates `execution contexts`.

Each execution context has two phases: `the creation phase` and the `execution phase`.

### The creation phase
When the JavaScript engine executes a script for the first time, it creates **`the global execution context`**. During this phase (global execution context - creation phase), the JavaScript engine performs the following tasks:

+ Create the global object i.e., *window* in the web browser or global in Node.js.
+ Create the *this* object and bind it to the global object.
+ Setup a memory heap for storing variables and function references.
+ Store the function declarations in the memory heap and variables within the global execution context with the initial values as *undefined*.

When the JavaScript engine executes the code example above, it does the following in the creation phase:

+ First, store the variables x and y and function declaration timesTen() in the global execution context.
+ Second, initialize the variables x and y to undefined.

![Global Execution Context - Creation Phase](../../img/js_execution/js-execution-context-1.png "Global Execution Context - Creation Phase")

After the creation phase, the global execution context moves to the execution phase.

### The execution phase
During the execution phase(global execution context - execution phase), the JavaScript engine executes the code line by line, assigns the values to variables, and executes the function calls.

![Global Execution Context - Execution Phase](../../img/js_execution/js-execution-context-2.png "Global Execution Context - Execution Phase")

For each function call, the JavaScript engine creates a new **`function execution context`**.

The function execution context is similar to the global execution context. But instead of creating the global object, the JavaScript engine creates the *arguments* object that is a reference to all the parameters of that function:

![Function Execution Context - Creation Phase](../../img/js_execution/js-execution-context-3.png "Function Execution Context - Creation Phase")

In our example, the function execution context creates the *arguments* object that references all parameters passed into the function, sets *this* value to the global object, and initializes the *a* parameter to *undefined*.

During the execution phase of the function execution context, the JavaScript engine assigns 10 to the parameter *a* and returns the result (100) to the global execution context:

![Function Execution Context - Execution Phase](../../img/js_execution/js-execution-context-4.png "Function Execution Context - Execution Phase")

To keep track of all the execution contexts, including the global execution context and function execution contexts, the JavaScript engine uses the `call stack`.

### JavaScript Call Stack
The call stack is a data structure that keeps track of function calls during the execution of a program. It's used by the JavaScript engine to manage the flow of execution of the program.

Also, the JavaScript engine uses a call stack to manage execution contexts:

+ Global execution context
+ function execution contexts

The call stack works based on the `LIFO` principle i.e., `last-in-first-out`.

When you execute a script, the JavaScript engine creates a global execution context and pushes it on top of the call stack.

Whenever a function is called, the JavaScript engine creates a function execution context for the function, pushes it on top of the call stack, and starts executing the function.

If a function calls another function, the JavaScript engine creates a new function execution context for the function being called and pushes it on top of the call stack.

When the current function completes, the JavaScript engine pops it off the call stack and resumes the execution where it left off.

The script will stop when the call stack is empty.

#### Let’s continue with the following example:

```js
function add(a, b) {
    return a + b;
}

function average(a, b) {
    return add(a, b) / 2;
}

let x = average(10, 20);
```

When the JavaScript engine executes this script, it places the global execution context (denoted by `main()` or `global()` ) function on the call stack.

![Call Stack](../../img/js_execution/call_stack/call-stack-1.png)

The global execution context first enters the creation phase and then moves to the execution phase.

The JavaScript engine executes the call to the `average(10, 20)` function and creates a function execution context for the `average()` function and pushes it on top of the call stack:

![Call Stack](../../img/js_execution/call_stack/call-stack-2.png)

The JavaScript engine starts executing the average() since because the average() function is on the top of the call stack.

The average() function calls add() function. At this point, the JavaScript engine creates another function execution context for the `add()` function and places it on the top of the call stack:

![Call Stack](../../img/js_execution/call_stack/call-stack-3.png)

JavaScript engine executes the add() function and pops it off the call stack:

![Call Stack](../../img/js_execution/call_stack/call-stack-4.png)

At this point, the average() function is on the top of the call stack, the JavaScript engine executes and pops it off the call stack.

![Call Stack](../../img/js_execution/call_stack/call-stack-5.png)

Now, the call stack is empty so the script stops executing:

![Call Stack](../../img/js_execution/call_stack/call-stack-6.png "Empty Stack")

The following picture illustrates the overall status of the Call Stack in all steps:

![Call Stack](../../img/js_execution/call_stack/call-stack-7.png)

#### Stack overflow

The call stack has a fixed size, depending on the implementation of the host environment, either the web browser or Node.js.

If the number of execution contexts exceeds the size of the stack, a **stack overflow** error will occur.

For example, when you execute a recursive function that has no exit condition, the JavaScript engine will issue a stack overflow error:

```js
function fn() {
    fn();
}

fn(); // stack overflow
```

The call stack is designed to have a fixed size in JavaScript (and in most programming languages) for several reasons and not limited to:

1. **Predictable Memory Management**: Having a fixed-size call stack allows for more predictable memory management. When the maximum size is known and fixed, the JavaScript engine can allocate memory for the stack at the program's start, ensuring that the memory requirements are clear and consistent.

2. **Resource Constraints**: JavaScript is often executed in environments with limited resources, such as web browsers or embedded systems. By defining a fixed-size call stack, the language ensures that the memory used for function calls is limited and can be managed efficiently within these resource constraints.

3. **Security and Stability**: Limiting the size of the call stack helps prevent stack overflow vulnerabilities and makes the JavaScript environment more stable. Without a maximum limit, malicious or poorly designed code could potentially consume all available memory, leading to crashes or denial-of-service attacks.

#### Asynchronous JavaScript

JavaScript is a single-threaded programming language. This means that the JavaScript engine has only one call stack. Therefore, it only can do one thing at a time.

When executing a script, the JavaScript engine executes code from top to bottom, line by line. In other words, it is synchronous.

Asynchronous means the JavaScript engine can execute other tasks while waiting for another task to be completed. For example, the JavaScript engine can:

+ Request for data from a remote server.
+ Display a spinner
+ When the data is available, display it on the webpage.

To do this, the JavaScript engine uses an *event loop*, which will be covered in following lessons.


---

### Knowledge Check

**Q1.** What are functions useful for?

**A1.** Functions are useful for executing the same blocks of code multiple times in our program. When we define a function, we can call that function in various places of our code, avoiding the need for writing the same lines of code over and over again.

**Q2.** How do you invoke a function?

**A2.** To invoke a function, it's not enough to just define the function, we also need to call that function in our code. For example, we define and call(invoke) a function as the following:

```js
function add(firstNumber, secondNumber) {   
  return firstNumber + secondNumber;        // Function definition
}

add(5, 10); // Function call
```

**Q3.** What are anonymous functions?

**A3.** In JavaScript, an anonymous function refers to a function that does not have a name. Instead of being defined with a specific identifier, anonymous functions are typically created on the fly as expressions and are often used as callbacks or inline functions. They are also known as "function expressions."

Anonymous functions are commonly used in scenarios where you need a function temporarily for a specific task or when you don't want to pollute the global namespace with a named function. 

**Q4.** What is function scope?

**A4.** Variables declared inside a function or block have local scope. They are only accessible within the function or block in which they are declared. Once the function or block finishes executing, local variables are discarded, and they cannot be accessed from outside the function or block.

So, as a variable with a block scope can only be accessed within that block, a variable with a function scope can only be accessed from the function in which it was declared. They both have local scope unlike the variables defined in the global scope.

**Q5.** What are return values?
  
**A5.** In JavaScript, a return value refers to the value that a function produces and gives back to the caller when the function is invoked. Every function in JavaScript, unless explicitly specified otherwise, returns a value. If there is no explicit return statement in a function, it will automatically return *undefined*.

**Q6.** What are arrow functions?

**A6.** Arrow functions are function expressions. They are introduced relatively recently in javascript as an alternative way for function expressions. Example:

```js
let arrowFunc = (para1, para2) => para1 + para2; // takes two parameters, para1 and para2, adds them and returns the result
```