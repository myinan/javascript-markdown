# Objects and Object Constructors
## Objects as a design pattern
One of the simplest ways you can begin to organize your code is by simply grouping things into objects. Take these examples from a ‘tic tac toe’ game:

```javascript
// example one
const playerOneName = "tim"
const playerTwoName = "jenn"
const playerOneMarker = "X"
const playerTwoMarker = "O"

// example two
const playerOne = {
  name: "tim",
  marker: "X"
}

const playerTwo = {
  name: "jenn",
  marker: "O"
}
```

At first glance, the first doesn’t seem so bad.. and it actually takes fewer lines to write than the example using objects, but the benefits of the second approach are huge! Let me demonstrate:

```js
function printName(player) {
  console.log(player.name)
}
```

This is something that you just could NOT do with the example one setup. Instead, every time you wanted to print a specific player’s name, you would have to remember the correct variable name and then manually console.log it:

```js
console.log(playerOneName)
console.log(playerTwoName)
```

Again, this isn’t that bad… but what if you don’t know which player’s name you want to print?

```js
function gameOver(winningPlayer){
  console.log("Congratulations!")
  console.log(winningPlayer.name + " is the winner!")
}
```

Or, what if we aren’t making a 2 player game, but something more complicated such as an online shopping site with a large inventory? In that case, using objects to keep track of an item’s name, price, description and other things is the only way to go. Unfortunately, in that type of situation, manually typing out the contents of our objects is not feasible either. We need a cleaner way to create our objects, which brings us to…

## Object constructor (Constructor Function)
Constructor functions are functions that are used to construct new objects. The `new` operator is used to create new instances based off a constructor function. We have seen some built-in JavaScript constructors, such as `new Array()` and `new Date()`, but we can also create our own custom templates from which to build new objects.

When you have a specific type of object that you need to duplicate like our player or inventory items, a better way to create them is using an object constructor, which is a function that looks like this:

```js
function Player(name, marker) {
  this.name = name
  this.marker = marker
}
```

and which you use by calling the function with the keyword `new`.

```js
const player = new Player('steve', 'X')
console.log(player.name) // 'steve'
```

Just like with objects created using the Object Literal method, you can add functions to the object:

```js
function Player(name, marker) {
  this.name = name
  this.marker = marker
  this.sayName = function() {
    console.log(name)
  }
}

const player1 = new Player('steve', 'X')
const player2 = new Player('john', 'O')
player1.sayName() // logs 'steve'
player2.sayName() // logs 'john'
```

**Note:** A constructor function is just a regular function. It becomes a constructor when it is called on by an instance with the `new` keyword. In JavaScript, we capitalize the first letter of a constructor function by convention.

## The `prototype` object
### Concept of Prototypes in JavaScript:

#### 1. **Prototype Basics:**

   - **Every Object Has a Prototype:**
     In JavaScript, every object has a prototype. This prototype is an object itself, and it serves as a template or model from which the object inherits properties and methods.

   - **Prototype Chain:**
     Prototypes form a chain where an object's prototype may itself have a prototype, and this chain continues until it reaches `Object.prototype`, which is at the end of the chain.

```js
/* Creating Objects and Accessing their Prototypes */

// Object constructor function
function Player(name, marker) {
  this.name = name;
  this.marker = marker;
}

// Adding a function to the prototype
Player.prototype.sayHello = function () {
  console.log(`Hello, I'm ${this.name}!`);
};

// Creating player objects
const player1 = new Player('Alice', 'X');
const player2 = new Player('Bob', 'O');

// Accessing and using the prototype function
player1.sayHello(); // Output: "Hello, I'm Alice!"
player2.sayHello(); // Output: "Hello, I'm Bob!"

