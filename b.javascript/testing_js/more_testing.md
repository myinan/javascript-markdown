An important basic concept in testing is isolation. You should only test one method at a time, and your tests for one function should not depend upon an external function behaving correctly - especially if that function is being tested elsewhere. The main reason for this is that when your tests fail, you want to be able to narrow down the cause of this failure as quickly as possible. If you have a test that depends on several functions, it can be hard to tell exactly what is going wrong.

## Tightly-Coupled Code
"Tightly coupled code" refers to a programming paradigm where components or modules within a software system are highly dependent on each other. In other words, changes to one part of the code are likely to affect other parts, making the system less flexible, harder to maintain, and more prone to errors. This can lead to a lack of modularity, making it difficult to isolate and update individual components without affecting the entire system.

In the context of JavaScript, tight coupling can manifest in various ways:

1. **Direct Dependencies:**
   Components directly reference each other, creating a direct dependency. For example, one JavaScript file might reference variables or functions defined in another file.

   ```javascript
   // Module A
   function doSomething() {
       // ...
   }

   // Module B
   doSomething(); // directly referencing the function from Module A
   ```

   In this example, Module B is tightly coupled to Module A because it directly calls the `doSomething` function from Module A.

2. **Shared State:**
   Components share state variables or global variables, making them interdependent. This can lead to unexpected side effects if one component modifies shared state in a way that affects another component.

   ```javascript
   // Module A
   let sharedVariable = 0;

   // Module B
   function updateSharedVariable() {
       sharedVariable++;
   }
   ```

   Here, Module B is tightly coupled to Module A because it relies on and modifies the shared state variable.

3. **Implicit Dependencies:**
   Dependencies are not clearly defined or documented, making it challenging to understand how different modules interact. This can occur when modules rely on implicit assumptions about the environment.

   ```javascript
   // Module A
   function getData() {
       return fetch('/api/data').then(response => response.json());
   }

   // Module B
   getData().then(data => console.log(data));
   ```

   Module B is tightly coupled to the assumption that `getData` fetches data from a specific API endpoint. If the endpoint changes, Module B will break.

To address tight coupling and promote a more modular and maintainable codebase in JavaScript:

- **Use Encapsulation:**
  Encapsulate functionality within modules, exposing only what is necessary and hiding implementation details.

- **Adopt Dependency Injection:**
  Pass dependencies explicitly as parameters or use a dependency injection mechanism to decouple components.

- **Event-Driven Architecture:**
  Use events and callbacks to communicate between modules instead of direct function calls, reducing direct dependencies.

- **Utilize Design Patterns:**
  Apply design patterns like the Module Pattern, Observer Pattern, or Dependency Injection to structure code in a more decoupled manner.

By reducing tight coupling in your JavaScript code, you improve code maintainability, scalability, and flexibility. It becomes easier to modify or extend specific parts of the codebase without affecting the entire system.

### Use Encapsulation
Encapsulation is a fundamental concept in object-oriented programming that involves bundling data (variables) and the methods (functions) that operate on the data into a "single unit" such as class, function or object.

Here's an example of how encapsulation works in the context of JavaScript:

1. **Define a Module:**
   A module is a self-contained unit that groups related functionality. It can be implemented using functions or objects. The goal is to keep the internal details of the module hidden from the outside world.

   ```javascript
   // Module definition using a function
   function Calculator() {
       // private variable
       let result = 0;

       // private function
       function add(a, b) {
           result = a + b;
       }

       // public function (exposed to the outside)
       this.addAndReturn = function (a, b) {
           add(a, b);
           return result;
       };
   }

   // Creating an instance of the Calculator module
   const calculator = new Calculator();
   ```

   In this example, `Calculator` is a module that encapsulates the logic of addition. The internal details (like the `result` variable and the `add` function) are hidden from external code.

2. **Expose Only Necessary Functionality:**
   The module exposes only those functions or variables that are necessary for external code to interact with it. In the example above, only the `addAndReturn` function is exposed, allowing users of the module to perform addition without directly manipulating the internal state.

   ```javascript
   // Using the Calculator module
   const result = calculator.addAndReturn(3, 4);
   console.log(result); // Outputs: 7
   ```

   External code interacts with the module through the public interface (`addAndReturn`), and it doesn't have direct access to the internal workings of the module.

3. **Hide Implementation Details:**
   Encapsulation involves hiding the implementation details of a module, making it easier to change the internal structure without affecting the external code.

   ```javascript
   // Modified Calculator module with a different internal implementation
   function Calculator() {
       let result = 0;

       function multiply(a, b) {
           result = a * b;
       }

       this.multiplyAndReturn = function (a, b) {
           multiply(a, b);
           return result;
       };
   }

   // External code remains unaffected
   const calculator = new Calculator();
   const newResult = calculator.multiplyAndReturn(3, 4);
   console.log(newResult); // Outputs: 12
   ```

   Even though the internal implementation has changed (now the module handles multiplication), external code that uses the public interface (`multiplyAndReturn`) doesn't need to be modified.

Encapsulation helps in creating more modular and maintainable code by providing a clear separation between a module's internal implementation and its external interface. It reduces the likelihood of unintended interactions between different parts of the code and makes it easier to update or extend the functionality of a module without affecting the rest of the application.

### Adopt Dependency Injection
Dependency Injection (DI) is a design pattern that promotes loose coupling between components in a software system. The idea is to pass the dependencies that a component needs from the outside, rather than letting the component create or manage its dependencies internally. This makes the code more modular, testable, and easier to maintain. In JavaScript, you can implement dependency injection through explicit parameter passing or by using a dedicated DI container.

