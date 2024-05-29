# Recursion
Recursion is a programming concept in computer science where a function calls itself in order to solve a specific problem. In other words, a recursive function is a function that performs a task in part and delegates the remaining task to a new invocation of itself. This process continues until a base case is reached, at which point the function returns a result without making a recursive call.

The structure of a recursive function typically includes two components:

1. **Base Case:** This is the condition under which the function stops calling itself and returns a result. It prevents the recursion from continuing indefinitely.

2. **Recursive Case:** This is the part of the function where it calls itself with a modified set of parameters, typically moving closer to the base case. Each recursive call should make progress toward reaching the base case.

Here's a simple example of a recursive function in Python to calculate the factorial of a number:

```python
def factorial(n):
    # Base case
    if n == 0 or n == 1:
        return 1
    # Recursive case
    else:
        return n * factorial(n-1)
```

In this example, `factorial(n)` calls itself with a smaller argument (`n-1`) until it reaches the base case (`n == 0` or `n == 1`), at which point it returns 1. The final result is the product of all the numbers from 1 to `n`.

Recursion is a powerful and elegant technique, but it requires careful consideration of base cases to avoid infinite recursion and stack overflow errors. It is commonly used in algorithms like tree traversal, sorting (e.g., quicksort, mergesort), and various mathematical problems.

## Recursive Depth
"Recursive depth" refers to the level or depth of nested recursive calls in a program. In the context of recursion, each time a function calls itself, it goes one level deeper into the recursion. The depth of recursion is the measure of how many nested calls have been made.

Consider the following example of a simple recursive function in Python that calculates the factorial of a number:

```python
def factorial(n):
    if n == 0 or n == 1:
        return 1
    else:
        return n * factorial(n-1)
```

If you call `factorial(5)`, the recursive depth for this particular call would be 5. This is because the function makes five nested calls (`factorial(5)`, `factorial(4)`, `factorial(3)`, `factorial(2)`, and `factorial(1)`) before reaching the base case.

Understanding the recursive depth is important for analyzing the efficiency and potential resource usage of recursive algorithms. Each recursive call adds a new frame to the call stack, and a large recursive depth can lead to a stack overflow if not managed properly. It's crucial to have a proper base case and ensure that the recursion doesn't go too deep, especially in situations where there's a risk of exhausting the available stack space.

## Stack Overflow
The maximal recursion depth in JavaScript is limited by the JavaScript engine. Each function call consumes a certain amount of memory on the call stack, and there is a finite amount of stack space available. When a function is called, a new frame is added to the call stack, and when the function returns, the frame is removed.

If the recursion depth becomes too large and the call stack(the region of memory used for function call management) grows beyond the available stack space, it can lead to a **stack overflow**. A stack overflow occurs when the call stack exceeds its allocated size, and the program can't continue because there is no more space to store function call information.

In JavaScript, the specific maximum recursion depth depends on the JavaScript engine being used (e.g., V8 for Chrome, SpiderMonkey for Firefox, etc.) and the available stack space. If the recursion depth is too deep, it can result in a "Maximum call stack size exceeded" error. This error indicates that the JavaScript engine has detected a stack overflow and is preventing the program from causing a crash due to running out of stack space.

Here's a simple example in JavaScript that could lead to a stack overflow:

```javascript
function infiniteRecursion() {
  infiniteRecursion(); // Calling itself without a termination condition
}

// This will result in a stack overflow
infiniteRecursion();
```

In this example, the `infiniteRecursion` function keeps calling itself without any base case to stop the recursion, leading to a stack overflow error.

It's important to be mindful of recursion depth in recursive algorithms and ensure that it doesn't become excessively deep to avoid stack overflow errors. In some cases, iterative solutions or optimizations may be preferable to mitigate the risk of hitting the recursion depth limit.

## Recursive vs Iterative:
```js
function pow(x, n) {
  if (n == 1) {
    return x;
  } else {
    return x * pow(x, n - 1);
  }
}
```

Recursion depth equals the maximal number of context in the stack. Contexts take memory. In our case, raising to the power of n actually requires the memory for n contexts, for all lower values of n.

A loop-based algorithm is more memory-saving:

```js
function pow(x, n) {
  let result = 1;

  for (let i = 0; i < n; i++) {
    result *= x;
  }

  return result;
}
```

The iterative pow uses a single context, changing i and result in the process. Its memory requirements are small, fixed and do not depend on n.

**Any recursion can be rewritten as a loop. The loop variant usually can be made more effective.**

…But sometimes the rewrite is non-trivial, especially when a function uses different recursive subcalls depending on conditions and merges their results or when the branching is more intricate. Or the optimization may be unneeded and totally not worth the efforts.