// Checking the prototype of objects
console.log(Object.getPrototypeOf(player1) === Player.prototype); // true
console.log(Object.getPrototypeOf(player2) === Player.prototype); // true
```

#### 2. **Inheritance and Access:**

   - **Inheritance Mechanism:**
     When an object is created, it links to its prototype, and it can access properties and methods defined on that prototype as if they were its own.

   - **Prototype Lookup:**
     If a property or method is not directly found on an object, JavaScript searches through the prototype chain to find it. If it's not found anywhere in the chain, `undefined` is returned.

#### 3. **Practical Usage and Implications:**

   - **Memory Efficiency:**
     By defining common properties and methods on a prototype, JavaScript conserves memory. Objects don't need to duplicate these shared properties, as they're accessed via the prototype chain.

   - **Flexible and Dynamic:**
     Prototypes allow dynamic modification of objects' behaviors. Altering the prototype affects all objects linked to it.

### Exploring Prototypal Inheritance:

#### 1. **Creating and Accessing Prototypes:**

   - **Defining Prototypes:**
     Properties and methods can be defined on a prototype object. For instance, defining a method on `Player.prototype` will be accessible to all instances of `Player`.

   - **Accessing Prototypes:**
     The `Object.getPrototypeOf()` method allows access to an object's prototype. This method returns the prototype object linked to a particular object.

#### 2. **Prototype Chain and Object Relationship:**

   - **Chain of Inheritance:**
     Objects can inherit from a prototype, and that prototype may, in turn, inherit from another, forming a chain. This continues until it reaches `Object.prototype`.

   - **Understanding Object Hierarchy:**
     The relationship between objects and their prototypes forms a hierarchy, allowing shared methods and properties across different object types.

     **Note:** <br>Every prototype object inherits from Object.prototype by default.<br>An object’s Object.getPrototypeOf() value can only be one unique prototype object.

#### 3. **Working with Prototypes:**

   - **Setting Up Inheritance:**
     `Object.setPrototypeOf()` is used to define the prototype an object should inherit from. This setup is recommended to occur before object creation to avoid performance issues.

```js
/* Prototypal Inheritance */

// Creating a Parent object
function Person(name) {
  this.name = name;
}

Person.prototype.sayName = function () {
  console.log(`My name is ${this.name}.`);
};

// Creating a Child object that inherits from the Parent
function Player(name, marker) {
  this.name = name;
  this.marker = marker;
}

// Setting up inheritance using Object.setPrototypeOf()
Object.setPrototypeOf(Player.prototype, Person.prototype);

// Creating Player objects
const player1 = new Player('Emily', 'X');
const player2 = new Player('David', 'O');

// Accessing inherited functions
player1.sayName(); // Output: "My name is Emily."
player2.sayName(); // Output: "My name is David."