Let's explore both approaches:

1. **Explicit Parameter Passing:**
   In this approach, a component explicitly receives its dependencies as parameters when it is created or when a method is called. This makes the dependencies transparent and allows for better control and flexibility.

   ```javascript
   // Without Dependency Injection
   function createOrder() {
       const paymentProcessor = new PaymentProcessor();
       const order = new Order(paymentProcessor);
       order.process();
   }

   // With Dependency Injection
   function createOrder(paymentProcessor) {
       const order = new Order(paymentProcessor);
       order.process();
   }

   // Usage
   const paymentProcessor = new PaymentProcessor();
   createOrder(paymentProcessor);
   ```

   In the example without dependency injection, the `createOrder` function creates a new `PaymentProcessor` instance internally. In the example with dependency injection, the `PaymentProcessor` instance is passed as a parameter, allowing external code to provide different implementations.

2. **Dependency Injection Container:**
   A Dependency Injection Container is a mechanism that manages and provides instances of dependencies to components. It centralizes the configuration of dependencies, making it easier to change or replace implementations. While there are dedicated DI containers available for JavaScript frameworks, you can also create a simple container using plain JavaScript.

   ```javascript
   // Dependency Injection Container
   class DependencyContainer {
       constructor() {
           this.instances = {};
       }

       register(name, instance) {
           this.instances[name] = instance;
       }

       resolve(name) {
           if (!(name in this.instances)) {
               throw new Error(`Dependency not registered: ${name}`);
           }
           return this.instances[name];
       }
   }

   // Usage
   const container = new DependencyContainer();

   // Register dependencies
   container.register('paymentProcessor', new PaymentProcessor());
   container.register('orderProcessor', new OrderProcessor());

   // Resolve dependencies
   const paymentProcessor = container.resolve('paymentProcessor');
   const orderProcessor = container.resolve('orderProcessor');

   // Use dependencies
   const order = new Order(paymentProcessor, orderProcessor);
   order.process();
   ```

   In this example, the `DependencyContainer` registers and resolves instances of dependencies. External code can register different implementations, and components can retrieve dependencies from the container, reducing the need for direct instantiation within the component.

By adopting dependency injection, you achieve the following benefits:

- **Decoupling:** Components become independent of how their dependencies are created, promoting better separation of concerns.
  
- **Testability:** It becomes easier to mock or substitute dependencies during testing, facilitating unit testing.

- **Flexibility:** You can change or update dependencies without modifying the dependent components, making the codebase more adaptable to change.

- **Readability:** Dependencies are explicitly defined in the component's interface, making the code more readable and self-documenting.

### Event-Driven Architecture
Event-Driven Architecture (EDA) is a design pattern where components or modules communicate with each other through events and callbacks. In an event-driven system, components are decoupled, meaning they are not directly aware of each other. Instead, they communicate by triggering and responding to events. This promotes a more flexible and loosely-coupled architecture.

Here's how you can implement an Event-Driven Architecture in JavaScript:

1. **Event Emitter:**
   Start by creating an event emitter or a centralized event manager. This can be a simple custom implementation or you can use existing libraries like Node.js's `EventEmitter` or third-party libraries like `EventEmitter2`.

   ```javascript
   // Event Emitter
   class EventEmitter {
       constructor() {
           this.events = {};
       }

       on(eventName, callback) {
           this.events[eventName] = this.events[eventName] || [];
           this.events[eventName].push(callback);
       }

       emit(eventName, data) {
           const callbacks = this.events[eventName];
           if (callbacks) {
               callbacks.forEach(callback => callback(data));
           }
       }
   }

   // Usage
   const emitter = new EventEmitter();

   // Module A
   emitter.on('someEvent', data => {
       console.log(`Module A received data: ${data}`);
   });

   // Module B
   emitter.on('someEvent', data => {
       console.log(`Module B received data: ${data}`);
   });

   // Triggering the event
   emitter.emit('someEvent', 'Hello, Event-Driven Architecture!');
   ```

   In this example, `Module A` and `Module B` register callback functions using the `on` method of the event emitter. When the event is triggered with `emit`, both modules receive and process the event.

2. **Reduced Direct Dependencies:**
   By using events and callbacks, modules don't directly call each other's functions. Instead, they communicate through the shared event emitter. This reduces the direct dependencies between modules, making the system more modular and easier to maintain.

   ```javascript
   // Module A
   emitter.on('calculate', (a, b) => {
       const result = a + b;
       emitter.emit('calculationResult', result);
   });

   // Module B
   emitter.on('calculationResult', result => {
       console.log(`Module B received result: ${result}`);
   });

   // Triggering the calculation
   emitter.emit('calculate', 3, 4);
   ```

   In this example, `Module A` triggers a calculation event, and `Module B` responds to the calculation result event. The modules are decoupled from each other, as `Module A` doesn't need to directly call a function in `Module B`.

3. **Dynamic Component Interaction:**
   Events allow for dynamic interaction between components. New modules can be added or removed without affecting the existing modules, as long as they adhere to the agreed-upon event contract.

   ```javascript
   // New Module C added dynamically
   emitter.on('calculationResult', result => {
       console.log(`Module C received result: ${result}`);
   });

   // Triggering the calculation
   emitter.emit('calculate', 5, 2);
   ```

   In this case, adding `Module C` dynamically doesn't require changes to `Module A` or `Module B`. It simply subscribes to the existing event and participates in the system.

By adopting an Event-Driven Architecture, you achieve the following benefits:

- **Loose Coupling:** Modules are loosely coupled, as they communicate through events rather than direct function calls.

- **Flexibility:** New modules can be added or removed without affecting existing modules, promoting a more flexible and extensible system.

