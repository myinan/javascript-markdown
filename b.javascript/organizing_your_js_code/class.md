# `class` in Javascript
JavaScript does not have classes in the same sense as other Object Oriented languages like Java or Ruby. However, the `class` syntax was introduced with ECMAScript 2015 (ES6) to provide a more convenient and familiar syntax for creating constructor functions and defining object prototypes. The class syntax is essentially a more concise way to work with prototypes and constructor functions.

There is a bit of controversy about using the `class` syntax, however. Opponents argue that class is basically just *syntactic sugar* over the existing prototype-based constructors and that it’s dangerous and/or misleading to obscure what’s really going on with these objects. Despite the controversy, classes are beginning to crop up in real code bases that you are almost certainly going to encounter such as frameworks like React (especially if you end up working with class-based React code).

Since we’ve already gone fairly in-depth with Constructors, you don’t have too much left to learn here beyond the new syntax. If you choose to use classes in your code (that’s fine!) you can use them much the same way as object constructors.

# Accessor properties (property `getter` and `setter`)
There are two kinds of object properties.

The first kind is **data properties**. We already know how to work with them. All properties that we’ve been using until now were data properties. Data properties directly store a value and have attributes associated with them, such as writable, enumerable, and configurable.

The second type of property is something new. It’s an **accessor property**. Accessor properties are a newer and more advanced concept in JavaScript. Unlike data properties, accessor properties don't directly hold a value. Instead, they define functions (getters and setters) to retrieve or modify a value. Accessor properties are defined using the `get` and `set` keywords. The get function is called when the property is read, and the set function is called when the property is assigned a new value. From the external code perspective, when you access or modify the property, it appears like a regular property, even though behind the scenes, functions are executed. This allows for more control and customization when getting and setting values.

In JavaScript, accessor properties are a type of object property that allows you to define **custom behavior** for getting and setting the value of a property. Unlike data properties, which directly store a value, accessor properties define functions to be called when the property is **read (get)** or **written (set)**. These functions are known as getter and setter functions.

Accessor properties are defined using the `get` and `set` keywords within an object literal or added to an existing object using the `Object.defineProperty()` method.

Here's an example to illustrate accessor properties:

```javascript
let person = {
  _name: 'John', // Conventionally, a leading underscore is used to indicate a private variable
  get name() {
    console.log('Getting name');
    return this._name;
  },
  set name(newName) {
    console.log('Setting name to ' + newName);
    this._name = newName;
  }
};

console.log(person.name); // Outputs: Getting name, John
person.name = 'Jane';     // Outputs: Setting name to Jane
console.log(person.name); // Outputs: Getting name, Jane
```

In this example, the `person` object has an accessor property named `name`. The `get` function is called when attempting to access the `name` property, and the `set` function is called when attempting to modify the `name` property. The use of getter and setter functions allows you to perform custom actions or validations when reading or updating the property.

Accessor properties are particularly useful when you want to control access to an object's properties, enforce validation rules, or perform additional logic when a property is accessed or modified.

### Advantages of accessor properties
1. **Syntax and Readability:**
   - Using `get` and `set` directly in the property definition makes the code cleaner and more readable. It explicitly conveys the intention that you are defining a property with special behavior.
   - It provides a clear separation between getting and setting behavior, enhancing code organization.

   Example with `get` and `set`:
   ```javascript
   let obj = {
     _value: 0,
     get value() {
       console.log("Getting the value");
       return this._value;
     },
     set value(newValue) {
       console.log("Setting the value");
       this._value = newValue;
     }
   };
   ```

   Equivalent example using traditional methods:
   ```javascript
   let obj = {
     _value: 0,
     value: function() {
       console.log("Getting or setting the value");
       return this._value;
     },
     setValue: function(newValue) {
       console.log("Setting the value");
       this._value = newValue;
     }
   };
   ```

2. **Property Access:**
   - When using `get` and `set`, you access the property as if it were a regular data property, making the syntax more intuitive and similar to working with regular properties.

   Example with `get` and `set`:
   ```javascript
   obj.value = 10; // Calls the setter
   console.log(obj.value); // Calls the getter
   ```

   Equivalent example using traditional methods:
   ```javascript
   obj.setValue(10); // Using a setter method
   console.log(obj.value()); // Using a getter method
   ```

3. **Execute Custom Logic:**
   - The `get` and `set` functions associated with accessor properties enable you to execute custom logic when a property is accessed or modified.
   - This customization can include validation, logging, side-effect operations, or any other behavior you want to associate with getting or setting a value.

    Here's a simple example to illustrate the idea:

    ```javascript
    let person = {
    _age: 0,
    get age() {
        console.log("Getting age");
        return this._age;
    },
    set age(newAge) {
        if (newAge >= 0 && newAge <= 120) {
        console.log("Setting age");
        this._age = newAge;
        } else {
        console.log("Invalid age value");
        }
    }
    };

    person.age = 25; // Calls the setter and sets the age to 25
    console.log(person.age); // Calls the getter and logs "Getting age", then returns the current age
    person.age = 150; // Calls the setter, but logs "Invalid age value" and doesn't update the age
    ```

    In this example, the `get` and `set` functions associated with the `age` property allow you to customize the behavior of getting and setting the person's age, including validation to ensure that the age remains within a reasonable range.

### Property Descriptors
In JavaScript, property descriptors are used to define and control the behavior of object properties. A property descriptor is an object that describes the attributes of a property, such as whether the property is writable, enumerable, and configurable. Property descriptors are commonly used with the `Object.defineProperty()` method, which allows you to add a new property to an object or modify an existing one.

A property descriptor can have the following attributes:

1. **value**: The value of the property.
2. **writable**: A boolean indicating whether the property's value can be changed.
3. **enumerable**: A boolean indicating whether the property can be enumerated (listed) when iterating over the object's properties.
4. **configurable**: A boolean indicating whether the property can be deleted or its attributes can be modified.
5. **get**: A function that serves as a getter for the property.
6. **set**: A function that serves as a setter for the property.

Here's an example of using `Object.defineProperty()` with property descriptors:

```javascript
const obj = {};

Object.defineProperty(obj, 'example', {
  value: 42,
  writable: false,
  enumerable: true,
  configurable: true
});

console.log(obj.example); // 42

// Attempting to change the value of 'example' will result in an error because it's not writable.
// obj.example = 100; // This would throw an error in strict mode.

// Enumerating over the object will include 'example' since it's enumerable.
for (let prop in obj) {
  console.log(prop); // 'example'
}

// Deleting the 'example' property is allowed because it's configurable.
delete obj.example;
console.log(obj.example); // undefined
```

In this example, the `example` property is created with a property descriptor that makes it read-only (`writable: false`), enumerable, and configurable. Property descriptors provide fine-grained control over how properties behave in JavaScript objects.

**The descriptor for a data property includes `value`, `writable`, `enumerable`, and `configurable`; while the descriptor for an accessor property includes `get`, `set`, `enumerable`, and `configurable`.**

### Descriptor of an accessor property
Descriptors for accessor properties are different from those for data properties.

For accessor properties, there is no `value` or `writable`, but instead there are `get` and `set` functions.

That is, an accessor descriptor may have:

- `get` – a function without arguments, that works when a property is read,
- `set` – a function with one argument, that is called when the property is set,
- `enumerable` – same as for data properties,
- `configurable` – same as for data properties.

For instance, to create an accessor `fullName` with `Object.defineProperty()`, we can pass a descriptor with get and set:

```js
let user = {
  name: "John",
  surname: "Smith"
};

Object.defineProperty(user, 'fullName', {
  get() {
    return `${this.name} ${this.surname}`;
  },

  set(value) {
    [this.name, this.surname] = value.split(" ");
  }
});

alert(user.fullName); // John Smith

for(let key in user) alert(key); // name, surname
```

Please note that a property can be either an accessor (has `get/set` methods) or a data property (has a `value`), not both.

If we try to supply both `get` and `value` in the same descriptor, there will be an error:

