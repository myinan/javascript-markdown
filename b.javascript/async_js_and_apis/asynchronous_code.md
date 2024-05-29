# Asynchronous Code
## Callback Function
A callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine or action.

The consumer of a callback-based API writes a function that is passed into the API. The provider of the API (called the caller) takes the function and calls back (or executes) the function at some point inside the caller's body. The caller is responsible for passing the right parameters into the callback function. The caller may also expect a particular return value from the callback function, which is used to instruct further behavior of the caller.

There are two ways in which the callback may be called: synchronous and asynchronous. Synchronous callbacks are called immediately after the invocation of the outer function, with no intervening asynchronous tasks, while asynchronous callbacks are called at some point later, after an asynchronous operation has completed.

Understanding whether the callback is synchronously or asynchronously called is particularly important when analyzing side effects. Consider the following example:

```js
let value = 1;

doSomething(() => {
  value = 2;
});

console.log(value);
```

If `doSomething` calls the callback synchronously, then the last statement would log `2` because `value = 2` is synchronously executed; otherwise, if the callback is asynchronous, the last statement would log `1` because `value = 2` is only executed after the `console.log` statement.

Examples of synchronous callbacks include the callbacks passed to `Array.prototype.map()`, `Array.prototype.forEach()`, etc. Examples of asynchronous callbacks include the callbacks passed to `setTimeout()` and `Promise.prototype.then()`.


## When to use sync / async functions
The choice between synchronous and asynchronous functions in JavaScript often depends on the nature of the task and the resources involved.

- **Synchronous functions:**
  - Well-suited for tasks that involve local processing, such as CPU-intensive calculations or operations that primarily use RAM.
  - The program waits for each operation to complete before moving on to the next one, which can simplify code structure.

- **Asynchronous functions:**
  - Ideal for tasks that involve I/O operations, such as reading from a file, making network requests, or interacting with a database.
  - By using asynchronous functions, you can initiate an operation and continue with other tasks without waiting for the operation to complete. Callbacks, Promises, and async/await are common mechanisms for handling asynchronous operations in JavaScript.

In scenarios where you need to access hard drives or make network requests (which involve waiting for external resources), using asynchronous functions helps ensure that your program doesn't get blocked while waiting for these operations to finish. This is particularly important in web development where waiting for I/O operations synchronously could lead to unresponsive user interfaces.

It's worth noting that the introduction of the `async/await` syntax in JavaScript has made it more convenient to work with asynchronous code, making it resemble synchronous code in structure while still allowing non-blocking behavior.

## Javascript `Promise` API
The Promise API in JavaScript is a mechanism for handling asynchronous operations. It provides a way to deal with the result or failure of an asynchronous operation once it completes. Promises are objects representing the eventual completion or failure of an asynchronous operation, and they are used to simplify the handling of asynchronous code.

The Promise API aims to solve two major categories of deficiencies with using callbacks to express program asynchrony and manage concurrency: lack of sequentiality (non-linear nature of callbacks) and lack of trustability (the inversion of control).

A Promise can be in one of three states:

1. **Pending**: The initial state. The asynchronous operation is still in progress.
2. **Fulfilled**: The operation completed successfully, and the promise has a result.
3. **Rejected**: The operation failed, and the promise has a reason for the failure.

Here's a basic overview of the Promise API:

### Creating a Promise
To create a promise, you use the `Promise` constructor, which takes a function as an argument. This function is called the "executor" and is responsible for the asynchronous operation. The executor function takes two parameters: `resolve` and `reject`. You call `resolve` when the operation succeeds and `reject` when it fails.

```javascript
const myPromise = new Promise((resolve, reject) => {
  // Asynchronous operation
  // If successful, call resolve(result)
  // If failed, call reject(error)
});
```

P.S.: Saying that on success(fullfillment) the resolve function is called is not accurate. `Promise.resolve(..)` can actually result in either fulfillment or rejection. The first callback parameter of the Promise(..) constructor will unwrap either a thenable(a thenable object which is not a Promise object)  or a genuine Promise (this behaviour is identical to what `Promise.resolve(..)` does):