- **Readability:** The flow of events provides a clear and readable way to understand how different components interact within the system.

- **Testability:** Components can be easily tested in isolation by mocking or stubbing the event emitter.

Event-Driven Architecture is particularly useful in scenarios where components need to communicate asynchronously or when you want to create a modular system that can easily accommodate changes and extensions.

### Utilize Design Patterns
Design patterns are proven solutions to recurring problems in software design. They provide general templates for solving common architectural challenges, and their application can lead to more maintainable, scalable, and flexible code. Here's an explanation of how you can utilize some design patterns—specifically, the Module Pattern, Observer Pattern, and Dependency Injection—to structure code in a more decoupled manner in JavaScript:

1. **Module Pattern:**
   The Module Pattern is a way to encapsulate private and public members of a module, providing a clear structure for organizing code. It promotes encapsulation and reduces the likelihood of naming conflicts. In JavaScript, this pattern is often implemented using closures.

   ```javascript
   // Module Pattern Example
   const CalculatorModule = (function () {
       // private variable
       let result = 0;

       // private function
       function add(a, b) {
           result = a + b;
       }

       // public interface
       return {
           addAndReturn: function (a, b) {
               add(a, b);
               return result;
           }
       };
   })();

   // Usage
   const sum = CalculatorModule.addAndReturn(3, 4);
   console.log(sum); // Outputs: 7
   ```

   In this example, the `CalculatorModule` encapsulates its internal state and logic, exposing only the `addAndReturn` function as the public interface.

2. **Observer Pattern:**
   The Observer Pattern is used to establish a one-to-many dependency between objects, where one object (the subject) maintains a list of dependents (observers) that are notified of state changes. This pattern is useful for implementing event handling systems.

   ```javascript
   // Observer Pattern Example
   class Subject {
       constructor() {
           this.observers = [];
       }

       addObserver(observer) {
           this.observers.push(observer);
       }

       notifyObservers(data) {
           this.observers.forEach(observer => observer.update(data));
       }
   }

   class Observer {
       update(data) {
           console.log(`Received data: ${data}`);
       }
   }

   // Usage
   const subject = new Subject();
   const observerA = new Observer();
   const observerB = new Observer();

   subject.addObserver(observerA);
   subject.addObserver(observerB);

   subject.notifyObservers('Hello, Observer Pattern!');
   ```

   In this example, `Subject` maintains a list of observers (`observerA` and `observerB`), and when `notifyObservers` is called, each observer is notified of the data change.

3. **Dependency Injection:**
   Dependency Injection involves passing dependencies explicitly to components, reducing their direct dependencies on specific implementations. This pattern helps in achieving loose coupling and making the code more testable.

   ```javascript
   // Dependency Injection Example
   class Logger {
       log(message) {
           console.log(message);
       }
   }

   class OrderProcessor {
       constructor(logger) {
           this.logger = logger;
       }

       processOrder(order) {
           // Processing logic
           this.logger.log('Order processed successfully');
       }
   }

   // Usage
   const logger = new Logger();
   const orderProcessor = new OrderProcessor(logger);

   orderProcessor.processOrder({ /* order data */ });
   ```

   In this example, the `OrderProcessor` class depends on a `Logger`. Instead of creating a `Logger` instance internally, the dependency is injected through the constructor. This makes it easy to replace the `Logger` or mock it during testing.

By applying these design patterns, you enhance the modularity, maintainability, and flexibility of your JavaScript code. Each pattern addresses specific concerns, and their combination can lead to well-structured, decoupled systems. Understanding when and how to apply these patterns depends on the specific requirements and challenges of your application.

## Loosely-Coupled Code
Loosely-coupled code refers to a design principle in software development where the components or modules of a system are designed to have minimal dependencies on each other. In a loosely-coupled system, changes to one component have little to no impact on other components, promoting flexibility, maintainability, and ease of modification.

Key characteristics of loosely-coupled code include:

1. **Reduced Direct Dependencies:**
   Loosely-coupled code minimizes direct dependencies between components. Components communicate through well-defined interfaces or protocols rather than relying on direct function calls or tight integrations.

2. **High Modularity:**
   The system is structured into modular components, each responsible for a specific functionality. These modules are designed to be independent and self-contained, making it easier to understand, maintain, and extend the codebase.

3. **Encapsulation:**
   Components encapsulate their internal implementation details, exposing only what is necessary through well-defined interfaces. This reduces the likelihood of unintended interactions between different parts of the code.

4. **Flexibility and Extensibility:**
   Loosely-coupled systems are more adaptable to change. Adding, removing, or modifying components can be done with minimal impact on the rest of the system. New features or functionalities can be introduced without affecting existing code.

5. **Testability:**
   Loosely-coupled code is typically more testable. Unit testing becomes easier because components can be isolated and tested independently. Mocking or substituting dependencies for testing purposes is also more straightforward.

6. **Event-Driven Communication:**
   Loosely-coupled systems often utilize event-driven communication patterns, where components communicate through events and callbacks. This reduces direct dependencies and allows for dynamic interactions between components.

7. **Dependency Injection:**
   The use of dependency injection further reduces direct dependencies by passing dependencies explicitly rather than creating them internally. This promotes a more modular and testable design.

Loosely-coupled code is essential for building robust and maintainable software systems, particularly in large and complex projects. It enables teams to work on different parts of the system independently, reduces the risk of unintended side effects when making changes, and enhances the overall agility of the software development process. Design patterns and architectural principles, such as those mentioned earlier (Module Pattern, Observer Pattern, Dependency Injection, and Event-Driven Architecture), contribute to achieving loosely-coupled code by providing structured approaches to code organization and communication between components.