```js
// Error: Invalid property descriptor.
Object.defineProperty({}, 'prop', {
  get() {
    return 1
  },

  value: 2
});
```

## `class`
Classes are a template for creating objects. They encapsulate data with code to work on that data. Classes in JS are built on prototypes but also have some syntax and semantics that are unique to classes.

The basic syntax is:

```js
class MyClass {
  // class methods
  constructor() { ... }
  method1() { ... }
  method2() { ... }
  method3() { ... }
  ...
}
```

Then use `new MyClass()` to create a new object with all the listed methods.<br>
The `constructor()` method is called automatically by `new`, so we can initialize the object there.

**Important:** A common pitfall for novice developers is to put a comma between class methods, which would result in a syntax error. The notation here is not to be confused with object literals. Within the class, no commas are required between methods.

### How does `class` work?

```js
class User {
  constructor(name) { this.name = name; }
  sayHi() { alert(this.name); }
}

// proof: User is a function
alert(typeof User); // function
```

What `class User {...}` construct really does is:

1. Creates a function named `User`, that becomes the result of the class declaration. The function code is taken from the `constructor` method (assumed empty if we don’t write such method).
2. Stores class methods, such as `sayHi`, in `User.prototype`.

After `new User()` call, object is created; then when we call its method, it’s taken from the prototype.

Here’s the code to introspect:

```js
class User {
  constructor(name) { this.name = name; }
  sayHi() { alert(this.name); }
}

// User is a function
alert(typeof User); // function

// ...or, more precisely, the constructor method
alert(User === User.prototype.constructor); // true

// The methods are in User.prototype, e.g:
alert(User.prototype.sayHi); // the code of the sayHi method

// there are exactly two methods in the prototype
alert(Object.getOwnPropertyNames(User.prototype)); // constructor, sayHi
```

### Not just a syntactic sugar?
Sometimes people say that `class` is a “syntactic sugar” (syntax that is designed to make things easier to read, but doesn’t introduce anything new), because we could actually declare the same thing without using the class keyword at all:

```js
// rewriting class User in pure functions

// 1. Create constructor function
function User(name) {
  this.name = name;
}
// a function prototype has "constructor" property by default,
// so we don't need to create it

// 2. Add the method to prototype
User.prototype.sayHi = function() {
  alert(this.name);
};

// Usage:
let user = new User("John");
user.sayHi();
```

The result of this definition is about the same. So, there are indeed reasons why `class` can be considered a syntactic sugar to define a constructor together with its prototype methods.

Still, there are important differences.

1. First, a function created by class is labelled by a special internal property `[[IsClassConstructor]]: true`. So it’s not entirely the same as creating it manually.

2. Class methods are non-enumerable. A class definition sets `enumerable flag` to `false` for all methods in the `prototype`.<br>
That’s good, because if we `for..in` over an object, we usually don’t want its class methods.

3. Classes always `use strict`. All code inside the class construct is automatically in strict mode.

Besides, class syntax brings many other features that we’ll explore later.

### Class expressions
Similar to function expressions, we can also create class expressions. Class expressions can be named or unnamed.

```js
let User = class {
  sayHi() {
    alert("Hello");
  }
};
```

Similar to Named Function Expressions, class expressions may have a name. If a class expression has a name, it’s visible inside the class only:

```js
// "Named Class Expression"
// (no such term in the spec, but that's similar to Named Function Expression)
let User = class MyClass {
  sayHi() {
    alert(MyClass); // MyClass name is visible only inside the class
  }
};

new User().sayHi(); // works, shows MyClass definition

alert(MyClass); // error, MyClass name isn't visible outside of the class
```

### Classes may include `getters/setters`
Just like literal objects, classes may include getters/setters.

```js
class User {

  constructor(name) {
    // invokes the setter
    this.name = name;
  }

  get name() {
    return this._name;
  }

  set name(value) {
    if (value.length < 4) {
      alert("Name is too short.");
      return;
    }
    this._name = value;
  }

}

let user = new User("John");
alert(user.name); // John

user = new User(""); // Name is too short.
```

Technically, such class declaration works by creating getters and setters in `User.prototype`.

Though we can still achieve the same functionality using constructor functions and prototypes;

```js
// Using Constructor Function:

function MyClass() {
  // Private variable
  let _myProperty = 0;

  // Getter
  Object.defineProperty(this, 'myProperty', {
    get: function() {
      console.log('Getter called');
      return _myProperty;
    }
  });

  // Setter
  Object.defineProperty(this, 'myProperty', {
    set: function(value) {
      console.log('Setter called');
      if (value >= 0) {
        _myProperty = value;
      } else {
        console.log('Value must be non-negative');
      }
    }
  });
}

// Usage
const instance = new MyClass();

console.log(instance.myProperty); // Getter called, 0

instance.myProperty = 42; // Setter called
console.log(instance.myProperty); // Getter called, 42

instance.myProperty = -1; // Setter called, Value must be non-negative
console.log(instance.myProperty); // Getter called, 42 (unchanged)
```

```js
// Using Prototypal Inheritance:

function MyClass() {
  // Private variable
  this._myProperty = 0;
}

// Getter
Object.defineProperty(MyClass.prototype, 'myProperty', {
  get: function() {
    console.log('Getter called');
    return this._myProperty;
  }
});

// Setter
Object.defineProperty(MyClass.prototype, 'myProperty', {
  set: function(value) {
    console.log('Setter called');
    if (value >= 0) {
      this._myProperty = value;
    } else {
      console.log('Value must be non-negative');
    }
  }
});

// Usage
const instance = new MyClass();

console.log(instance.myProperty); // Getter called, 0

instance.myProperty = 42; // Setter called
console.log(instance.myProperty); // Getter called, 42

instance.myProperty = -1; // Setter called, Value must be non-negative
console.log(instance.myProperty); // Getter called, 42 (unchanged)
```

Clearly `class` syntax provide a more convenient syntax for defining getters and setters.

### class syntax and computed names [...]
In JavaScript, "computed names" typically refer to the ability to dynamically compute property names for object literals and classes. This feature was introduced in ECMAScript 2015 (ES6) and allows us to use expressions inside square brackets to compute the name of an object property.

Here's an example:

```javascript
let propertyName = 'dynamicProperty';

// Using computed names in object literals
let myObject = {
  [propertyName]: 'Hello, World!',
  // other properties...
};

console.log(myObject.dynamicProperty); // Output: Hello, World!
```

In the example above, the `propertyName` variable is used to dynamically compute the name of the property in the `myObject` object. This is particularly useful when we need to create objects with dynamic property names.

The same concept can be applied to class methods:

```javascript
class MyClass {
  // Using computed names for methods
  [propertyName]() {
    return 'Hello, World!';
  }
}

const myInstance = new MyClass();
console.log(myInstance.dynamicProperty()); // Output: Hello, World!
```

In this case, the method name is dynamically computed using the `propertyName` variable.

Computed names provide flexibility when creating objects and classes, allowing us to use dynamic values to define property names.

On the other hand, while constructor functions themselves don't directly support computed names for properties, we can achieve a similar effect by using the `Object.defineProperty` method within the constructor to dynamically set property names.

```js
function MyConstructor() {
  let propertyName = 'dynamicProperty';

  // Using Object.defineProperty to create a property with a computed name
  Object.defineProperty(this, propertyName, {
    value: 'Hello, World!',
    enumerable: true,
    writable: true,
    configurable: true,
  });

  // Other constructor logic...
}

// Instantiate an object using the constructor
const myInstance = new MyConstructor();

console.log(myInstance.dynamicProperty); // Output: Hello, World!
```

In this example, the `Object.defineProperty` method is used within the constructor function `MyConstructor` to dynamically create a property with the name specified by the `propertyName` variable. The `value` property of `Object.defineProperty` is set to `'Hello, World!'`.

It is clear that this approach involves a bit more manual work compared to the more concise syntax available with class declarations.