```js
var rejectedPr = new Promise( function(resolve,reject){
	// resolve this promise with a rejected promise
	resolve( Promise.reject( "Oops" ) );
} );

rejectedPr.then(
	function fulfilled(){
		// never gets here
	},
	function rejected(err){
		console.log( err );	// "Oops"
	}
);
```

That is also the reason the first callback passed to the Promise constructor is called "resolve" instead of "fulfill".

In this example, the promise chain is initiated by a custom-written new Promise() construct; but in actual practice, promise chains more typically start with an API function (written by someone else) that returns a promise.

### Handling Promise Results
Once you have a promise, you can attach callbacks to it using the `.then()` method. This method takes two optional callback functions: one for the fulfillment case and one for the rejection case.

```javascript
function fulfilled(msg) {
	console.log( msg );
}

function rejected(err) {
	console.error( err );
}

myPromise.then(
	fulfilled,
	rejected
);
```

In the case of the first parameter to then(..), it's unambiguously always the fulfillment case, so there's no need for the duality of "resolve" terminology used in the Promise constructor.

### Chaining Promises
Promises can be chained using multiple `.then()` calls. This is useful for sequential asynchronous operations.

```javascript
myPromise
  .then((result) => {
    // First operation successful, do something with result
    return anotherPromise; // Return a new promise for chaining
  })
  .then((result) => {
    // Handle the result of the second operation
  })
  .catch((error) => {
    // Handle any error in the chain
  });
```

### Handling Errors
You can use the `.catch()` method to handle errors at any point in the promise chain. The catch callback is executed when the promise is rejected. What you provide to the reject method is up to you. A frequent pattern is sending an `Error` to the catch.

```javascript
myPromise
  .then((result) => {
    // Handle success
  })
  .catch((error) => {
    // Handle error
  });
```

### The `finally` method
`finally` callback is called regardless of success or failure:

```js
(new Promise((resolve, reject) => { reject("Nope"); }))
    .then(() => { console.log("success") })
    .catch(() => { console.log("fail") })
    .finally(res => { console.log("finally") });

// >> fail
// >> finally
```

**IMPORTANT:** The behavior of `finally` is different from `then` in terms of the returned Promise.

When you use the `then` method, it returns a new Promise. The `then` method creates and returns a new Promise that can be used to chain additional `then` or `catch` handlers. Each `then` call in the chain creates a new Promise.

On the other hand, the `finally` method returns the same Promise instance to which it was applied. It does not create a new Promise; rather, it allows you to attach a callback that will be executed when the original Promise is settled (either fulfilled or rejected), and it returns a reference to the original Promise.

Here's a simple illustration:

```javascript
const originalPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Success!");
    // or
    // reject(new Error("Failed!"));
  }, 1000);
});

const thenPromise = originalPromise.then(result => {
  console.log("Result:", result);
  return "New Value";
});

const finallyPromise = originalPromise.finally(() => {
  console.log("Finally block executed.");
});

console.log(originalPromise === thenPromise); // false, because then creates a new Promise
console.log(originalPromise === finallyPromise); // true, because finally returns the original Promise
```

In this example, `thenPromise` is a new Promise created by the `then` method, while `finallyPromise` is a reference to the original Promise returned by the `finally` method.

### Promise.all and Promise.race
The `Promise.all()` method takes an array of promises and returns a new promise that fulfills with an array of results when all of the input promises have fulfilled. On the other hand, `Promise.race()` takes an array of promises and returns a new promise that fulfills or rejects as soon as one of the input promises fulfills or rejects.

```javascript
const promisesArray = [promise1, promise2, promise3];

Promise.all(promisesArray)
  .then((results) => {
    // All promises fulfilled, results is an array of their results
  })
  .catch((error) => {
    // At least one promise rejected
  });

Promise.race(promisesArray)
  .then((result) => {
    // The first promise to fulfill or reject
  })
  .catch((error) => {
    // The first promise to reject
  });
```

With `Promise.all` you could combine APIs like fetch and the Battery API since they both return promises:

```js
Promise.all([fetch('/users.json'), navigator.getBattery()]).then(function(results) {
	// Both promises done!
});
```

With `Promise.all`, if any promise is rejected the catch fires for the first rejection:

```js
var req1 = new Promise(function(resolve, reject) { 
	// A mock async action using setTimeout
	setTimeout(function() { resolve('First!'); }, 4000);
});
var req2 = new Promise(function(resolve, reject) { 
	// A mock async action using setTimeout
	setTimeout(function() { reject('Second!'); }, 3000);
});
Promise.all([req1, req2]).then(function(results) {
	console.log('Then: ', results);
}).catch(function(err) {
	console.log('Catch: ', err);
});

// From the console:
// Catch: Second!
```

**Note:** Technically, the array of values passed into `Promise.all([ .. ])` can include Promises, thenables, or even immediate values. Each value in the list is essentially passed through `Promise.resolve(..)` to make sure it's a genuine Promise to be waited on, so an immediate value will just be normalized into a Promise for that value. If the array is empty, the main Promise is immediately fulfilled.

The main promise returned from Promise.all([ .. ]) will only be fulfilled if and when all its constituent promises are fulfilled. If any one of those promises instead is rejected, the main Promise.all([ .. ]) promise is immediately rejected, discarding all results from any other promises.

`Promise.race`, instead of waiting for all promises to be resolved or rejected, triggers as soon as any promise in the array is resolved or rejected:

```js
var req1 = new Promise(function(resolve, reject) { 
	// A mock async action using setTimeout
	setTimeout(function() { resolve('First!'); }, 8000);
});
var req2 = new Promise(function(resolve, reject) { 
	// A mock async action using setTimeout
	setTimeout(function() { resolve('Second!'); }, 3000);
});
Promise.race([req1, req2]).then(function(one) {
	console.log('Then: ', one);
}).catch(function(one, two) {
	console.log('Catch: ', one);
});

// From the console:
// Then: Second!
```

A use case could be triggering a request to a primary source and a secondary source (in case the primary or secondary are unavailable).

`Promise.race([ .. ])` also expects a single array argument, containing one or more Promises, thenables, or immediate values. It doesn't make much practical sense to have a race with immediate values, because the first one listed will obviously win -- like a foot race where one runner starts at the finish line!

### Timeout Race
`Promise.race([ .. ])` can be used to express the "promise timeout" pattern:

```js
// `foo()` is a Promise-aware function

// `timeoutPromise(..)` returns a Promise
//  that rejects after a specified delay

// setup a timeout for `foo()`
Promise.race( [
	foo(),					// attempt `foo()`
	timeoutPromise( 3000 )	// give it 3 seconds
] )
.then(
	function(){
		// `foo(..)` fulfilled in time!
	},
	function(err){
		// either `foo()` rejected, or it just
		// didn't finish in time, so inspect
		// `err` to know which
	}
);
```

### `Promise.resolve()`
Returns a `Promise` object that is resolved with the given value. If the value is a thenable or a Promise object (i.e. has a then method), the returned promise will "follow/unwrap" that thenable, adopting its eventual state; otherwise, the returned promise will be fulfilled with the value.

### Understanding the `Event Loop`
The event loop is a fundamental concept in JavaScript and is crucial for understanding how asynchronous code execution works in web development. Let's break down the event loop in detail:

1. **Single-threaded Nature:**
   JavaScript is single-threaded, meaning it has only one execution thread. This thread is responsible for executing the JavaScript code, and it does so sequentially, one statement at a time. This can become problematic when dealing with time-consuming tasks or operations that could potentially block the execution of other code.

2. **Blocking vs Non-blocking:**
   In a blocking operation, the program stops and waits for an external operation to finish before moving on. In contrast, non-blocking operations allow the program to continue executing other tasks while waiting for an operation to complete.

3. **Asynchronous JavaScript:**
   JavaScript employs an asynchronous programming model to handle potentially time-consuming operations without blocking the execution thread. Asynchronous operations are managed through a combination of callback functions, promises, and events.

4. **Event Queue:**
   The event queue is a data structure that holds events and their associated callback functions. Events can be user interactions (like clicks or keyboard input), network responses, timers, or other asynchronous operations.