Recursion can give a shorter code, easier to understand and support. Optimizations are not required in every place, mostly we need a good code, and that’s why it’s used.

## Recursive Traversal
Another great application of the recursion is a recursive traversal.

Imagine, we have a company. The staff structure can be presented as an object:

```js
let company = {
  sales: [{
    name: 'John',
    salary: 1000
  }, {
    name: 'Alice',
    salary: 1600
  }],

  development: {
    sites: [{
      name: 'Peter',
      salary: 2000
    }, {
      name: 'Alex',
      salary: 1800
    }],

    internals: [{
      name: 'Jack',
      salary: 1300
    }]
  }
};
```

In other words, a company has departments.

+ A department may have an array of staff. For instance, sales department has 2 employees: John and Alice.

+ Or a department may split into subdepartments, like development has two branches: sites and internals. Each of them has their own staff.

+ It is also possible that when a subdepartment grows, it divides into subsubdepartments (or teams).
For instance, the sites department in the future may be split into teams for siteA and siteB. And they, potentially, can split even more. That’s not on the picture, just something to have in mind.

Now let’s say we want a function to get the sum of all salaries. How can we do that?

An iterative approach is not easy, because the structure is not simple. The first idea may be to make a for loop over company with nested subloop over 1st level departments. But then we need more nested subloops to iterate over the staff in 2nd level departments like sites… And then another subloop inside those for 3rd level departments that might appear in the future? If we put 3-4 nested subloops in the code to traverse a single object, it becomes rather ugly.

Let’s try recursion.

As we can see, when our function gets a department to sum, there are two possible cases:

Either it’s a “simple” department with an array of people – then we can sum the salaries in a simple loop.
Or it’s an object with N subdepartments – then we can make N recursive calls to get the sum for each of the subdeps and combine the results.
The 1st case is the base of recursion, the trivial case, when we get an array.

The 2nd case when we get an object is the recursive step. A complex task is split into subtasks for smaller departments. They may in turn split again, but sooner or later the split will finish at (1).

The algorithm is probably even easier to read from the code:

```js
let company = { // the same object, compressed for brevity
  sales: [{name: 'John', salary: 1000}, {name: 'Alice', salary: 1600 }],
  development: {
    sites: [{name: 'Peter', salary: 2000}, {name: 'Alex', salary: 1800 }],
    internals: [{name: 'Jack', salary: 1300}]
  }
};

// The function to do the job
function sumSalaries(department) {
  if (Array.isArray(department)) { // case (1)
    return department.reduce((prev, current) => prev + current.salary, 0); // sum the array
  } else { // case (2)
    let sum = 0;
    for (let subdep of Object.values(department)) {
      sum += sumSalaries(subdep); // recursively call for subdepartments, sum the results
    }
    return sum;
  }
}

alert(sumSalaries(company)); // 7700
```

While recursion has its advantages, it's important to consider potential downsides, such as increased memory usage due to the function call stack. In some cases, an iterative approach might be preferred for performance reasons or to avoid stack overflow issues.

## Recursive Structures
A recursive (recursively-defined) data structure is a structure that replicates itself in parts.

We’ve just seen it in the example of a company structure above.

A company department is:
+ Either an array of people.
+ Or an object with departments.

For web-developers there are much better-known examples: HTML and XML documents.

In the HTML document, an HTML-tag may contain a list of:

+ Text pieces.
+ HTML-comments.
+ Other HTML-tags (that in turn may contain text pieces/comments or other tags etc).

That’s once again a recursive definition.

For better understanding, we’ll cover one more recursive structure named “Linked list” that might be a better alternative for arrays in some cases.

### Linked List
Imagine, we want to store an ordered list of objects.

The natural choice would be an array:

```js
let arr = [obj1, obj2, obj3];
```

…But there’s a problem with arrays. The “delete element” and “insert element” operations are expensive. For instance, arr.unshift(obj) operation has to renumber all elements to make room for a new obj, and if the array is big, it takes time. Same with arr.shift().

The only structural modifications that do not require mass-renumbering are those that operate with the end of array: arr.push/pop. So an array can be quite slow for big queues, when we have to work with the beginning.

Alternatively, if we really need fast insertion/deletion, we can choose another data structure called a linked list.

The linked list element is recursively defined as an object with:

+ value.
+ next property referencing the next linked list element or null if that’s the end.

```js
// Definition of a node in a linked list
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

// Recursive linked list
function createLinkedList(arr) {
  if (arr.length === 0) {
    return null;
  }

  const node = new Node(arr[0]);
  node.next = createLinkedList(arr.slice(1));
  return node;
}

// Usage
const myList = createLinkedList([1, 2, 3, 4, 5]);
```