---
## A deeper dive into `class`

 class syntax was introduced with ECMAScript 2015 (ES6) to provide a more convenient and familiar syntax for creating constructor functions and defining object prototypes. The class syntax is essentially a more concise way to work with prototypes and constructor functions. Classes in JS are built on prototypes but also have some syntax and semantics that are unique to classes.

```js
class MyClass {
  // Constructor
  constructor() {
    // Constructor body
  }
  // Instance field
  myField = "foo";
  // Instance method
  myMethod() {
    // myMethod body
  }
  // Static field
  static myStaticField = "bar";
  // Static method
  static myStaticMethod() {
    // myStaticMethod body
  }
  // Static block
  static {
    // Static initialization code
  }
  // Fields, methods, static fields, and static methods all have
  // "private" forms
  #myPrivateField = "bar";
}
```

After a class has been declared, you can create instances of it using the `new` operator.

```js
const myInstance = new MyClass();
console.log(myInstance.myField); // 'foo'
myInstance.myMethod();
```

Typical function constructors can both be constructed with new and called without new. However, attempting to "call" a class without new will result in an error.

```js
const myInstance = MyClass(); // TypeError: Class constructor MyClass cannot be invoked without 'new'
```

Unlike function declarations, class declarations are not hoisted (or, in some interpretations, hoisted but with the temporal dead zone restriction), which means you cannot use a class before it is declared.

```js
new MyClass(); // ReferenceError: Cannot access 'MyClass' before initialization

class MyClass {}
```

This behavior is similar to variables declared with let and const.

Similar to functions, class declarations also have their expression counterparts.

```js
const MyClass = class {
  // Class body...
};
```

Class expressions can have names as well. The expression's name is only visible to the class's body.

```js
const MyClass = class MyClassLongerName {
  // Class body. Here MyClass and MyClassLongerName point to the same class.
};
new MyClassLongerName(); // ReferenceError: MyClassLongerName is not defined
```

In classes, the instance creation is done by the `constructor()` method. Each time you call `new`, a different instance is created.

Within a class constructor, the value of `this` points to the newly created instance.

The `this` value will be automatically returned as the result of `new`. You are advised to not return any value from the constructor — because if you return a non-primitive value, it will become the value of the `new` expression, and the value of `this` is dropped.

```js
class MyClass {
  constructor() {
    this.myField = "foo";
    return {};
  }
}

console.log(new MyClass().myField); // undefined
```

### `class` fields
Class fields allow developers to define instance variables directly within the class body, making it more convenient and concise compared to the traditional way of defining instance variables in the constructor. Class fields are declared using the `static` keyword for static fields and without the static keyword for instance fields. Both static and instance fields can be either private fields or public fields.

`class` fields are set on individual objects, not on `prototype`.

```js
class MyClass {
  // Public instance field
  publicInstanceField = 10;

  // Private instance field (using '#' syntax)
  #privateInstanceField = 20;

  // Public static field
  static publicStaticField = 30;

  // Private static field (using '#' syntax)
  static #privateStaticField = 40;

  // Constructor
  constructor() {
    // Accessing private instance field within the class is allowed
    console.log(`Private instance field: ${this.#privateInstanceField}`);
  }

  // Methods can also use private fields
  getPrivateInstanceField() {
    return this.#privateInstanceField;
  }

  // Public method accessing private static field
  static getPrivateStaticField() {
    return this.#privateStaticField; // Error: private field '#privateStaticField' must be declared in an enclosing class
  }
}

// Creating an instance of the class
const myInstance = new MyClass();

// Accessing public and private instance fields
console.log(`Public instance field: ${myInstance.publicInstanceField}`);
console.log(`Private instance field: ${myInstance.getPrivateInstanceField()}`);

// Accessing public and private static fields
console.log(`Public static field: ${MyClass.publicStaticField}`);
console.log(`Private static field: ${MyClass.getPrivateStaticField()}`);
```

A private field is an identifier prefixed with `#` (the hash symbol). The hash is an integral part of the field's name, which means a private field can never have name clash with a public field. In order to refer to a private field anywhere in the class, we must declare it in the class body.

Accessing private fields outside the class is an early syntax error. The language can guard against this because `#privateField` is a special syntax, so it can do some static analysis and find all usage of private fields before even evaluating the code.

**Note:** Code run in the Chrome console can access private properties outside the class. This is a DevTools-only relaxation of the JavaScript syntax restriction.

Private fields in JavaScript are hard private: if the class does not implement methods that expose these private fields, there's absolutely no mechanism to retrieve them from outside the class. This means you are safe to do any refactors to your class's private fields, as long as the behavior of exposed methods stay the same.

A class method can read the private fields of other instances, as long as they belong to the same class.

```js
class Color {
  #values;
  constructor(r, g, b) {
    this.#values = [r, g, b];
  }
  redDifference(anotherColor) {
    // #values doesn't necessarily need to be accessed from this:
    // you can access private fields of other instances belonging
    // to the same class.
    return this.#values[0] - anotherColor.#values[0];
  }
}

const red = new Color(255, 0, 0);
const crimson = new Color(220, 20, 60);
red.redDifference(crimson); // 35
```

However, if `anotherColor` is not a `Color` instance, `#values` won't exist. (Even if another class has an identically named `#values` private field, it's not referring to the same thing and cannot be accessed here.) Accessing a nonexistent private property throws an error instead of returning undefined like normal properties do. If you don't know if a private field exists on an object and you wish to access it without using `try/catch` to handle the error, you can use the `in` operator.

```js
class Color {
  #values;
  constructor(r, g, b) {
    this.#values = [r, g, b];
  }
  redDifference(anotherColor) {
    if (!(#values in anotherColor)) {
      throw new TypeError("Color instance expected");
    }
    return this.#values[0] - anotherColor.#values[0];
  }
}
```

There are some limitations in using private properties: the same name can't be declared twice in a single class, and they can't be deleted. Both lead to early syntax errors.

```js
class BadIdeas {
  #firstName;
  #firstName; // syntax error occurs here
  #lastName;
  constructor() {
    delete this.#lastName; // also a syntax error
  }
}
```

Methods, getters, and setters can be private as well. They're useful when you have something complex that the class needs to do internally but no other part of the code should be allowed to call.

Private fields also have their public counterparts:

```js
class MyClass {
  luckyNumber = Math.random();
}
console.log(new MyClass().luckyNumber); // 0.5
console.log(new MyClass().luckyNumber); // 0.3
```

Public fields are almost equivalent to assigning a property to `this`. For example, the above example can also be converted to:

```js
class MyClass {
  constructor() {
    this.luckyNumber = Math.random();
  }
}
```

#### Making bound methods with class fields
As we already know, the `this` value in a function change depending on the context of the call.<br>
So if an object method is passed around and called in another context, `this` won’t be a reference to its object any more.

For instance, the following code will show undefined:

```js
class Button {
  constructor(value) {
    this.value = value;
  }

  click() {
    alert(this.value);
  }
}

let button = new Button("hello");

setTimeout(button.click, 1000); // undefined
```


The reason the `this` value changes in the context of setTimeout(button.click, 1000) is related to how the `this` keyword works in JavaScript.

When we pass `button.click` as the first argument to setTimeout, we are passing the method reference without the context of the object (`button`). In JavaScript, when a method is referenced without the object context, the `this` value becomes undefined (or it refers to the global object in non-strict mode).

Class fields provide quite elegant syntax to solve this problem:

```js
class Button {
  constructor(value) {
    this.value = value;
  }
  click = () => {
    alert(this.value);
  }
}

let button = new Button("hello");

setTimeout(button.click, 1000); // hello
```

Arrow functions don't have their own `this` context. Instead, they inherit the `this` value from the enclosing scope. So, if an arrow function is passed as an argument to another function, it retains the `this` value of the surrounding scope.

The class field `click = () => {...}` is created on a per-object basis, there’s a separate function for each `Button` object, with `this` inside it referencing that object. We can pass `button.click` around anywhere, and the value of `this` will always be correct.