5. **Event Loop:**
   The event loop is the mechanism that continually checks the event queue and processes events when the execution stack is empty. It ensures that asynchronous operations are handled in a non-blocking manner. The event loop follows these steps:

   - **Check the Execution Stack:** If the execution stack is empty, the event loop checks the event queue.

   - **Process Events:** If there are events in the queue, the event loop takes the first event and pushes its associated callback function onto the execution stack.

   - **Execute Callback:** The callback function is executed, and if it contains asynchronous operations (e.g., fetching data or setting a timer), those operations are initiated.

   - **Continue Looping:** The event loop repeats this process, continually checking for events and processing them as long as the execution stack remains empty.

6. **Callback Functions:**
   Callback functions are key to asynchronous programming in JavaScript. They are functions that are passed as arguments to other functions and are executed once a particular task is completed. For example, in event handling, a callback function is triggered when an event occurs.

Here's a simple example using a `setTimeout` function:

```javascript
console.log("Start");

setTimeout(function() {
    console.log("Inside setTimeout callback");
}, 2000);

console.log("End");
```

In this example, "Start" and "End" will be logged first, and then, after a 2-second delay, "Inside setTimeout callback" will be logged.

Asynchronous functionality like `setTimeout`, as well as other asynchronous operations such as making network requests (`fetch` or XMLHttpRequest), handling events (`addEventListener`), and working with promises, are not part of the JavaScript language itself. Instead, they are provided by the browser environment in which JavaScript is executed.

JavaScript engines, like V8 in Chrome or SpiderMonkey in Firefox, are responsible for executing JavaScript code in a single-threaded manner. However, the browser environment, which includes the Document Object Model (DOM), Web APIs, and the event loop, extends beyond the JavaScript engine and provides additional functionality to interact with the browser and perform asynchronous operations.

Here's a simplified overview of how asynchronous operations are typically handled in a browser environment:

1. **JavaScript Engine:**
   - Executes JavaScript code in a single thread.
   - Manages the execution stack and the event loop.

2. **Web APIs:**
   - Provide additional functionality beyond the core JavaScript language.
   - Examples include the DOM (Document Object Model) API, XMLHttpRequest, Fetch API, and Timer functions (`setTimeout`, `setInterval`).
   - These APIs are not part of the JavaScript language specification but are provided by the browser.

3. **Event Loop:**
   - Monitors the execution stack and the event queue.
   - When an asynchronous operation is initiated (e.g., `setTimeout`), the corresponding callback is moved to the event queue after the specified time.
   - The event loop picks up the callback from the event queue and executes it when the execution stack is empty.

So, while the JavaScript engine itself is single-threaded, the browser environment provides mechanisms for handling asynchronous operations and interacting with the broader web environment. Web APIs play a crucial role in enabling asynchronous behavior and extending the capabilities of JavaScript in a browser setting.

---
### Knowledge Check

**Q1.** What is a callback?

**A1.** A callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine or action.

The consumer of a callback-based API writes a function that is passed into the API. The provider of the API (called the caller) takes the function and calls back (or executes) the function at some point inside the caller's body. The caller is responsible for passing the right parameters into the callback function. The caller may also expect a particular return value from the callback function, which is used to instruct further behavior of the caller.

There are two ways in which the callback may be called: synchronous and asynchronous. Synchronous callbacks are called immediately after the invocation of the outer function, with no intervening asynchronous tasks, while asynchronous callbacks are called at some point later, after an asynchronous operation has completed.

Understanding whether the callback is synchronously or asynchronously called is particularly important when analyzing side effects. Consider the following example:

```js
let value = 1;

doSomething(() => {
  value = 2;
});

console.log(value);
```

If `doSomething` calls the callback synchronously, then the last statement would log `2` because `value = 2` is synchronously executed; otherwise, if the callback is asynchronous, the last statement would log `1` because `value = 2` is only executed after the `console.log` statement.

Examples of synchronous callbacks include the callbacks passed to `Array.prototype.map()`, `Array.prototype.forEach()`, etc. Examples of asynchronous callbacks include the callbacks passed to `setTimeout()` and `Promise.prototype.then()`.


**Q2.** What is a promise?

**A2.** In JavaScript, a "promise" refers to an object that represents the eventual completion or failure of an asynchronous operation and its resulting value. Promises are a part of the Promise API, which was introduced to handle asynchronous operations more effectively and improve the readability of asynchronous code.