In this example, the Node class defines a node in the linked list, and the createLinkedList function recursively constructs the linked list from an array.

## Let's remember how the memory (RAM) is managed by the runtime engines
Ythe call stack manages the execution of functions and keeps track of their local variables, while the heap is used for dynamic memory allocation to store objects and variables with a longer lifespan. These two components work together to manage memory effectively during the execution of a JavaScript program.

1. **Call Stack:** The call stack is a region of memory that keeps track of the execution of functions in a program. It operates in a Last In, First Out (LIFO) manner, meaning that the last function called is the first one to be resolved. As functions are called, their information, such as local variables and the return address, is pushed onto the stack. When a function completes its execution, its information is popped off the stack. This mechanism is crucial for managing the flow of control and memory for function calls.

2. **Heap:** The heap is a larger region of memory that is used for dynamic memory allocation. It is where objects and variables are stored, and memory is allocated and deallocated during the runtime of a program. Objects and variables in the heap can persist beyond the scope of a single function call. Memory management in the heap is typically handled by the runtime environment, and languages like JavaScript have automatic garbage collection to reclaim memory occupied by objects that are no longer needed.

When dealing with asynchronous operations in JavaScript, such as those handled by async functions, an additional component comes into play: the Event Loop and the Task Queue.

Here's a breakdown of how these components work together:

1. **Call Stack:** The call stack, as mentioned earlier, keeps track of the execution of synchronous code, managing the flow of function calls.

2. **Heap:** The heap stores objects and variables.

3. **Event Loop:** The event loop is a continuous process that constantly checks the call stack for any synchronous code to execute. If the call stack is empty, it looks at the task queue for asynchronous tasks that need to be moved to the call stack.

4. **Task Queue (Event Queue):** The task queue is where asynchronous tasks, such as callbacks from `setTimeout`, network requests, or resolved promises in async functions, are placed after their completion. These tasks are then processed by the event loop when the call stack is empty.

So, when an async function is executed, and it encounters an asynchronous operation (e.g., `setTimeout`, a promise), the associated callback is not immediately executed and placed on the call stack. Instead, it gets pushed into the task queue.

The event loop constantly checks if the call stack is empty. If it is, it takes tasks from the task queue and moves them to the call stack for execution. This mechanism allows asynchronous operations to be handled without blocking the main thread.

In summary, the task queue is where asynchronous tasks are stored until the event loop processes them and moves them to the call stack for execution. By using the task queue and the event loop, JavaScript is able to handle asynchronous operations in a non-blocking manner, allowing the program to remain responsive and efficient. This is a key aspect of the single-threaded, non-blocking nature of JavaScript, which relies on event-driven programming.

---
### Knowledge Check

**Q1.** How would you briefly define a recursive function?

**A1.** In it's essence, a recursive function is just a function that calls itself.

**Q2.** What is the point of recursion? Is it more efficient than using a plain loop?

**A2.** Recursion is often used to write code in a more understandable, simple and elegant way. Generally, recursion is not as efficient as a for loop for example, because recursion(calling the function again and again) creates a new execution context and fills up the callstack. This process costs both memory/space and time. A loop on the other hand, executes the function in a single execution context and only changes the local variables of the loop. Having said that, some problems are solved much more easily with recursion than loops. For example, if we have an object which has several deeply nested objects inside it, when looking a particular value in that object, recursion is usually a better solution than iteration/loops. Because creating loops nested deeper than 2 layers gets quickly confusing, and since we might not know how deep the object gets, the iteration solution gets more complex than the recursive one.

**Q3.** What are the 2 essential parts in a recursive function?

**A3.** A recursive function has 2 essential parts:

1. **Base Case:** This is the condition under which the function stops calling itself and returns a result. It prevents the recursion from continuing indefinitely.

2. **Recursive Case:** This is the part of the function where it calls itself with a modified set of parameters, typically moving closer to the base case. Each recursive call should make progress toward reaching the base case.

**Q4.** Why is “stack overflow” relevant to a recursive problem?

**A4.** With recursion, everytime the recursive function calls itself, javascript engine creates a new execution context and pushes it to the callstack. Since our memory is a finite source, javascript engines are designed with a top limit of calls that can be placed on the callstack. For example, if we forget to include a base case in our recursive function and the function tries to call itself indefinitely, at some point the limit of avaliable space in the callstack will be reached. In that case, the javascript engine will throw a "stack overflow" error, and stop the execution of the script.