## Pure Functions
A pure function is a concept in functional programming that describes a function with two main characteristics:

1. **Deterministic:**
   A pure function, given the same set of input parameters, will always produce the same output. There are no hidden or external factors that can affect the result. The function's behavior is entirely determined by its inputs.

2. **No Side Effects:**
   A pure function does not have side effects. Side effects refer to any observable changes made outside the function's scope, such as modifying a global variable, modifying a mutable input parameter, or performing I/O operations like writing to a file or making network requests.

   Having said that, side effects themselves are not bad and are often required. Except, for a function to be declared pure it must not contain any. Not all functions need to be, or should be, pure.

   Side effects include, but are not limited to:

    + Making a HTTP request
    + Mutating data
    + Printing to a screen or console
    + DOM Query/Manipulation
    + Math.random()
    + Getting the current time

Pure functions have several benefits:

- **Predictability:** Because pure functions produce the same output for the same input, they are predictable and easy to reason about. This makes code more reliable and less error-prone.

- **Testability:** Since pure functions don't rely on external state or have side effects, they are easy to test. Unit testing is straightforward because you can isolate the function and assert the expected output based on different inputs.

- **Parallelization:** Pure functions are inherently thread-safe and can be executed in parallel without concerns about shared state or synchronization issues.

- **Memoization:** Pure functions are suitable candidates for memoization, a technique where the results of expensive function calls are cached based on their input parameters to improve performance.

Here's an example of a pure function:

```javascript
// Pure Function Example
function add(a, b) {
    return a + b;
}

const result1 = add(3, 4); // Outputs: 7
const result2 = add(3, 4); // Outputs: 7 (same input, same output)
```

In this example, the `add` function takes two parameters and returns their sum. It is deterministic because calling it with the same inputs will always produce the same result, and it has no side effects because it doesn't modify any external state.

Contrast this with an impure function that has side effects:

```javascript
// Impure Function Example
let total = 0;

function addToTotal(value) {
    total += value;
}

addToTotal(5);
console.log(total); // Outputs: 5 (observable side effect)
```

In this example, the `addToTotal` function modifies the external variable `total`, making it impure because it has a side effect that can be observed outside the function's scope.

Not all functions need to be , or should be, pure. For example, an event handler for a button press that manipulates the DOM is not a good candidate for a pure function. But, the event handler can call other pure functions which will reduce the number of impure functions in your application.

## Pure Functions and Testability
One of the major benefits of using pure functions is they are immediately testable. They will always produce the same result if you pass in the same arguments.

They also makes maintaining and refactoring code much easier. You can change a pure function and not have to worry about unintended side effects messing up the entire application and ending up in debugging hell.

Pure functions align well with the principles of TDD, providing the following advantages:

1. **Isolation for Testing:**
   Pure functions are isolated from external state and side effects, making them easy to test in isolation. This isolation simplifies the process of creating unit tests because you can focus on testing the function's behavior based on input and output without worrying about external dependencies.

2. **Deterministic Testing:**
   Pure functions are deterministic, meaning they produce the same output for the same input. This predictability is crucial in TDD, as it allows you to write tests with specific expected outcomes. Deterministic functions make it easier to reason about the behavior of the code and ensure that tests are reliable.

3. **Easy Mocking and Stubbing:**
   Because pure functions don't rely on external state or global variables, it's straightforward to use mocking or stubbing techniques during testing. Mocking external dependencies becomes unnecessary, and you can provide controlled inputs to the function without worrying about unexpected interactions.

4. **Facilitates Test Refactoring:**
   TDD often involves refactoring code while ensuring that the tests remain valid. Pure functions, being isolated and free from side effects, make refactoring easier. You can confidently make changes to the function's internals, knowing that as long as the input-output contract remains the same, the tests will continue to accurately reflect the function's behavior.

5. **Parallel Test Execution:**
   Pure functions are inherently thread-safe, as they don't rely on shared mutable state. This property makes it easier to run tests in parallel, improving test suite performance.

6. **Promotes Unit Testing:**
   TDD encourages a focus on unit tests, which test individual components in isolation. Pure functions naturally fit into this paradigm, allowing you to create meaningful and thorough unit tests for specific pieces of functionality.

Here's an example to illustrate testing a pure function using TDD:

```javascript
// Pure Function Example
function add(a, b) {
    return a + b;
}

// TDD Test Case
const assert = require('assert');

// Test Case 1
const result1 = add(3, 4);
assert.strictEqual(result1, 7, 'Test Case 1 failed');

// Test Case 2
const result2 = add(-2, 5);
assert.strictEqual(result2, 3, 'Test Case 2 failed');

// ...
```

In this example, tests are written for the `add` function, ensuring that it behaves as expected for different input values. The pure nature of the function simplifies the testing process, allowing for focused unit tests and making it easier to maintain the test suite as the code evolves.

## Mocking
In the context of testing with Jest, "mocking" refers to the practice of replacing a function or module with a fake implementation during the test execution. The purpose of mocking is to isolate the code being tested and control its behavior in order to focus on specific scenarios and ensure predictable and reliable test results.

Jest provides a built-in mocking system that allows you to create mock functions, mock modules, and control their behavior. Here are some common use cases for mocking in Jest:

1. **Mock Functions:** You can create mock functions to replace actual functions in your code. This is useful for testing how a function is called, with what arguments, and what it returns.

   ```javascript
   const myFunction = jest.fn();
   myFunction.mockReturnValue(42);

   // Now use `myFunction` in your code, and it will return 42 during tests
   ```