### Static properties
In JavaScript, static properties are properties that are associated with a class itself rather than with instances of the class. Unlike instance properties, which are specific to individual objects created from a class, static properties are shared among all instances of a class and can be accessed directly on the class itself.

Here's an example to illustrate static properties in JavaScript:

```javascript
class MyClass {
  // Instance property
  constructor(name) {
    this.name = name;
  }

  // Static property
  static staticProperty = "I am a static property";

  // Instance method
  display() {
    console.log(`Instance property: ${this.name}`);
  }

  // Static method
  static staticMethod() {
    console.log("This is a static method");
  }
}

// Creating instances of the class
const obj1 = new MyClass("Object 1");
const obj2 = new MyClass("Object 2");

// Accessing instance property and calling instance method
obj1.display(); // Output: Instance property: Object 1

// Accessing static property and calling static method
console.log(MyClass.staticProperty); // Output: I am a static property
MyClass.staticMethod(); // Output: This is a static method
```

In this example, `staticProperty` is a static property of the `MyClass` class, while `name` is an instance property specific to each object created from the class. Similarly, `staticMethod` is a static method, which can be called directly on the class, while `display` is an instance method that operates on individual instances of the class.

Static properties `(static fields, methods, getter/setters)` are often used for values or functionality that are associated with the class as a whole, rather than with instances of the class.

There is a restriction on private static fields: only the class which defines the private static field can access the field. This can lead to unexpected behavior when using `this`. In the following example, `this` refers to the `Subclass` class (not the ClassWithPrivateStaticField class) when we try to call `Subclass.publicStaticMethod()`, and so causes a `TypeError`.

```js
class ClassWithPrivateStaticField {
  static #privateStaticField = 42;

  static publicStaticMethod() {
    return this.#privateStaticField;
  }
}

class Subclass extends ClassWithPrivateStaticField {}

Subclass.publicStaticMethod(); // TypeError: Cannot read private member #privateStaticField from an object whose class did not declare it
```

The same restriction previously mentioned for private static fields holds for private static methods as well, and similarly can lead to unexpected behavior when using `this`.

#### Calling static members from another static method
In order to call a static method or property within another static method of the same class, you can use the `this` keyword.

```js
class StaticMethodCall {
  static staticProperty = "static property";
  static staticMethod() {
    return `Static method and ${this.staticProperty} has been called`;
  }
  static anotherStaticMethod() {
    return `${this.staticMethod()} from another static method`;
  }
}
StaticMethodCall.staticMethod();
// 'Static method and static property has been called'

StaticMethodCall.anotherStaticMethod();
// 'Static method and static property has been called from another static method'
```

There is also a special construct called a **`static initialization block`**, which is a block of code that runs when the class is first loaded.

#### Static initialization blocks
Static initialization blocks are declared within a class. It contains statements to be evaluated during class initialization. This permits more flexible initialization logic than `static` properties, such as using `try...catch` or setting multiple fields from a single value. Initialization is performed in the context of the current class declaration, with access to private state, which allows the class to share information of its private properties with other classes or functions declared in the same scope.

```js
class ClassWithStaticInitializationBlock {
  static staticProperty1 = 'Property 1';
  static staticProperty2;
  static {
    this.staticProperty2 = 'Property 2';
  }
}

console.log(ClassWithStaticInitializationBlock.staticProperty1);
// Expected output: "Property 1"
console.log(ClassWithStaticInitializationBlock.staticProperty2);
// Expected output: "Property 2"

```


```js
class MyClass {
  static {
    MyClass.myStaticProperty = "foo";
  }
}

console.log(MyClass.myStaticProperty); // 'foo'
```

Static initialization blocks are almost equivalent to immediately executing some code after a class has been declared. The only difference is that they have access to static private properties.

Without static initialization blocks, complex static initialization might be achieved by calling a static method after the class declaration:

```js
class MyClass {
  static init() {
    // Access to private static fields is allowed here
  }
}

MyClass.init();
```

However, this approach exposes an implementation detail (the init() method) to the user of the class. On the other hand, any initialization logic declared outside the class does not have access to private static fields. Static initialization blocks allow arbitrary initialization logic to be declared within the class and executed during class evaluation.

The scope of the static block is nested within the lexical scope of the class body, and can access private properties declared within the class without causing a syntax error.

### Simulating private constructors
Many other languages include the capability to mark a constructor as private, which prevents the class from being instantiated outside of the class itself — you can only use static factory methods that create instances, or not be able to create instances at all. JavaScript does not have a native way to do this, but it can be accomplished by using a private static flag.

```js
class PrivateConstructor {
  static #isInternalConstructing = false;

  constructor() {
    if (!PrivateConstructor.#isInternalConstructing) {
      throw new TypeError("PrivateConstructor is not constructable");
    }
    PrivateConstructor.#isInternalConstructing = false;
    // More initialization logic
  }

  static create() {
    PrivateConstructor.#isInternalConstructing = true;
    const instance = new PrivateConstructor();
    return instance;
  }
}

new PrivateConstructor(); // TypeError: PrivateConstructor is not constructable
PrivateConstructor.create(); // PrivateConstructor {}
```

### `extends` and inheritance
In JavaScript, the `extends` keyword is used to create a subclass (derived class) that inherits from another class (base class). This mechanism is part of the object-oriented programming (OOP) features introduced in ECMAScript 6 (ES6) and is often referred to as "class inheritance."

Here's a breakdown of how `extends` works in JavaScript classes:

1. **Defining a Base Class (Superclass):**
   You start by defining a base class using the `class` keyword. This class serves as the template for other classes that will inherit from it.

    ```javascript
    class Animal {
      constructor(name) {
        this.name = name;
      }

      makeSound() {
        console.log("Some generic sound");
      }
    }
    ```

2. **Creating a Subclass (Derived Class) with `extends`:**
   You can create a subclass that inherits from the base class using the `extends` keyword. The subclass can have its own methods and properties, and it inherits the methods and properties from the base class.

    ```javascript
    class Dog extends Animal {
      constructor(name, breed) {
        // Call the constructor of the base class using super()
        super(name);
        this.breed = breed;
      }

      // You can override methods from the base class
      makeSound() {
        console.log("Bark! Bark!");
      }

      // You can also add new methods specific to the subclass
      fetch() {
        console.log(`${this.name} is fetching the ball.`);
      }
    }
    ```

3. **`super` Keyword:**
   In the constructor of the subclass, you use the `super()` keyword to call the constructor of the base class. This is necessary to initialize the properties inherited from the base class.

    ```javascript
    class Dog extends Animal {
      constructor(name, breed) {
        // Call the constructor of the base class using super()
        // It is a language requirement to call `super()` before accessing `this`. The `super()` call calls the parent class's constructor to initialize `this`.
        super(name);
        this.breed = breed;
      }
    }
    ```

4. **Overriding Methods:**
   Subclasses can override methods from the base class by redefining them. In the example above, the `makeSound` method is overridden in the `Dog` subclass.

5. **Adding New Methods and Properties:**
   Subclasses can also have their own methods and properties in addition to those inherited from the base class.

    ```javascript
    class Dog extends Animal {
      // ... (constructor and other methods)

      // You can also add new methods specific to the subclass
      fetch() {
        console.log(`${this.name} is fetching the ball.`);
      }
    }
    ```

Here's an example of how you might use these classes:

```javascript
// Create an instance of the base class
const genericAnimal = new Animal("Generic Animal");
genericAnimal.makeSound();  // Outputs: Some generic sound

// Create an instance of the subclass
const myDog = new Dog("Buddy", "Golden Retriever");
myDog.makeSound();  // Outputs: Bark! Bark!
myDog.fetch();      // Outputs: Buddy is fetching the ball.
```

In this example, `Dog` is a subclass that extends the `Animal` base class, demonstrating the use of the `extends` keyword in JavaScript class inheritance.

The derived class has access to all public properties of the parent class.

Within derived classes, you can access the parent class's methods by using `super`. This allows you to build enhancement methods and avoid code duplication.

When you use `extends`, the static methods inherit from each other as well, so you can also override or enhance them.