```

   - **Avoiding Direct Assignments:**
     Directly assigning one prototype to another (`Player.prototype = Person.prototype`) may cause issues as changes to one will reflect on the other. `Object.setPrototypeOf()` ensures independent prototypes.

#### 4. **Prototypal Inheritance in Real-World Scenarios:**

   - **Customizing Inheritance:**
     Developers can create custom inheritance structures by linking prototypes, enabling objects to inherit desired properties and behaviors.

   - **Maintaining Efficiency and Performance:**
     Careful setup and understanding of prototypes are crucial to maintain efficient code, preventing performance problems due to improper manipulation of prototypes after object creation.

### Significance of Prototypes:

- **Facilitating Code Reusability:**
  Prototypes aid in code organization by enabling objects to share and inherit properties and methods, promoting code reusability and maintenance.

- **Dynamic Nature of JavaScript:**
  The dynamic nature of prototypes allows for flexible adjustments to an object's behavior and structure.

Understanding JavaScript prototypes forms the cornerstone of effective object-oriented programming in JavaScript, allowing developers to create organized, memory-efficient, and flexible code structures through inheritance and property sharing.

**NOTE: The for..in loop iterates over both object's own and its inherited properties. All other key/value-getting methods only operate on the object itself.**

## The `this` keyword
### [**A comprehensive explanation of the `this` keyword by Dmitri Pavlutin**](https://dmitripavlutin.com/gentle-explanation-of-this-in-javascript/)

From a background like Java, PHP or other standard language, `this` is the instance of the current object in the class method. `this` cannot be used outside the method and such a simple approach does not create confusion.

In JavaScript the situation is different: `this` is the context of a function invocation (a.k.a. execution). The language has 4 function invocation types:

```
function invocation: alert('Hello World!')
method invocation: console.log('Hello World!')
constructor invocation: new RegExp('\\d')
indirect invocation: alert.call(undefined, 'Hello World!')
```

Each invocation type defines the context in its way, so `this` behaves differently than the developer expects.

Moreover strict mode also affects the execution context.

**The key to understanding this keyword is having a clear view of function invocation and how it impacts the context.**

Before starting, let's familiarize with a couple of terms:

+ Invocation of a function is executing the code that makes the body of a function, or simply calling the function. For example parseInt function invocation is parseInt('15').
+ Context of an invocation is the value of `this` within function body.
+ Scope of a function is the set of variables and functions accessible within a function body.

### Function invocation
Function invocation is performed when an expression that evaluates to a function object is followed by an open parenthesis (, a comma separated list of arguments expressions and a close parenthesis ). For example parseInt('18').

_`this` is the **global object** in a function invocation._

The global object is determined by the execution environment. In a browser, the global object is `window` object.

In a function invocation, the execution context is the global object.

```js
function sum(a, b) {
  console.log(this === window); // => true
  this.myNumber = 20; // add 'myNumber' property to global object
  return a + b;
}
// sum() is invoked as a function
// this in sum() is a global object (window)
sum(15, 16);     // => 31
window.myNumber; // => 20
```

At the time sum(15, 16) is called, JavaScript automatically sets `this` as the global object (window in a browser).

`this` in a function invocation, strict mode: `this` is `undefined` in a function invocation in strict mode.

A common trap with the function invocation is thinking that `this` is the same in an inner function as in the outer function.

The context of the inner function (except arrow function) depends only on its own invocation type, but not on the outer function's context.

To make `this` have a desired value, modify the inner function's context with indirect invocation (using .call() or .apply() ) or create a bound function (using .bind() ).

```js
const numbers = {
  numberA: 5,
  numberB: 10,

  sum: function() {
    console.log(this === numbers); // => true

    function calculate() {
      // this is window or undefined in strict mode
      console.log(this === numbers); // => false
      return this.numberA + this.numberB;
    }

    return calculate();
  }
};

numbers.sum(); // => NaN or throws TypeError in strict mode
```

numbers.sum() is a method invocation on an object thus `this` equals `numbers`. calculate() function is defined inside sum(), so you might expect to have `this` as numbers object when invoking calculate() too.

calculate() is a function invocation (but not method invocation), thus here `this` is the global object window or undefined in strict mode. Even if the outer function numbers.sum() has the context as numbers object, it doesn't have influence here.

To solve the problem, calculate() function must execute with the same context as the numbers.sum() method, to access this.numberA and this.numberB properties.

One solution is to change manually the context of calculate() to the desired one by calling calculate.call(this) (an indirect invocation of a function).

```js
const numbers = {
  numberA: 5,
  numberB: 10,
  sum: function() {
    console.log(this === numbers); // => true

    function calculate() {
      console.log(this === numbers); // => true
      return this.numberA + this.numberB;
    }

    // use .call() method to modify the context
    return calculate.call(this);
  }
};
numbers.sum(); // => 15
```

calculate.call(this) executes calculate() function as usual, but additionally modifies the context to a value specified as the first parameter.

Now this.numberA + this.numberB is same as numbers.numberA + numbers.numberB. The function returns the expected result 5 + 10 = 15.

Another solution, slightly better, is to use an arrow function:

```js
const numbers = {
  numberA: 5,
  numberB: 10,
  sum: function() {
    console.log(this === numbers); // => true

    const calculate = () => {
      console.log(this === numbers); // => true
      return this.numberA + this.numberB;
    }

    return calculate();
  }
};