2. **Mock Modules:** You can mock entire modules to simulate their behavior without actually executing the real code. This is helpful when you want to isolate the code under test from external dependencies.

   ```javascript
   jest.mock('./myModule');

   // Now any import of './myModule' in your code will be replaced with a mock
   ```

3. **Control Side Effects:** Mocking allows you to control side effects such as API calls or database interactions. You can replace actual implementations with mock functions that return predefined values or simulate specific behaviors.

   ```javascript
   const fetchData = jest.fn(() => Promise.resolve('Mocked data'));

   // Replace the actual fetchData function with the mock during testing
   ```

4. **Spying on Function Calls:** You can use Jest's mocking capabilities to spy on function calls, track how many times a function is called, and check the arguments passed to it.

   ```javascript
   const myFunction = jest.fn();

   // Use myFunction in your code, and then check its usage in the test
   expect(myFunction).toHaveBeenCalledTimes(1);
   expect(myFunction).toHaveBeenCalledWith('someArg');
   ```

By using mocking in Jest, you can create controlled environments for testing and ensure that your tests focus on specific aspects of your code, leading to more robust and maintainable test suites.

## Composition and Mocking in Testing
### What does composition have to do with mocking?
Everything. The essence of all software development is the process of breaking a large problem down into smaller, independent pieces (decomposition) and composing the solutions together to form an application that solves the large problem (composition).

**Mocking is required when our decomposition strategy has failed.**

Mocking is required when the units used to break the large problem down into smaller parts depend on each other. Put another way, mocking is required when our supposed atomic units of composition are not really atomic, and our decomposition strategy has failed to decompose the larger problem into smaller, independent problems.

When decomposition succeeds, it’s possible to use a generic composition utility to compose the pieces back together. Examples:

+ Function composition e.g., lodash/fp/compose
+ Component composition e.g., composing higher-order components with function composition
+ State store/model composition e.g., Redux combineReducers
+ Object or factory composition e.g., mixins or functional mixins
+ Process composition e.g., transducers
+ Promise or monadic composition e.g., asyncPipe(), Kleisli composition with composeM(), composeK(), etc...

When you use generic composition utilities, each element of the composition can be unit tested in isolation without mocking the others.

The compositions themselves will be **declarative**, so they’ll contain zero unit-testable logic (presumably the composition utility is a third party library with its own unit tests).

Under those circumstances, there’s nothing meaningful to unit test. You need integration tests, instead.

Let’s contrast imperative vs declarative composition using a familiar example:


```js
// Function composition OR
// import pipe from 'lodash/fp/flow';
const pipe = (...fns) => x => fns.reduce((y, f) => f(y), x);
// Functions to compose
const g = n => n + 1;
const f = n => n * 2;
// Imperative composition
const doStuffBadly = x => {
  const afterG = g(x);
  const afterF = f(afterG);
  return afterF;
};
// Declarative composition
const doStuffBetter = pipe(g, f);
console.log(
  doStuffBadly(20), // 42
  doStuffBetter(20) // 42
);
```

Function composition is the process of applying a function to the return value of another function. In other words, you create a pipeline of functions, then pass a value to the pipeline, and the value will go through each function like a stage in an assembly line, transforming the value in some way before it’s passed to the next function in the pipeline. Eventually, the last function in the pipeline returns the final value.

initialValue -> [g] -> [f] -> result

You can compose functions manually (imperatively), or automatically (declaratively). In languages without first-class functions, you don’t have much choice. You’re stuck with imperative. In JavaScript (and almost all the other major popular languages), you can do it better with declarative composition.

Imperative style means that we’re commanding the computer to do something step-by-step. It’s a how-to guide. In the example above, the imperative style says:

1. Take an argument and assign it to x
2. Create a binding called afterG and assign the result of g(x) to it
3. Create a binding called afterF and assign the result of f(afterG) to it
4. Return the value of afterF.

The imperative style version requires logic that should be tested. I know those are just simple assignments, but I’ve frequently seen (and written) bugs where I pass or return the wrong variable.

Declarative style means we’re telling the computer the relationships between things. It’s a description of structure using equational reasoning. The declarative example says:

	doStuffBetter is the piped composition of g and f.

That’s it.

Assuming f and g have their own unit tests, and pipe() has its own unit tests (use flow() from Lodash or pipe() from Ramda, and it will), there's no new logic here to unit test.

**In order for this style to work correctly, the units we compose need to be decoupled.**

### How do we remove coupling?
To remove coupling, we first need a better understanding of where coupling dependencies come from. Here are the main sources, roughly in order of how tight the coupling is:

Tight coupling:

+ Class inheritance (coupling is multiplied by each layer of inheritance and each descendant class)
+ Global variables
+ Other mutable global state (browser DOM, shared storage, network, etc…)
+ Module imports with side-effects
+ Implicit dependencies from compositions, e.g., const enhancedWidgetFactory = compose(eventEmitter, widgetFactory, enhancements); where widgetFactory depends on eventEmitter
+ Dependency injection containers
+ Dependency injection parameters
+ Control parameters (an outside unit is controlling the subject unit by telling it what to do)
+ Mutable parameters

Loose coupling:

+ Module imports without side-effects (in black box testing, not all imports need isolating)
+ Message passing/pubsub
+ Immutable parameters (can still cause shared dependencies on state shape)

Ironically, most of the sources of coupling are mechanisms originally designed to reduce coupling. That makes sense, because in order to recompose our smaller problem solutions into a complete application, they need to integrate and communicate somehow. There are good ways, and bad ways. The sources that cause tight coupling should be avoided whenever it’s practical to do so. The loose coupling options are generally desirable in a healthy application.