```js
class ColorWithAlpha extends Color {
  // ...
  static isValid(r, g, b, a) {
    // Call the parent class's isValid() and build on the return value
    return super.isValid(r, g, b) && a >= 0 && a <= 1;
  }
}

console.log(ColorWithAlpha.isValid(255, 0, 0, -1)); // false
```

Derived classes don't have access to the parent class's private fields — this is another key aspect to JavaScript private fields being "hard private". Private fields are scoped to the class body itself and do not grant access to any outside code.

A class can only extend from one class. However, due to the dynamic nature of JavaScript, it's still possible to achieve the effect of multiple inheritance through `class composition` and `mixins`.

Instances of derived classes are also instances of the base class.

```js
const color = new ColorWithAlpha(255, 0, 0, 0.5);
console.log(color instanceof Color); // true
console.log(color instanceof ColorWithAlpha); // true
```

The `extends` keyword not only establishes a prototype link between the child and parent classes but also sets up the prototype chain for instances created from those classes. `extends` sets the prototype for both `ChildClass` and `ChildClass.prototype`. 

```js
class ParentClass {}
class ChildClass extends ParentClass {}

// Allows inheritance of static properties
Object.getPrototypeOf(ChildClass) === ParentClass;
// Allows inheritance of instance properties
Object.getPrototypeOf(ChildClass.prototype) === ParentClass.prototype;
```

Any constructor that can be called with `new` and has the `prototype` property can be the candidate for the parent class. The two conditions must both hold — for example, bound functions and Proxy can be constructed, but they don't have a prototype property, so they cannot be subclassed.

The right-hand side of `extends` does not have to be an identifier. You can use any expression that evaluates to a constructor. This is often useful to create `mixins`. The `this` value in the `extends` expression is the `this` surrounding the class definition, and referring to the class's name is a `ReferenceError` because the class is not initialized yet.

```js
class SomeClass extends class {
  constructor() {
    console.log("Base class");
  }
} {
  constructor() {
    super();
    console.log("Derived class");
  }
}

new SomeClass();
// Base class
// Derived class
```

### Subclassing built-ins
**Warning:** The standard committee now holds the position that the built-in subclassing mechanism in previous spec versions is over-engineered and causes non-negligible performance and security impacts. New built-in methods consider less about subclasses, and engine implementers are investigating whether to remove certain subclassing mechanisms. Consider using `composition` instead of `inheritance` when enhancing built-ins.

#### Challenges when extending/subclassing built-in classes to create custom classes with additional or modified functionality:

1. **Static Factory Method on a Subclass:**
   - *Expectation:* When you use a static factory method (like `Promise.resolve()` or `Array.from()`) on a subclass, the result should be an instance of that subclass.
   - *Issue:* There's a challenge when the static method tries to create an instance using `this`. For example, if you do `[p1, p2, p3].map(Promise.resolve)`, it might throw an error because `this` inside `Promise.resolve` is undefined.
   - *Solution:* This problem can be fixed by making sure the static method checks if `this` is a constructor. If it's not, then fall back to the base class.

   ```javascript
   class CustomPromise extends Promise {
     // Static factory method
     static customResolve() {
       if (typeof this !== 'function') {
         // If not a constructor, fall back to the base class
         return Promise.resolve.apply(Promise, arguments);
       }
       // Create an instance of the subclass
       return new this(resolve => resolve(...arguments));
     }
   }

   const customInstance = [1, 2, 3].map(CustomPromise.customResolve);
   ```

2. **Instance Method Returning a New Instance on a Subclass:**
   - *Expectation:* When you call an instance method that returns a new instance (like `Promise.prototype.then()` or `Array.prototype.map()`) on a subclass, the result should be an instance of that subclass.
   - *Issue:* The instance method needs to read `this.constructor` to get the constructor function. However, using `new this.constructor()` might break existing code.
   - *Solution:* Instead of directly using `this.constructor`, many methods use the constructor's `@@species` property, which returns the constructor itself by default. This helps avoid potential issues with legacy code.

   ```javascript
   class CustomArray extends Array {
     // Instance method returning a new instance
     customMap(callback) {
       // Using @@species to create a new instance
       return new this.constructor[Symbol.species](...this.map(callback));
     }
   }

   const customArray = new CustomArray(1, 2, 3);
   const mappedArray = customArray.customMap(x => x * 2);
   ```

3. **Delegating to Primitive Methods:**
   - *Expectation:* Instance methods should delegate to a minimal set of primitive methods where possible, affecting the behavior of related methods.
   - *Issue:* This can lead to visible invocations of custom code, making optimizations harder to implement.
   - *Example:* If you override the `then()` method in a subclass of `Promise`, it automatically changes the behavior of `catch()`.

   ```javascript
   class CustomPromise extends Promise {
     // Overriding then() to change catch() behavior
     then(onFulfilled, onRejected) {
       // Custom logic here
       console.log("Custom logic in then()");
       return super.then(onFulfilled, onRejected);
     }
   }

   const customInstance = new CustomPromise(resolve => resolve('success'));
   customInstance.then(result => console.log(result)).catch(error => console.error(error));
   ```

These problems are not unique to built-in classes. For your own classes, you will likely have to make the same decisions. However, for built-in classes, optimizability and security are a much bigger concern. New built-in methods always construct the base class and call as few custom methods as possible. If you want to subclass built-ins while achieving the above expectations, you need to override all methods that have the default behavior baked into them. Any addition of new methods on the base class may also break the semantics of your subclass because they are inherited by default. Therefore, a better way to extend built-ins is to use `composition`.

### Extending `null`
`extends null` was designed to allow easy creation of objects that do not inherit from `Object.prototype`. However, due to unsettled decisions about whether `super()` should be called within the constructor, it's not possible to construct such a class in practice using any constructor implementation that doesn't return an object. The TC39 committee is working on re-enabling this feature.

```js
new (class extends null {})();
// TypeError: Super constructor null of anonymous class is not a constructor

new (class extends null {
  constructor() {}
})();
// ReferenceError: Must call super constructor in derived class before accessing 'this' or returning from derived constructor

new (class extends null {
  constructor() {
    super();
  }
})();
// TypeError: Super constructor null of anonymous class is not a constructor
```

Instead, you need to explicitly return an instance from the constructor.

```js
class NullClass extends null {
  constructor() {
    // Using new.target allows derived classes to
    // have the correct prototype chain
    return Object.create(new.target.prototype);
  }
}

const proto = Object.getPrototypeOf;
console.log(proto(proto(new NullClass()))); // null
```

### Extending plain objects
Classes cannot extend regular (non-constructible) objects. If you want to inherit from a regular object by making all properties of this object available on inherited instances, you can instead use Object.setPrototypeOf():

```js
const Animal = {
  speak() {
    console.log(`${this.name} makes a noise.`);
  },
};

class Dog {
  constructor(name) {
    this.name = name;
  }
}

Object.setPrototypeOf(Dog.prototype, Animal);

const d = new Dog("Mitzie");
d.speak(); // Mitzie makes a noise.
```

### `Symbol.species`
In JavaScript, when you perform operations like `map`, `filter`, or other array methods on an array, the result is an array of the same type as the original array( by default, array methods return a new array with the same constructor (class) as the original array). However, when you extend the `Array` class to create a custom array class (for example, `MyArray`), there's a potential issue: the methods return instances of the custom class (`MyArray`) instead of the parent class (`Array`).

To address this, we can use the `Symbol.species` symbol. The `Symbol.species` symbol is a well-known symbol in JavaScript that can be used to customize the constructor that is used to create new instances when a method creates a new array. By default, the `Symbol.species` property is set to the current constructor, but we can override it to return a different constructor.

```js
class MyArray extends Array {
  // Overwrite species to the parent Array constructor
  static get [Symbol.species]() {
    return Array;
  }
}
```

Here, the `MyArray` class overrides the `Symbol.species` property to return `Array`. This means that when array methods like `map` are called on an instance of `MyArray`, the result will be an instance of `Array` rather than `MyArray`.