numbers.sum(); // => 15
```

The arrow function resolves `this` lexically, or, in other words, uses `this` value of numbers.sum() method.

### Method invocation
A `method` is a function stored in a property of an object.

```js
const myObject = {
  // helloMethod is a method
  helloMethod: function() {
    return 'Hello World!';
  }
};
const message = myObject.helloMethod();
```

`helloMethod` is a method of `myObject`. Use a property accessor `myObject.helloMethod` to access the method.

Method invocation is performed when an expression in a form of property accessor that evaluates to a function object is followed by an open parenthesis (, a comma separated list of arguments expressions and a close parenthesis ).

Recalling the previous example, myObject.helloMethod() is a method invocation of helloMethod on the object myObject.

More examples of method calls are: [1, 2].join(',') or /\s/.test('beautiful world').

Understanding the difference between function invocation and method invocation is important!

The method invocation requires a property accessor form to call the function (obj.myFunc() or obj\['myFunc'\]()), while function invocation does not (myFunc()).

`this` in a method invocation: `this` is the **object that owns the method** in a method invocation.

```js
const calc = {
  num: 0,
  increment() {
    console.log(this === calc); // => true
    this.num += 1;
    return this.num;
  }
};

// method invocation. this is calc
calc.increment(); // => 1
calc.increment(); // => 2
```

Calling calc.increment() makes the context of increment function to be calc object. So using this.num to increment the num property works well.

**Important:** A JavaScript object inherits a method from its prototype. When the inherited method is invoked on the object, the context of the invocation is still the object itself:

```js
const myDog = Object.create({
  sayName() {
    console.log(this === myDog); // => true
    return this.name;
  }
});

myDog.name = 'Milo';
// method invocation. this is myDog
myDog.sayName(); // => 'Milo'
```

Object.create() creates a new object myDog and sets its prototype from the first argument. myDog object inherits sayName method.

When myDog.sayName() is executed, myDog is the context of invocation.

**IMPORTANT:** A method can be extracted from an object into a separated variable const alone = myObj.myMethod. When the method is called alone `alone()`, detached from the original object, you might think that `this` is the object `myObj` on which the method was defined.

But, if the method is called without an object, then a function invocation happens, where `this` is the global object window or undefined in strict mode.

A bound function `const alone = myObj.myMethod.bind(myObj)` (using .bind() ) fixes the context by binding `this` of the object that owns the method.

The following example defines Pet constructor and makes an instance of it: myCat. Then setTimeout() after 1 second logs myCat object information:

```js
function Pet(type, legs) {
  this.type = type;
  this.legs = legs;

  this.logInfo = function() {
    console.log(this === myCat); // => false
    console.log(`The ${this.type} has ${this.legs} legs`);
  }
}

const myCat = new Pet('Cat', 4);
// logs "The undefined has undefined legs"
// or throws a TypeError in strict mode
setTimeout(myCat.logInfo, 1000);
```

You might think that setTimeout(myCat.logInfo, 1000) will call the myCat.logInfo(), which should log the information about myCat object.

Unfortunately, **the method gets separated from its object when passed as an argument**: setTimeout(myCat.logInfo).

A function bounds with an object using `.bind()` method. If the separated method is bound with `myCat` object, the context problem is solved:

```js
function Pet(type, legs) {
  this.type = type;
  this.legs = legs;

  this.logInfo = function() {
    console.log(this === myCat); // => true
    console.log(`The ${this.type} has ${this.legs} legs`);
  };
}

const myCat = new Pet('Cat', 4);

// Create a bound function
const boundLogInfo = myCat.logInfo.bind(myCat);
// logs "The Cat has 4 legs"
setTimeout(boundLogInfo, 1000);
```

myCat.logInfo.bind(myCat) returns a new function that executes exactly like logInfo, but has `this` as myCat, even in a function invocation.

An alternative solution is to define logInfo() method as an arrow function, which binds `this` lexically:

```js
function Pet(type, legs) {
  this.type = type;
  this.legs = legs;

  this.logInfo = () => {
    console.log(this === myCat); // => true
    console.log(`The ${this.type} has ${this.legs} legs`);
  };
}