A promise can be in one of three states:

1. **Pending:** The initial state; the promise is neither fulfilled nor rejected.
2. **Fulfilled:** The asynchronous operation completed successfully, and the promise has a resulting value.
3. **Rejected:** The asynchronous operation failed, and the promise has a reason for the failure.

The Promise API provides a clean and consistent way to work with asynchronous code, making it easier to manage complex asynchronous workflows. You can create a promise using the `Promise` constructor and chaining `.then()` and `.catch()` methods to handle the fulfillment or rejection of the promise.

Here's a basic example of using a promise in JavaScript:

```javascript
const myPromise = new Promise((resolve, reject) => {
  // Asynchronous operation
  const isSuccess = true;

  if (isSuccess) {
    resolve("Operation successful");
  } else {
    reject("Operation failed");
  }
});

myPromise
  .then((result) => {
    console.log("Fulfilled:", result);
  })
  .catch((error) => {
    console.error("Rejected:", error);
  });
```

In this example, the `myPromise` is either fulfilled with the message "Operation successful" or rejected with the message "Operation failed." The `.then()` method is used to handle fulfillment, and the `.catch()` method is used to handle rejection.

Promises are especially useful when dealing with asynchronous operations like fetching data from a server, reading a file, or handling events. They provide a more structured and readable way to work with asynchronous code compared to traditional callback patterns.

**Q3.** When should you use promises over callbacks?

**A3.** The Promise API aims to solve two major categories of deficiencies with using callbacks to express program asynchrony and manage concurrency: lack of sequentiality (non-linear nature of callbacks) and lack of trustability (the inversion of control).

One of the main problems with callbacks is that since we pass our callback function to the third party api to complete an async task, we have to trust that api will run the callback correctly. Promises fix this inversion of control. Instead of passing a callback to the third party api, we expect an promise object from the api which signals either the fullfillment or rejection of the async task. This way, we retain the control of execution of our callback function.

The other important problem with callbacks is that when we chain callbacks it creates this pyramid shape within our code, which is also referred as the callback hell. Within this callback hell, its hard to track what happens where. This lack of sequentiality within our code makes it harder to reason about our code, and track and fix possible bugs.

**Q4.** What does the .then() function do?

**A4.** The `Promise.prototype.then()` method is avaliable on every Promise instance. Every promise has to be resolved and be resolved only a single time. This resolution state can only have two values: fullfillment or rejection. The resolution value of the object is immutable. The`.then()` method takes two optional parameters: the first parameter is the callback for fullfillment, and the second parameter is the callback for rejection. When we call `.then()` on the Promise object, the fullfillment or rejection callback is executed depending on the resolution state of the Promise. `.then()` returns an another Promise instance.The resolution state of the returned promise from the `.then()` method is determined by the following rules:

1. **If the callback for fulfillment is invoked (first parameter of `.then()`):**
   - If the fulfillment callback returns a value, the returned promise is resolved with that value.
   - If the fulfillment callback returns a promise, the returned promise adopts the resolution state of that promise.
   - If the fulfillment callback throws an exception, the returned promise is rejected with the thrown exception.

2. **If the callback for rejection is invoked (second parameter of `.then()`):**
   - If the rejection callback returns a value, the returned promise is resolved with that value.
   - If the rejection callback returns a promise, the returned promise adopts the resolution state of that promise.
   - If the rejection callback throws an exception, the returned promise is rejected with the thrown exception.

3. **If no callback is provided (omitting either or both parameters):**
   - If the original promise is fulfilled, the returned promise is fulfilled with the same value.
   - If the original promise is rejected, the returned promise is rejected with the same reason.

In essence, the resolution state and value of the returned promise depend on the outcome of the callback functions provided in the `.then()` method. If no callbacks are provided, the returned promise simply adopts the resolution state and value of the original promise. This behavior enables chaining of `.then()` calls, allowing you to perform sequential asynchronous operations.

---
### Further Reading
+ [You Don't Know JS / Chapter 2: Callbacks](https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/async%20%26%20performance/ch2.md)
+ [You Don't Know JS / Chapter 3: Promises](https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/async%20%26%20performance/ch3.md)
+ [MDN Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)