```js
const a = new MyArray(1, 2, 3);
const mapped = a.map((x) => x * x);

console.log(mapped instanceof MyArray); // false
console.log(mapped instanceof Array);   // true
```

As a result, `mapped instanceof MyArray` evaluates to `false` because the `map` method has used the overridden `Symbol.species` property to construct a new array, and `mapped instanceof Array` evaluates to `true` because the result is an instance of the parent `Array` class. This ensures consistency with the behavior of built-in array methods.

The specific example provided, where MyArray extends Array and then uses MyArray to create instances of the Array class, may seem a bit counterintuitive and unnecessary. The example is intended to illustrate the concept of the Symbol.species pattern and how it can be used to control the behavior of certain array methods.

As an another example, let's consider an another scenario where we have a custom array class called `FilterArray` that extends the built-in `Array` class. This custom array class overrides the `filter` method to filter out certain elements based on a specific criterion. However, we want to ensure that the result of the `filter` operation returns an instance of the parent `Array` class, not the `FilterArray` class.

```javascript
class FilterArray extends Array {
  constructor(...args) {
    super(...args);
  }

  // Override filter method to filter out elements based on a criterion
  filter(callback) {
    const filteredArray = super.filter(callback);
    // Additional custom logic, if needed
    return filteredArray;
  }

  // Override Symbol.species to return the parent Array constructor
  static get [Symbol.species]() {
    return Array;
  }
}

const filterArray = new FilterArray(1, 2, 3, 4, 5);

// Use the overridden filter method
const filteredResult = filterArray.filter(x => x % 2 === 0);

console.log(filteredResult instanceof FilterArray); // false
console.log(filteredResult instanceof Array);       // true
```

In this example:

- `FilterArray` extends `Array` to inherit all the standard array functionality.
- The `filter` method is overridden to provide custom filtering logic.
- The `Symbol.species` pattern is used to ensure that the result of the `filter` operation returns an instance of the parent `Array` class.

By using `Symbol.species`, when we call `filter` on an instance of `FilterArray`, the result is an instance of the parent `Array` class. This is particularly useful when we want to maintain consistency with other code that expects standard array behavior and ensures that the result is not an instance of the custom `FilterArray` class.

### `mix-ins`
Abstract subclasses or `mix-ins` are templates for classes. A class can only have a single superclass, so multiple inheritance from tooling classes, for example, is not possible. The functionality must be provided by the superclass.

A function with a superclass as input and a subclass extending that superclass as output can be used to implement mix-ins:

```js
const calculatorMixin = (Base) =>
  class extends Base {
    calc() {}
  };

const randomizerMixin = (Base) =>
  class extends Base {
    randomize() {}
  };
```

A class that uses these mix-ins can then be written like this:

```js
class Foo {}
class Bar extends calculatorMixin(randomizerMixin(Foo)) {}
```

### `Composition` / Avoiding inheritance
`Inheritance` is a very strong coupling relationship in object-oriented programming. It means all behaviors(properties and methods) of the base class are inherited by the subclass by default, which may not always be what you want.

`Composition` on the other hand, refers to a design pattern where a class is created by combining multiple smaller classes or objects to form a new class. Instead of using inheritance, where a class inherits properties and methods from a single parent class, composition allows you to build a class by assembling various components.

In JavaScript, classes are created using the `class` keyword, and composition can be achieved by creating **instances** of other classes within a class constructor or methods. This promotes code reusability and flexibility, as you can mix and match different components to create new classes without relying on a strict hierarchy.

Here's a simple example to illustrate composition in JavaScript:

```javascript
// Component A
class Engine {
  start() {
    console.log('Engine started');
  }
}

// Component B
class Wheels {
  roll() {
    console.log('Wheels rolling');
  }
}

// Class using composition
class Car {
  constructor() {
    this.engine = new Engine();
    this.wheels = new Wheels();
  }

  drive() {
    this.engine.start();
    this.wheels.roll();
    console.log('Car is moving');
  }
}

// Creating an instance of the composed class
const myCar = new Car();
myCar.drive();
```

In this example, the `Car` class is composed of an `Engine` and `Wheels`. Instead of inheriting from these components, the `Car` class creates instances of them within its constructor. This approach allows for a more modular and flexible code structure.

In general, unless there's a very good reason to use inheritance, it's better to use composition instead. **Composition means that a class has a reference to an object of another class, and only uses that object as an implementation detail.**

Composition is often favored over inheritance in modern JavaScript development because it reduces tight coupling, makes the code more maintainable, and avoids some of the pitfalls associated with the classical inheritance model.

Here is an another example to composition:

```js
class ReadOnlyMap {
  #data;
  constructor(values) {
    this.#data = new Map(values);
  }
  get(key) {
    return this.#data.get(key);
  }
  has(key) {
    return this.#data.has(key);
  }
  get size() {
    return this.#data.size;
  }
  *keys() {
    yield* this.#data.keys();
  }
  *values() {
    yield* this.#data.values();
  }
  *entries() {
    yield* this.#data.entries();
  }
  *[Symbol.iterator]() {
    yield* this.#data[Symbol.iterator]();
  }
}
```

In this case, the ReadOnlyMap class is not a subclass of Map, but it still implements most of the same methods. This means more code duplication, but it also means that the ReadOnlyMap class is not strongly coupled to the Map class, and does not easily break if the Map class is changed.

---
### Knowledge Check

**Q1.** Describe the pros and cons of using classes in JavaScript.

**A1.** 
### Pros:

1. **Encapsulation:**
   - *Pro:* Classes allow you to encapsulate data and behavior within a single unit. This helps in organizing code and makes it more modular and maintainable.

2. **Inheritance:**
   - *Pro:* Classes support inheritance, enabling the creation of a hierarchy of objects. This can lead to code reusability and a more natural representation of relationships between objects.

3. **Readability:**
   - *Pro:* Classes make the code more readable and understandable. They provide a clear structure and syntax for defining object blueprints.

4. **Constructor Functions Simplification:**
   - *Pro:* Classes provide a more concise and readable syntax for creating constructor functions and defining prototypes.

5. **Instantiation:**
   - *Pro:* Creating instances of objects using classes is straightforward and requires less boilerplate code compared to traditional constructor functions.

6. **Getter and Setter Methods:**
   - *Pro:* Classes support the use of getter and setter methods, allowing better control over access to object properties.

7. **Static Methods:**
   - *Pro:* Classes support the definition of static methods, which are associated with the class itself rather than its instances. This can be useful for utility functions.
  
8. **Private Members:**
   - *Pro:* The availability of private class members addresses the concern about the lack of native support for private members in JavaScript classes.


### Cons:
1. **Function Hoisting:**
   - *Con:* Unlike function declarations, class declarations are not hoisted. This means that you need to declare a class before using it, which can affect the order of your code.

2. **Prototypal Inheritance:**
  - *Con:* `Inheritance` is a very strong coupling relationship in object-oriented programming. It means all behaviors(properties and methods) of the base class are inherited by the subclass by default, which may not always be what you want.

3. **The concept of “Class” doesn’t exist in JavaScript:**
  - *Con:* Javascript uses prototypal inheritance. Even though class notation exists in Javascript, it still uses prototypal inheritance to create the baseclass subclass relationship between classes. Some developers think that the "class" syntax in Javascript is misleading and should be avoided.

**Q2.** How does JavaScript’s object creation differ from a language like Java or Ruby?

**A2.** JavaScript's object creation differs from languages like Java or Ruby primarily in its use of prototypal inheritance instead of class-based inheritance.

In Java or Ruby, objects are typically created using classes, which serve as blueprints defining the structure and behavior of objects. Instances of classes are then created using constructors or instantiation methods.

In contrast, JavaScript employs prototypal inheritance, where objects can inherit properties and methods directly from other objects. Each object in JavaScript has an internal link to another object called its prototype. If a property or method is not found on the object itself, JavaScript looks up the prototype chain until it finds the property or until it reaches the end of the chain.