const myCat = new Pet('Cat', 4);
// logs "The Cat has 4 legs"
setTimeout(myCat.logInfo, 1000);
```

### Constructor invocation
**Constructor invocation** is performed when `new` keyword is followed by an expression that evaluates to a function object, an open parenthesis (, a comma separated list of arguments expressions and a close parenthesis ).

Examples of construction invocation: new Pet('cat', 4), new RegExp('\\\d').

This example declares a function `Country`, then invokes it as a constructor:

```js
function Country(name, traveled) {
  this.name = name ? name : 'United Kingdom';
  this.traveled = Boolean(traveled); // transform to a boolean
}

Country.prototype.travel = function() {
  this.traveled = true;
};

// Constructor invocation
const france = new Country('France', false);
// Constructor invocation
const unitedKingdom = new Country;

france.travel(); // Travel to France
```

`new Country('France', false)` is a constructor invocation of the `Country` function. This call creates a new object, which name property is 'France'.

If the constructor is called without arguments, then the parenthesis pair can be omitted: `new Country`.

Starting ECMAScript 2015, JavaScript allows to define constructors using `class` syntax:

```js
class City {
  constructor(name, traveled) {
    this.name = name;
    this.traveled = false;
  }

  travel() {
    this.traveled = true;
  }
}

// Constructor invocation
const paris = new City('Paris', false);
paris.travel();
```

`new City('Paris', false)` is a constructor invocation. The object's initialization is handled by a special method in the class: `constructor`, which has `this` as the newly created object.

this in a constructor invocation: `this` is the **newly created object** in a constructor invocation.

The context of a constructor invocation is the newly created object. The constructor initializes the object with data that comes from constructor arguments, sets up initial values for properties, attaches event handlers, etc.

```js
function Foo () {
  // this is fooInstance
  this.property = 'Default Value';
}

// Constructor invocation
const fooInstance = new Foo();
fooInstance.property; // => 'Default Value'
```

new Foo() is making a constructor call where the context is fooInstance. Inside Foo the object is initialized: this.property is assigned with a default value.

**IMPORTANT:** Constructors, generally, omit the logic to initialize the object when `new` keyword is missing.

```js
function Vehicle(type, wheelsCount) {
  this.type = type;
  this.wheelsCount = wheelsCount;
  return this;
}

// Function invocation
const car = Vehicle('Car', 4);
car.type; // => 'Car'
car.wheelsCount // => 4
car === window // => true
```

Vehicle is a function that sets type and wheelsCount properties on the context object. When executing Vehicle('Car', 4) an object car is returned, which has the correct properties: car.type is 'Car' and car.wheelsCount is 4.

You might think it works well for creating and initializing new objects.

However, `this` is `window` object in a function invocation, thus Vehicle('Car', 4) sets properties on the window object. This is a mistake. A new object is not created.

**Make sure to use the `new` operator in cases when a constructor call is expected.**

```js
function Vehicle(type, wheelsCount) {
  if (!(this instanceof Vehicle)) {
    throw Error('Error: Incorrect invocation');
  }

  this.type = type;
  this.wheelsCount = wheelsCount;
  return this;
}

// Constructor invocation
const car = new Vehicle('Car', 4);
car.type               // => 'Car'
car.wheelsCount        // => 4
car instanceof Vehicle // => true

// Function invocation. Throws an error.
const brokenCar = Vehicle('Broken Car', 3);
```

new Vehicle('Car', 4) works well: a new object is created and initialized because new keyword is present in the constructor invocation.

### Indirect invocation
**Indirect** invocation is performed when a function is called using `myFunc.call()` or `myFunc.apply()` methods.

Functions in JavaScript are first-class objects, which means that a function is an object. The type of function object is `Function`.

.call() and .apply() methods of the function object are used to invoke the function with a configurable context.

`myFunction.call(thisArg, arg1, arg2, ...)` accepts the first argument `thisArg` as the `context of the invocation` and a list of arguments arg1, args2, ... that are passed as arguments to the called function.

`myFunction.apply(thisArg, [arg1, arg2, ...])` accepts the first argument `thisArg` as the `context of the invocation` and an array of arguments [arg1, args, ...] that are passed as arguments to the called function.

The following example demonstrates the indirect invocation:

```js
function sum(number1, number2) {
  return number1 + number2;
}