You might be confused that I classified dependency injection containers and dependency injection parameters in the “tight coupling” group, when so many books and blog post categorize them as “loose coupling”. Coupling is not binary. It’s a gradient scale. That means that any grouping is going to be somewhat subjective and arbitrary.

I draw the line with a simple, objective litmus test:

**Can the unit be tested without mocking dependencies? If it can’t, it’s tightly coupled to the mocked dependencies.**

The more dependencies your unit has, the more likely it is that there may be problematic coupling. Now that we understand how coupling happens, what can we do about it?

+ Use pure functions as the atomic unit of composition, as opposed to classes, imperative procedures, or mutating functions.
+ Isolate side-effects from the rest of your program logic. That means don’t mix logic with I/O (including network I/O, rendering UI, logging, etc…).
+ Remove dependent logic from imperative compositions so that they can become declarative compositions which don’t need their own unit tests. If there’s no logic, there’s nothing meaningful to unit test.

That means that the code you use to set up network requests and request handlers won’t need unit tests. Use integration tests for those, instead.

That bears repeating: Don’t unit test I/O. I/O is for integrations. Use integration tests, instead.

It’s perfectly OK to mock and fake for integration tests.

### Use pure functions
Using pure functions takes a little practice, and without that practice, it’s not always clear how to write a pure function to do what you want to do. Pure functions can’t directly mutate global variables, the arguments passed into them, the network, the disk, or the screen. All they can do is return a value.

If you’re passed an array or an object, and you want to return a changed version of that object, you can’t just make the changes to the object and return it. You have to create a new copy of the object with the required changes.

### Isolate side-effects from the rest of your program logic
1. Use pub/sub to decouple I/O from views and program logic. Rather than directly triggering side-effects in UI views or program logic, emit an event or action object describing an event or intent.

2. Isolate logic from I/O e.g., compose functions which return promises using asyncPipe().


#### Use pub/sub
Pub/sub is short for the publish/subscribe pattern. In the publish/subscribe pattern, units don’t directly call each other. Instead, they publish messages that other units (subscribers) can listen to. Publishers don’t know what (if any) units will subscribe, and subscribers don’t know what (if any) publishers will publish.

#### Isolate logic from I/O
Sometimes you can use monad compositions (like promises) to eliminate dependent logic from your compositions. For example, the following function contains logic that you can’t unit test without mocking all of the async functions:

```js
async function uploadFiles({user, folder, files}) {
  const dbUser = await readUser(user);
  const folderInfo = await getFolderInfo(folder);
  if (await haveWriteAccess({dbUser, folderInfo})) {
    return uploadToFolder({dbUser, folderInfo, files });
  } else {
    throw new Error("No write access to that folder");
  }
}
```

Let’s throw in some helper pseudo-code to make it runnable:

```js
const log = (...args) => console.log(...args);
// Ignore these. In your real code you'd import
// the real things.
const readUser = () => Promise.resolve(true);
const getFolderInfo = () => Promise.resolve(true);
const haveWriteAccess = () => Promise.resolve(true);
const uploadToFolder = () => Promise.resolve('Success!');
// gibberish starting variables
const user = '123';
const folder = '456';
const files = ['a', 'b', 'c'];
async function uploadFiles({user, folder, files}) {
  const dbUser = await readUser({ user });
  const folderInfo = await getFolderInfo({ folder });
  if (await haveWriteAccess({dbUser, folderInfo})) {
    return uploadToFolder({dbUser, folderInfo, files });
  } else {
    throw new Error("No write access to that folder");
  }
}
uploadFiles({user, folder, files})
  .then(log);
```

And now refactor it to use promise composition via asyncPipe():


```js
const asyncPipe = (...fns) => x => (
  fns.reduce(async (y, f) => f(await y), x)
);
const uploadFiles = asyncPipe(
  readUser,
  getFolderInfo,
  haveWriteAccess,
  uploadToFolder
);
uploadFiles({user, folder, files})
  .then(log);
```

The conditional logic is easily removed because promises have conditional branching built-in. The idea is that logic and I/O don’t mix well, so we want to remove the logic from the I/O dependent code.

In order to make this kind of composition work, we need to ensure 2 things:

1. haveWriteAccess() will reject if the user doesn't have write access. That moves the conditional logic into the promise context so we don't have to unit test it or worry about it at all (promises have their own tests baked into the JS engine code).

2. Each of these functions takes and resolves with the same data type.

With those conditions met, it’s trivial to test each of these functions in isolation from each other without mocking the other functions. Since we’ve extracted all of the logic out of the pipeline, there’s nothing meaningful left to unit test in this file. All that’s left to test are the integrations.

# Integration Testing
Integration testing is a software testing technique that focuses on evaluating the interactions between different components or modules of a software system. The purpose of integration testing is to ensure that individual components work together as expected when integrated into a larger system.

In software development, a complex application is often built by combining various smaller modules or components. These components may be developed independently, and integration testing is crucial to identify issues that may arise when they are integrated. The goal is to detect defects in the interfaces and interactions between components, ensuring that the integrated system functions correctly as a whole.

Integration testing can be performed at different levels of granularity, such as:

1. **Module Integration Testing:** Testing interactions between individual modules or units of code.

2. **Subsystem Integration Testing:** Verifying the interactions between groups of related modules that form a subsystem within the larger system.

3. **System Integration Testing:** Testing the entire system to ensure that all components work together as intended.

4. **User Acceptance Testing (UAT):** While not strictly integration testing, UAT can be considered a form of high-level integration testing where the focus is on ensuring that the entire system meets the user's requirements.

There are different approaches to integration testing, including:

- **Top-Down Integration Testing:** Testing starts with the highest-level modules and gradually progresses to lower-level modules.

- **Bottom-Up Integration Testing:** Testing begins with the lower-level modules, and progressively higher-level modules are integrated and tested.

- **Big Bang Integration Testing:** All components are integrated simultaneously, and the entire system is tested as a whole.

- **Incremental Integration Testing:** Components are integrated and tested incrementally, one at a time, until the entire system is integrated and tested.

Integration testing helps ensure that the software functions as intended in real-world scenarios and helps identify and address issues related to data flow, control flow, and interface interactions. It plays a crucial role in the software development life cycle to deliver a reliable and robust product.

# End to End testing
End-to-End (E2E) testing is a software testing methodology that involves testing an entire application from start to finish, simulating real user scenarios. The primary goal of end-to-end testing is to ensure that the integrated components of a software application function as expected and that the entire system behaves correctly in a real-world environment.

Key characteristics of end-to-end testing include:

1. **Real User Scenarios:** E2E testing typically involves simulating real-world user interactions with the application. This includes user inputs, system interactions, and data flow from the beginning to the end of a specific process or workflow.

2. **Integration of Components:** Unlike unit testing or integration testing that focuses on individual modules or components, end-to-end testing verifies the interaction and cooperation of all components and systems within an application.

3. **Full System Testing:** E2E testing covers the entire system or a significant part of it, ensuring that various modules, databases, servers, and external interfaces work seamlessly together.

4. **User Interface Testing:** End-to-end testing often includes testing the user interface to ensure that the application's graphical elements and user interactions meet the design specifications.

5. **Data Flow and Control Flow:** E2E testing evaluates the flow of data and control throughout the application, checking if the information is processed correctly and if the system responds appropriately to user inputs.

6. **Real Environment Simulation:** Test environments for end-to-end testing are set up to closely resemble the production environment, allowing for a more accurate assessment of the application's behavior in real-world conditions.

7. **Automation:** E2E testing can be automated using testing tools and frameworks to execute a series of predefined test cases that simulate end-user interactions. Automated end-to-end tests help ensure repeatability and efficiency in testing large and complex systems.

End-to-end testing is often performed after unit testing and integration testing to provide a comprehensive assessment of the software's functionality and reliability. It helps identify issues related to system integration, data integrity, and overall system performance. The goal is to catch any defects or issues that may arise from the interaction of different components before the software is deployed to production.

---
### Knowledge Check

**Q1.** What is tightly coupled code?

**A1.** "Tightly coupled code" refers to a programming paradigm where components or modules within a software system are highly dependent on each other. In other words, changes to one part of the code are likely to affect other parts, making the system less flexible, harder to maintain, and more prone to errors. This can lead to a lack of modularity, making it difficult to isolate and update individual components without affecting the entire system.

**Q2.** What are the two requirements for a function to be pure?

**A2.** A pure function is a concept in functional programming that describes a function with two main characteristics:

1. **Deterministic:**
   A pure function, given the same set of input parameters, will always produce the same output. There are no hidden or external factors that can affect the result. The function's behavior is entirely determined by its inputs.

2. **No Side Effects:**
   A pure function does not have side effects. Side effects refer to any observable changes made outside the function's scope, such as modifying a global variable, modifying a mutable input parameter, or performing I/O operations like writing to a file or making network requests.

**Q3.** What are side effects and why is it important to identify them when testing a function?

**A3.** An observable side effect is any interaction with the outside world from within a function. That could be anything from changing a variable that exists outside the function, to calling another method from within a function.

Note: If a pure function calls a pure function this isn’t a side effect and the calling function is still pure.

Side effects include, but are not limited to:

+ Making a HTTP request
+ Mutating data
+ Printing to a screen or console
+ DOM Query/Manipulation
+ Math.random()
+ Getting the current time

Side effects themselves are not bad and are often required. Except, for a function to be declared pure it must not contain any. Not all functions need to be, or should be, pure.

Identifying and understanding side effects is crucial during the testing phase for several reasons:

+ Correctness: Side effects can introduce unintended behavior or alter the state of the program in unexpected ways. Identifying and managing side effects is essential to ensure that a function behaves as intended and produces correct results.

+ Predictability: Functions with minimal or well-defined side effects are more predictable and easier to reason about. Predictability is crucial for understanding how a function will behave in different situations and for maintaining code in the long term.

+ Maintainability: Code that relies heavily on side effects can be challenging to maintain. When a function has unexpected side effects, it becomes harder to modify or extend the code without introducing bugs or unintended consequences. Minimizing side effects makes code more modular and maintainable.

+ Testing: Identifying and managing side effects is crucial for effective testing. Functions with minimal side effects are generally easier to test because their behavior is more predictable, and they have a clear input-output relationship. Testing becomes more straightforward when you can isolate the function being tested without worrying about unexpected changes elsewhere in the system.

+ Debugging: When issues arise in a program, understanding the potential side effects of functions can help narrow down the possible causes of problems. This speeds up the debugging process and allows developers to locate and fix issues more efficiently.

+ Concurrency and Parallelism: In multi-threaded or parallel programming environments, side effects can lead to race conditions and other concurrency-related bugs. Identifying and managing side effects is crucial for writing concurrent and parallel code that behaves correctly and efficiently.

**Q4.** What are two solutions to the tightly coupled code problem?

**A4.** 
+ Use pure functions as the atomic unit of composition, as opposed to classes, imperative procedures, or mutating functions.
+ Isolate side-effects from the rest of your program logic. That means don’t mix logic with I/O (including network I/O, rendering UI, logging, etc…).

**Q5.** What is mocking?