This approach is more flexible than class-based inheritance, as any object can be used as a prototype for another object, allowing for dynamic and runtime changes to object structures. While JavaScript does have a `class` syntax introduced in ECMAScript 2015 (ES6), it is essentially syntactic sugar over the existing prototype-based inheritance system, providing a more familiar syntax for those coming from class-based languages.

**Q3.** Explain the differences between object constructors and classes.

**A3.** While it's possible to think that classes in javascript are just syntactic sugar over object constructors, in modern Javascript they provide many useful functionalities that are worth to mention.

Here is a simple class declaration example:

```js
class MyClass {
  // Constructor
  constructor() {
    // Constructor body
  }
  // Instance field
  myField = "foo";
  // Instance method
  myMethod() {
    // myMethod body
  }
  // Static field
  static myStaticField = "bar";
  // Static method
  static myStaticMethod() {
    // myStaticMethod body
  }
  // Static block
  static {
    // Static initialization code
  }
  // Fields, methods, static fields, and static methods all have
  // "private" forms
  #myPrivateField = "bar";
}
```

As shown in the example, the class syntax allows declaring instance methods and fields directly on class body. We can also declare static fields and methods within a class. Static properties are properties of the class itself and not of it's instances. It's also possible to declare private fields and methods within a class, private properties are prefixed with a "#".

**Q4.** What are “getters” & “setters”?

**A4.** There are two kinds of object properties.

The first kind is **data properties**. Data properties directly store a value and have attributes associated with them, such as writable, enumerable, and configurable.

The second type of property is **accessor property**. Unlike data properties, accessor properties don't directly hold a value. Instead, they define functions (getters and setters) to retrieve or modify a value. Accessor properties are defined using the `get` and `set` keywords. The get function is called when the property is read, and the set function is called when the property is assigned a new value. From the external code perspective, when you access or modify the property, it appears like a regular property, even though behind the scenes, functions are executed. This allows for more control and customization when getting and setting values.

In JavaScript, accessor properties(getters/setters) are a type of object property that allows you to define **custom behavior** for getting and setting the value of a property. Unlike data properties, which directly store a value, accessor properties define functions to be called when the property is **read (get)** or **written (set)**. These functions are known as getter and setter functions.

Accessor properties are defined using the `get` and `set` keywords within an object literal or added to an existing object using the `Object.defineProperty()` method.

Here's an example to illustrate accessor properties:

```javascript
let person = {
  _name: 'John', // Conventionally, a leading underscore is used to indicate a private variable
  get name() {
    console.log('Getting name');
    return this._name;
  },
  set name(newName) {
    console.log('Setting name to ' + newName);
    this._name = newName;
  }
};

console.log(person.name); // Outputs: Getting name, John
person.name = 'Jane';     // Outputs: Setting name to Jane
console.log(person.name); // Outputs: Getting name, Jane
```

In this example, the `person` object has an accessor property named `name`. The `get` function is called when attempting to access the `name` property, and the `set` function is called when attempting to modify the `name` property. The use of getter and setter functions allows you to perform custom actions or validations when reading or updating the property.

**Q5.** Describe computed names and class fields.

**A5.**
#### computed names [...]
In JavaScript, "computed names" typically refer to the ability to dynamically compute property names for object literals and classes. This feature was introduced in ECMAScript 2015 (ES6) and allows us to use expressions inside square brackets to compute the name of an object property.

Here's an example:

```javascript
let propertyName = 'dynamicProperty';

// Using computed names in object literals
let myObject = {
  [propertyName]: 'Hello, World!',
  // other properties...
};

console.log(myObject.dynamicProperty); // Output: Hello, World!
```

In the example above, the `propertyName` variable is used to dynamically compute the name of the property in the `myObject` object. This is particularly useful when we need to create objects with dynamic property names.

The same concept can be applied to class methods:

```javascript
class MyClass {
  // Using computed names for methods
  [propertyName]() {
    return 'Hello, World!';
  }
}

const myInstance = new MyClass();
console.log(myInstance.dynamicProperty()); // Output: Hello, World!
```

In this case, the method name is dynamically computed using the `propertyName` variable.

Computed names provide flexibility when creating objects and classes, allowing us to use dynamic values to define property names.

#### class fields
Class fields allow developers to define instance variables directly within the class body, making it more convenient and concise compared to the traditional way of defining instance variables in the constructor. Class fields are declared using the `static` keyword for static fields and without the static keyword for instance fields. Both static and instance fields can be either private fields or public fields.

`class` fields are set on individual objects, not on `prototype` (while instance methods are set on the `prototype`).

```js
class MyClass {
  // Public instance field
  publicInstanceField = 10;

  // Private instance field (using '#' syntax)
  #privateInstanceField = 20;

  // Public static field
  static publicStaticField = 30;

  // Private static field (using '#' syntax)
  static #privateStaticField = 40;

  // Constructor
  constructor() {
    // Accessing private instance field within the class is allowed
    console.log(`Private instance field: ${this.#privateInstanceField}`);
  }

  // Methods can also use private fields
  getPrivateInstanceField() {
    return this.#privateInstanceField;
  }

  // Public method accessing private static field
  static getPrivateStaticField() {
    return this.#privateStaticField; // Error: private field '#privateStaticField' must be declared in an enclosing class
  }
}

// Creating an instance of the class
const myInstance = new MyClass();

// Accessing public and private instance fields
console.log(`Public instance field: ${myInstance.publicInstanceField}`);
console.log(`Private instance field: ${myInstance.getPrivateInstanceField()}`);

// Accessing public and private static fields
console.log(`Public static field: ${MyClass.publicStaticField}`);
console.log(`Private static field: ${MyClass.getPrivateStaticField()}`);
```

**Q6.** Describe function binding.

**A6.** 
#### Class fields and function binding
The `this` value in a function change depending on the context of the call.<br>
So if an object method is passed around and called in another context, `this` won’t be a reference to its object any more.

For instance, the following code will show undefined:

```js
class Button {
  constructor(value) {
    this.value = value;
  }

  click() {
    alert(this.value);
  }
}

let button = new Button("hello");

setTimeout(button.click, 1000); // undefined
```


The reason the `this` value changes in the context of setTimeout(button.click, 1000) is related to how the `this` keyword works in JavaScript.

When we pass `button.click` as the first argument to setTimeout, we are passing the method reference without the context of the object (`button`). In JavaScript, when a method is referenced without the object context, the `this` value becomes undefined (or it refers to the global object in non-strict mode).

Class fields provide quite elegant syntax to solve this problem:

```js
class Button {
  constructor(value) {
    this.value = value;
  }
  click = () => {
    alert(this.value);
  }
}

let button = new Button("hello");

setTimeout(button.click, 1000); // hello
```

Arrow functions don't have their own `this` context. Instead, they inherit the `this` value from the enclosing scope. So, if an arrow function is passed as an argument to another function, it retains the `this` value of the surrounding scope.

The class field `click = () => {...}` is created on a per-object basis, there’s a separate function for each `Button` object, with `this` inside it referencing that object. We can pass `button.click` around anywhere, and the value of `this` will always be correct.

**Q7.** Describe static properties.

**A7.** In JavaScript, static properties are properties that are associated with a class itself rather than with instances of the class. Unlike instance properties, which are specific to individual objects created from a class, static properties are shared among all instances of a class and can be accessed directly on the class itself.

Here's an example to illustrate static properties in JavaScript:

```javascript
class MyClass {
  // Instance property
  constructor(name) {
    this.name = name;
  }

  // Static property
  static staticProperty = "I am a static property";

  // Instance method
  display() {
    console.log(`Instance property: ${this.name}`);
  }

  // Static method
  static staticMethod() {
    console.log("This is a static method");
  }
}

// Creating instances of the class
const obj1 = new MyClass("Object 1");
const obj2 = new MyClass("Object 2");

// Accessing instance property and calling instance method
obj1.display(); // Output: Instance property: Object 1