sum.call(undefined, 10, 2);    // => 12
sum.apply(undefined, [10, 2]); // => 12
```

sum.call() and sum.apply() both invoke the function with 10 and 2 arguments.

`this` in an indirect invocation: `this` is the **first argument** of `.call()` or `.apply()` in an indirect invocation.

`this` in indirect invocation is the value passed as first argument to .call() or .apply().

The following example shows the indirect invocation context:

```js
const rabbit = { name: 'White Rabbit' };

function concatName(string) {
  console.log(this === rabbit); // => true
  return string + this.name;
}

// Indirect invocations
concatName.call(rabbit, 'Hello ');  // => 'Hello White Rabbit'
concatName.apply(rabbit, ['Bye ']); // => 'Bye White Rabbit'
```

The indirect invocation is useful when a function should be executed with a specific context. For example, to solve the context problems with function invocation, where this is always window or undefined in strict mode. It can be used to simulate a method call on an object (see the previous code sample).

Another practical example is creating hierarchies of classes in ES5 to call the parent constructor:

```js
function Runner(name) {
  console.log(this instanceof Rabbit); // => true
  this.name = name;
}

function Rabbit(name, countLegs) {
  console.log(this instanceof Rabbit); // => true
  // Indirect invocation. Call parent constructor.
  Runner.call(this, name);
  this.countLegs = countLegs;
}

const myRabbit = new Rabbit('White Rabbit', 4);
myRabbit; // { name: 'White Rabbit', countLegs: 4 }
```

`Runner.call(this, name)` inside `Rabbit` makes an indirect call of the parent function to initialize the object.

### Bound function
A bound function is a function whose context and/or arguments are bound to specific values. You create a bound function using `.bind()` method. The original and bound functions share the same code and scope, but different contexts and arguments on execution.

myFunc.bind(thisArg, arg1, arg2, ...) accepts the first argument thisArg as the context and an optional list of arguments arg1, arg2, ... to bound to. .bind() returns a new function which context is bound to thisArg and arguments to arg1, arg2, ....

The following code creates a bound function and later invokes it:

```js
function multiply(number) {
  'use strict';
  return this * number;
}

// create a bound function with context
const double = multiply.bind(2);
// invoke the bound function
double(3); // => 6
double(10); // => 20
```

multiply.bind(2) returns a new function object `double`, which is bound with number 2. multiply and double have the same code and scope.

Contrary to .apply() and .call() methods, which invoke the function right away, the .bind() method only returns a new function supposed to be invoked later with a pre-defined `this` value.

`this` inside a bound function: `this` is the **first argument** of `myFunc.bind(thisArg)` when invoking a bound function.

The role of .bind() is to create a new function, which invocation will have the context as the first argument passed to .bind(). It is a powerful technique that allows creating functions with a predefined `this` value.

```js
const numbers = {
  array: [3, 5, 10],

  getNumbers() {
    return this.array;
  }
};

// Create a bound function
const boundGetNumbers = numbers.getNumbers.bind(numbers);
boundGetNumbers(); // => [3, 5, 10]

// Extract method from object
const simpleGetNumbers = numbers.getNumbers;
simpleGetNumbers(); // => undefined or throws an error in strict mode
```

numbers.getNumbers.bind(numbers) returns a function boundGetNumbers which context is bound to numbers. Then boundGetNumbers() is invoked with `this` as `numbers` and returns the correct array object.

The function numbers.getNumbers is extracted into a variable simpleGetNumbers without binding. On later function invocation simpleGetNumbers() has this as window or undefined in strict mode, but not numbers object. In this case simpleGetNumbers() will not return correctly the array.

**IMPORTANT:** .bind() makes a permanent context link and will always keep it. A bound function cannot change its linked context when using .call() or .apply() with a different context or even a rebound doesn't have any effect (Tight context binding).

The following example creates a bound function, then tries to change its already pre-defined context:

```js
function getThis() {
  'use strict';
  return this;
}