**A5.** Mocking is a technique used in software testing to isolate the code being tested by replacing certain components with mock objects. Mock objects simulate the behavior of real objects but allow developers to control their responses and interactions during testing.

**Q6.** When would you use a mock function?

**A6.** Mocking is particularly useful in the following scenarios:

1. **Dependency Isolation:** When a function or module has dependencies on external services, databases, APIs, or other components, mocking allows you to isolate the code under test by replacing these dependencies with mock objects. This ensures that the test focuses solely on the behavior of the code being tested, without being affected by external factors.

2. **Performance Testing:** In some cases, real dependencies may be impractical or too slow for certain types of testing, such as performance testing. Mocking allows you to simulate the behavior of these dependencies in a controlled and efficient manner, enabling you to assess the performance of the code in isolation.

3. **Testing Error Handling:** Mocking can be valuable when testing error-handling code paths. By using mock objects to simulate error conditions or exceptional cases, you can ensure that your code responds appropriately to different error scenarios without having to trigger those errors in the real system.

4. **Unit Testing:** In unit testing, the goal is to isolate and test individual units of code in isolation. Mocking is often employed to replace dependencies and ensure that the unit being tested is decoupled from external systems. This helps in creating focused and predictable tests for smaller units of code.

5. **Third-Party Services:** When working with third-party services, such as payment gateways or external APIs, mocking allows you to create controlled test scenarios without making actual requests to these services. This is beneficial for testing various scenarios, error conditions, or edge cases without affecting the real external service.

6. **Parallel and Concurrent Testing:** In situations where tests run in parallel or concurrently, using real external dependencies can lead to race conditions or contention issues. Mocking enables developers to simulate concurrent interactions and avoid interference between test cases.

7. **Unstable or Unpredictable Environments:** When testing in environments that are unstable or have unpredictable states, relying on real external services may lead to flaky tests. Mocking provides a stable and controlled environment for testing, helping to reduce test flakiness.

However, it's important to note that while mocking is a powerful testing tool, it should be used judiciously. Over-mocking can lead to tests that don't accurately reflect the real-world behavior of the system. Therefore, it's essential to strike a balance and use mocking when necessary to improve test isolation without sacrificing the validity of your tests.

**Q7.** How should you test incoming query messages?

**A7.** Testing incoming query messages typically involves verifying that a system responds appropriately to queries from external sources. These queries could be user input, API requests, database queries, or any form of input that triggers a read operation.

When dealing with incoming queries, which are typically read operations that retrieve data, the primary focus is on verifying the correctness of the result returned by the system in response to the query.

When testing incoming query messages, we should **assert results**, which means verifying that the system produces the correct and expected outcome in response to a read operation. This helps ensure the correctness of the system's behavior and provides confidence that the queries are handled appropriately.

Here's a breakdown of what "asserting results" means in the testing context:

**1. Identifying the Expected Result:**<br>
Before making the query or triggering the operation, you should have a clear understanding of what the expected result should be.
This involves defining the expected outcome based on the specific query and the state of the system.

**2. Executing the Query:**<br>
Trigger the incoming query, either directly in your test code or by calling the relevant function or method that handles the incoming query.

**3. Assertion:**<br>
After the query has been executed, use assertions to compare the actual result with the expected result.
The assertion checks whether the system's response aligns with what you anticipated.

**Assertions Examples:** For a query that retrieves data from a database, you might assert that the returned data matches a predefined set of values or meets certain criteria.
If the query involves calculations, you could assert that the calculated result is within an acceptable range.
Ensure that error conditions are handled correctly, and the system returns the appropriate error message or indication when the query cannot be fulfilled.

**Q8.** Why should you not test implementation?

**A8.** When testing our program we should test the interface and not the implementation. If we test only the interface, it means we can change the implementation without breaking the test.

When you test the interface, you are concerned with how the component behaves based on its inputs and how it produces outputs. The goal is to verify that the external contract or API of the component is upheld, regardless of the internal details. This approach promotes a black-box testing perspective, treating the component as a "black box" where you only observe inputs and outputs.

**Benefits of Testing the Interface:**
   - **Flexibility:** By focusing on the interface, you create tests that are less dependent on the specific implementation details. This allows for more flexibility in changing or refactoring the internal code without impacting the tests.
   - **Abstraction:** Testing the interface encourages abstraction and separation of concerns. It allows you to think about a component's functionality at a higher level, promoting a clearer understanding of its purpose.
   - **Maintenance:** Tests that rely on the interface are generally more robust to changes. As long as the external behavior remains consistent, you can modify or improve the internal code without rewriting the tests.
   - **Reducing Coupling:** Tight coupling between tests and implementation details can lead to brittle tests. If the tests are tightly bound to the internal structure of the code, any modification to the code may require corresponding changes in the tests. Testing the interface helps reduce this coupling, allowing for more maintainable and less fragile test suites.

**Q9.** Should you test private methods?

**A9.** When testing, we should not test private methods. Private methods are implementation details, we should not make assertions about their results and we should not expect to send those results.

**Q10.** Why should you not test outgoing messages with no side effects?

**A10.** When it comes to testing outgoing messages (such as events, notifications, or messages sent to external systems), the focus is often on ensuring that these messages are generated and sent correctly based on the system's behavior.  However, Outgoing messages that don't result in any observable changes or side effects within the system often do not provide meaningful behavior to test. If sending a message has no impact on the system's state or behavior, testing it can be considered redundant.

The principle of testing the interface and not the implementation suggests that tests should focus on the observable behavior of a system rather than its internal details. If sending an outgoing message doesn't affect the external behavior of the system, testing it really is not that valuable.