// Accessing static property and calling static method
console.log(MyClass.staticProperty); // Output: I am a static property
MyClass.staticMethod(); // Output: This is a static method
```

In this example, `staticProperty` is a static property of the `MyClass` class, while `name` is an instance property specific to each object created from the class. Similarly, `staticMethod` is a static method, which can be called directly on the class, while `display` is an instance method that operates on individual instances of the class.

Static properties `(static fields, methods, getter/setters)` are often used for values or functionality that are associated with the class as a whole, rather than with instances of the class.

**Q8.** Describe private class features.

**A8.** Fields, methods, getters, and setters can be private. They're useful when you have something complex that the class needs to do internally but no other part of the code should be allowed to call.

 Private properties get created by using a hash # prefix and cannot be legally referenced outside of the class. The privacy encapsulation of these class properties is enforced by JavaScript itself.

 ```js
 class ClassWithPrivate {
  #privateField;
  #privateFieldWithInitializer = 42;

  #privateMethod() {
    // …
  }

  static #privateStaticField;
  static #privateStaticFieldWithInitializer = 42;

  static #privateStaticMethod() {
    // …
  }
}
```

**Q9.** How is inheritance used with classes?

**A9.**
#### `extends` and inheritance
The `extends` keyword is used in class declarations or class expressions to create a class as a child of another constructor (either a class or a function).

In JavaScript, the extends keyword is used to create a subclass (derived class) that inherits from another class (base class). 

Here's a breakdown of how `extends` works in JavaScript classes:

1. **Defining a Base Class (Superclass):**
   You start by defining a base class using the `class` keyword. This class serves as the template for other classes that will inherit from it.

    ```javascript
    class Animal {
      constructor(name) {
        this.name = name;
      }

      makeSound() {
        console.log("Some generic sound");
      }
    }
    ```

2. **Creating a Subclass (Derived Class) with `extends`:**
   You can create a subclass that inherits from the base class using the `extends` keyword. The subclass can have its own methods and properties, and it inherits the methods and properties from the base class.

    ```javascript
    class Dog extends Animal {
      constructor(name, breed) {
        // Call the constructor of the base class using super()
        super(name);
        this.breed = breed;
      }

      // You can override methods from the base class
      makeSound() {
        console.log("Bark! Bark!");
      }

      // You can also add new methods specific to the subclass
      fetch() {
        console.log(`${this.name} is fetching the ball.`);
      }
    }
    ```

3. **`super` Keyword:**
   In the constructor of the subclass, you use the `super()` keyword to call the constructor of the base class. This is necessary to initialize the properties inherited from the base class.

    ```javascript
    class Dog extends Animal {
      constructor(name, breed) {
        // Call the constructor of the base class using super()
        // It is a language requirement to call `super()` before accessing `this`. The `super()` call calls the parent class's constructor to initialize `this`.
        super(name);
        this.breed = breed;
      }
    }
    ```

4. **Overriding Methods:**
   Subclasses can override methods from the base class by redefining them. In the example above, the `makeSound` method is overridden in the `Dog` subclass.

5. **Adding New Methods and Properties:**
   Subclasses can also have their own methods and properties in addition to those inherited from the base class.

    ```javascript
    class Dog extends Animal {
      // ... (constructor and other methods)

      // You can also add new methods specific to the subclass
      fetch() {
        console.log(`${this.name} is fetching the ball.`);
      }
    }
    ```

Here's an example of how you might use these classes:

```javascript
// Create an instance of the base class
const genericAnimal = new Animal("Generic Animal");
genericAnimal.makeSound();  // Outputs: Some generic sound

// Create an instance of the subclass
const myDog = new Dog("Buddy", "Golden Retriever");
myDog.makeSound();  // Outputs: Bark! Bark!
myDog.fetch();      // Outputs: Buddy is fetching the ball.
```

In this example, `Dog` is a subclass that extends the `Animal` base class, demonstrating the use of the `extends` keyword in JavaScript class inheritance.

The derived class has access to all public properties of the parent class.

Within derived classes, you can access the parent class's methods by using `super`. This allows you to build enhancement methods and avoid code duplication.

When you use `extends`, the static methods inherit from each other as well, so you can also override or enhance them.

```js
class ColorWithAlpha extends Color {
  // ...
  static isValid(r, g, b, a) {
    // Call the parent class's isValid() and build on the return value
    return super.isValid(r, g, b) && a >= 0 && a <= 1;
  }
}

console.log(ColorWithAlpha.isValid(255, 0, 0, -1)); // false
```

Derived classes don't have access to the parent class's private fields — this is another key aspect to JavaScript private fields being "hard private". Private fields are scoped to the class body itself and do not grant access to any outside code.

A class can only extend from one class. However, due to the dynamic nature of JavaScript, it's still possible to achieve the effect of multiple inheritance through `class composition` and `mixins`.

Instances of derived classes are also instances of the base class.

```js
const color = new ColorWithAlpha(255, 0, 0, 0.5);
console.log(color instanceof Color); // true
console.log(color instanceof ColorWithAlpha); // true
```

The `extends` keyword not only establishes a prototype link between the child and parent classes but also sets up the prototype chain for instances created from those classes. `extends` sets the prototype for both `ChildClass` and `ChildClass.prototype`. 

```js
class ParentClass {}
class ChildClass extends ParentClass {}

// Allows inheritance of static properties
Object.getPrototypeOf(ChildClass) === ParentClass;
// Allows inheritance of instance properties
Object.getPrototypeOf(ChildClass.prototype) === ParentClass.prototype;
```

**Q10.** Why is favoring Composition over Inheritance suggested?

**A10.**
#### `Composition` / Avoiding inheritance
`Inheritance` is a very strong coupling relationship in object-oriented programming. It means all behaviors(properties and methods) of the base class are inherited by the subclass by default, which may not always be what you want.

`Composition` on the other hand, refers to a design pattern where a class is created by combining multiple smaller classes or objects to form a new class. Instead of using inheritance, where a class inherits properties and methods from a single parent class, composition allows you to build a class by assembling various components.

In JavaScript, classes are created using the `class` keyword, and composition can be achieved by creating **instances** of other classes within a class constructor or methods. This promotes code reusability and flexibility, as you can mix and match different components to create new classes without relying on a strict hierarchy.

Here's a simple example to illustrate composition in JavaScript:

```javascript
// Component A
class Engine {
  start() {
    console.log('Engine started');
  }
}

// Component B
class Wheels {
  roll() {
    console.log('Wheels rolling');
  }
}

// Class using composition
class Car {
  constructor() {
    this.engine = new Engine();
    this.wheels = new Wheels();
  }

  drive() {
    this.engine.start();
    this.wheels.roll();
    console.log('Car is moving');
  }
}

// Creating an instance of the composed class
const myCar = new Car();
myCar.drive();
```

In this example, the `Car` class is composed of an `Engine` and `Wheels`. Instead of inheriting from these components, the `Car` class creates instances of them within its constructor. This approach allows for a more modular and flexible code structure.

In general, unless there's a very good reason to use inheritance, it's better to use composition instead. **Composition means that a class has a reference to an object of another class, and only uses that object as an implementation detail.**

Composition is often favored over inheritance in modern JavaScript development because it reduces tight coupling, makes the code more maintainable, and avoids some of the pitfalls associated with the classical inheritance model.

Here is an another example to composition:

```js
class ReadOnlyMap {
  #data;
  constructor(values) {
    this.#data = new Map(values);
  }
  get(key) {
    return this.#data.get(key);
  }
  has(key) {
    return this.#data.has(key);
  }
  get size() {
    return this.#data.size;
  }
  *keys() {
    yield* this.#data.keys();
  }
  *values() {
    yield* this.#data.values();
  }
  *entries() {
    yield* this.#data.entries();
  }
  *[Symbol.iterator]() {
    yield* this.#data[Symbol.iterator]();
  }
}
```

In this case, the ReadOnlyMap class is not a subclass of Map, but it still implements most of the same methods. This means more code duplication, but it also means that the ReadOnlyMap class is not strongly coupled to the Map class, and does not easily break if the Map class is changed.