const one = getThis.bind(1);

one();         // => 1

one.call(2);   // => 1
one.apply(2);  // => 1
one.bind(2)(); // => 1
```

### Arrow function
Arrow function is designed to declare the function in a shorter form and **lexically** bind the context.

It can be used the following way:

```js
const hello = (name) => {
  return 'Hello ' + name;
};

hello('World'); // => 'Hello World'
// Keep only even numbers
[1, 2, 5, 6].filter(item => item % 2 === 0); // => [2, 6]
```

`this` in arrow function: `this` is the **enclosing context** where the arrow function is defined.

The arrow function doesn't create its own execution context but takes `this` from the outer function where it is defined. In other words, the arrow function resolves `this` lexically.

```js
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  log() {
    console.log(this === myPoint); // => true
    setTimeout(() => {
      console.log(this === myPoint);      // => true
      console.log(this.x + ':' + this.y); // => '95:165'
    }, 1000);
  }
}
const myPoint = new Point(95, 165);
myPoint.log();
```

setTimeout() calls the arrow function with the same context (myPoint object) as the log() method. As seen, the arrow function "inherits" the context from the function where it is defined.

An arrow function is bound with the lexical `this` once and forever. `this` cannot be modified even when using the context modification methods.

#### Pitfall: defining method with an arrow function:
This example defines a method format() on a class Period using an arrow function:

```js
function Period (hours, minutes) { 
  this.hours = hours;
  this.minutes = minutes;
}

Period.prototype.format = () => {
  console.log(this === window); // => true
  return this.hours + ' hours and ' + this.minutes + ' minutes';
};

const walkPeriod = new Period(2, 30);
walkPeriod.format(); // => 'undefined hours and undefined minutes'
```

Since `format` is an arrow function and is defined in the global context (topmost scope), it has `this` as `window` object.

Even if format is executed as a method on an object walkPeriod.format(), window is kept as the context of invocation. It happens because the arrow function has a static context that doesn't change on different invocation types.

The function expression solves the problem because regular function expressions does change their context depending on invocation:

```js
function Period (hours, minutes) {
  this.hours = hours;
  this.minutes = minutes;
}

Period.prototype.format = function() {
  console.log(this === walkPeriod); // => true
  return this.hours + ' hours and ' + this.minutes + ' minutes';
};

const walkPeriod = new Period(2, 30);
walkPeriod.format(); // => '2 hours and 30 minutes'
```

walkPeriod.format() is a method invocation on an object with the context walkPeriod object. this.hours evaluates to 2 and this.minutes to 30, so the method returns the correct result: '2 hours and 30 minutes'.

---
### Knowledge Check

**Q1.** Write an object constructor and instantiate the object.

**A1.** 
```js
function Country(name, visited) {
  this.name = name;
  this.visited = Boolean(visited);
}

const germany = new Country("Germany", false);
// germany.name = "Germany";
// germany.visited = false;
```

**Q2.** Describe what a prototype is and how it can be used.

**A2.** In JavaScript, every object has a prototype. This prototype is an object itself, and it serves as a template or model from which the object inherits properties and methods.<br> Prototypes form a chain where an object's prototype may itself have a prototype, and this chain continues until it reaches Object.prototype, which is at the end of the chain.<br> When an object is created, it links to its prototype, and it can access properties and methods defined on that prototype as if they were its own.<br> If a property or method is not directly found on an object, JavaScript searches through the prototype chain to find it. If it's not found anywhere in the chain, undefined is returned.<br> By defining common properties and methods on a prototype, JavaScript conserves memory. Objects don't need to duplicate these shared properties, as they're accessed via the prototype chain.<br> Prototypes allow dynamic modification of objects' behaviors. Altering the prototype affects all objects linked to it.

Also, any regular JavaScript object can be used as a prototype. We can create an object and then create another object that inherits properties and methods from the first one.

**Q3.** Explain prototypal inheritance.

**A3.** Properties and methods can be defined on a prototype object. For instance, defining a method on Player.prototype will be accessible to all instances of Player. Objects can inherit from a prototype, and that prototype may, in turn, inherit from another, forming a chain. This continues until it reaches Object.prototype. The relationship between objects and their prototypes forms a hierarchy, allowing shared methods and properties across different object types.

Every prototype object inherits from Object.prototype by default.
An object’s Object.getPrototypeOf() value can only be one unique prototype object.

**Q4.** Understand the basic do’s and don’t’s of prototypal inheritance.

**A4.** Using Object.getPrototypeOf() to access an object’s prototype is recommended. The same thing can also be done using the .`__proto__` property of the object. However, this is a non-standard way of doing so, and deprecated. Hence, it is not recommended to access an object’s prototype by using the `__proto__` property. 

Object.setPrototypeOf() is used to define the prototype an object should inherit from. This setup is recommended to occur before object creation to avoid performance issues. (As a better alternative, use Object.create() instead of Object.setPrototypeof() to avoid the said performance issues.)

Directly assigning one prototype to another (Player.prototype = Person.prototype) may cause issues as changes to one will reflect on the other. Object.setPrototypeOf() ensures independent prototypes.

**Q5.** Explain what Object.create does.

**A5.** The Object.create() static method creates a new object, using an existing object as the prototype of the newly created object.

```js
const person = {
  isHuman: false,
  printIntroduction: function () {
    console.log(`My name is ${this.name}. Am I human? ${this.isHuman}`);
  },
};

const me = Object.create(person);

me.name = 'Matthew'; // "name" is a property set on "me", but not on "person"
me.isHuman = true; // Inherited properties can be overwritten

me.printIntroduction();
// Expected output: "My name is Matthew. Am I human? true"
```

**Q6.** How does `this` behave in different situations?

**A6.** `this` behaves differently depending on the invocation type of a function. There a 4 different types of function invocation in javascript:

```
function invocation: alert('Hello World!')
method invocation: console.log('Hello World!')
constructor invocation: new RegExp('\\d')
indirect invocation: alert.call(undefined, 'Hello World!')
```

+ function invocation: `this` is the global object in a function invocation.<br> The global object is determined by the execution environment. In a browser, the global object is window object.
+ method invocation: `this` is the object that owns the method in a method invocation.

```js
const calc = {
  num: 0,
  increment() {
    console.log(this === calc); // => true
    this.num += 1;
    return this.num;
  }
};

// method invocation. this is calc
calc.increment(); // => 1
calc.increment(); // => 2
```

A JavaScript object inherits a method from its prototype. When the inherited method is invoked on the object, the context of the invocation is still the object itself.

+ constructor invocation: `this` is the newly created object in a constructor invocation.

```js
function Foo () {
  // this is fooInstance
  this.property = 'Default Value';
}

// Constructor invocation
const fooInstance = new Foo();
fooInstance.property; // => 'Default Value'
```

IMPORTANT: Constructors, generally, omit the logic to initialize the object when new keyword is missing. Make sure to use the new operator in cases when a constructor call is expected.

+ indirect invocation: Indirect invocation is performed when a function is called using myFunc.call() or myFunc.apply() methods. `this` is the first argument of .call() or .apply() in an indirect invocation. `this` in indirect invocation is the value passed as first argument to .call() or .apply().

+ `this` inside a bound function: `this` is the first argument of myFunc.bind(thisArg) when invoking a bound function.

+ `this` in arrow function: `this` is the enclosing context where the arrow function is defined. The arrow function doesn't create its own execution context but takes this from the outer function where it is defined. In other words, the arrow function resolves `this` lexically.

```js
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  log() {
    console.log(this === myPoint); // => true
    setTimeout(() => {
      console.log(this === myPoint);      // => true
      console.log(this.x + ':' + this.y); // => '95:165'
    }, 1000);
  }
}
const myPoint = new Point(95, 165);
myPoint.log();
```

setTimeout() calls the arrow function with the same context (myPoint object) as the log() method. As seen, the arrow function "inherits" the context from the function where it is defined.











