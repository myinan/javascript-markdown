# Fundamentals Part 5

## Git Branching
Like the branches in a tree (hence the name), all of the branches for a project stem off of a “trunk” (the main branch) or off of other branches.

When you make commits on a specific branch, those changes only exist on that branch, leaving all of your other branches exactly as they were when you branched off of them.

This means that you can keep your main branch as a place for only finished features that you know are working properly, and add each feature to your project using dedicated branches which we call feature branches.

### Using Branches
You can make new branches by using the command `git branch <branch_name>`. You can then change to your new branch using `git checkout <branch_name>`. You can also create a new branch and change to it in a single command by using the -b flag with checkout, in the form `git checkout -b <branch_name>`.

You can see all of your current branches using `git branch` with no other arguments. The branch that you’re currently on will be indicated with an asterisk. If you want to change back to main from any other branch, you can do so just like changing to any other branch using `git checkout main`.

Once you are done working on your feature branch and are ready to bring the commits that you’ve made on it to your main branch, you will need to perform what is known as a `merge`.

Merges are done by using the command `git merge <branch_name>` which will take the changes you’ve committed in `branch_name` and add them to the branch that you’re currently on. You can see an example of a `develop` branch being created, committed to, and then merged to `main` in the diagram below.

```bash
---
title: Example of Git Branching
---
gitGraph
   commit id: "commit1"
   commit id: "commit2"
   branch develop
   checkout develop
   commit id: "commit1a"
   commit id: "commit2a"
   checkout main
   merge develop id: "merge to main"
```

Sometimes, the same lines in a file will have been changed by two different branches. When this happens, you will have a merge conflict when you try and merge those branches together. In order to finish merging the branches you will have to first resolve the conflict.

When you don’t need a branch anymore, it can be deleted using `git branch -d <branch_name>` if the branch has already been merged into main, or with `git branch -D <branch_name>` if it hasn’t. You will usually want to delete branches when you’re done with them, otherwise they can pile up and make it more difficult to find the branch you’re looking for when you need it.

### Resolving Merge Conflicts
Resolving merge conflicts in Git is a common task when collaborating with others on a shared codebase or when dealing with changes on different branches. A merge conflict occurs when Git can't automatically combine changes from different branches because they overlap or conflict with each other. Here's a step-by-step guide on how to resolve merge conflicts:

#### Step 1: Ensure you have the latest changes
Before starting any merge, ensure your local repository is up-to-date by fetching and pulling changes from the remote repository:
```bash
git fetch
git pull
```

#### Step 2: Checkout the target branch
Switch to the branch where you want to merge the changes. For example, if you want to merge changes from `feature-branch` into `main`, you can do:
```bash
git checkout main
```

#### Step 3: Merge the branches
Use the `git merge` command to merge the changes from the source branch into the target branch:
```bash
git merge feature-branch
```

#### Step 4: Identify the conflicts
If there are any conflicting changes, Git will notify you and list the files with conflicts.

#### Step 5: Open the conflicted file
Open the files with conflicts using a text editor or an IDE.

#### Step 6: Resolve the conflicts
Edit the conflicted files manually to resolve the conflicts. Remove the conflict markers (<<<<<<<, =======, >>>>>>>) and choose which changes to keep from both branches. Make sure the final code is functional and makes sense.

#### Step 7: Save the changes
Save the modified files after resolving the conflicts.

#### Step 8: Add and commit the changes
After resolving the conflicts, stage the changes and commit them:
```bash
git add path/to/conflicted-file
git commit -m "Resolve merge conflicts with feature-branch"
```

#### Step 9: Verify the merge
After committing the resolved changes, verify that everything works as expected. Test your code to ensure the merge was successful.

#### Step 10: Optional - Delete the source branch (if needed)
If you no longer need the source branch, you can delete it:
```bash
git branch -d feature-branch
```

Note that you should only delete the source branch if you're sure you won't need it anymore.

## Objects
In JavaScript, objects are fundamental data structures used to represent and store collections of related data and functionality. They are one of the most important concepts in the language and serve as the building blocks for various data structures and paradigms like Object-Oriented Programming (OOP). In this detailed explanation, we'll cover the following aspects of objects in JavaScript:

1. Object Basics
2. Creating Objects
3. Properties and Methods
4. Accessing and Modifying Properties
5. Object Prototypes and Inheritance
6. The "this" Keyword
7. Object Constructors and Classes

Let's delve into each of these topics:

### Object Basics:
An object in JavaScript is an unordered collection of key-value pairs. Each key is associated with a value. Property keys must be strings or symbols (usually strings). The value can be any JavaScript data type, including other objects. Objects can also contain functions, which are known as methods when they are associated with an object.

Objects in JavaScript are dynamic, meaning you can add, modify, or remove properties and methods at runtime, allowing for great flexibility in your code.

### Creating Objects:
There are multiple ways to create objects in JavaScript:

#### a. Object Literal:
The simplest way to create an object is using an object literal, denoted by curly braces:

```javascript
const person = {
  name: "John",
  age: 30,
  profession: "Engineer",
};
```

#### b. Object Constructor:
You can use the `Object` constructor to create an empty object and then add properties and methods to it:

```javascript
const person = new Object();
person.name = "John";
person.age = 30;
person.profession = "Engineer";
```

#### c. Object.create():
You can also create an object with a specific prototype using `Object.create()`:

```javascript
const personPrototype = {
  greet: function () {
    return `Hello, my name is ${this.name}.`;
  },
};

const person = Object.create(personPrototype);
person.name = "John";
person.age = 30;
person.profession = "Engineer";
```

### Properties and Methods:
Properties in objects are accessed using keys. For example, in the `person` object we defined earlier, `name`, `age`, and `profession` are properties. Properties can hold any valid JavaScript value, including strings, numbers, arrays, other objects, etc.

Methods are functions defined as values of object properties. In the example above, the `greet` function inside the `personPrototype` is a method.

### Accessing and Modifying Properties:
You can access properties using dot notation or square brackets:

```javascript
console.log(person.name); // Output: "John"
console.log(person["age"]); // Output: 30
```

To modify a property:

```javascript
person.name = "Alice";
person["age"] = 25;
```

### Object Prototypes and Inheritance:
In JavaScript, objects can inherit properties and methods from other objects through their prototypes. When accessing a property or method on an object, if the property is not found in the object itself, JavaScript looks for it in the object's prototype, then the prototype's prototype, and so on, until it reaches the top-level `Object.prototype`. This is known as the prototype chain.

```javascript
const personPrototype = {
  greet: function () {
    return `Hello, my name is ${this.name}.`;
  },
};

const person = Object.create(personPrototype);
person.name = "John";
person.age = 30;
person.profession = "Engineer";

console.log(person.greet()); // Output: "Hello, my name is John."
```

### The "this" Keyword:
The `this` keyword inside a method refers to the object on which the method is called. It allows methods to access and operate on the object's properties.

```javascript
const person = {
  name: "John",
  greet: function () {
    return `Hello, my name is ${this.name}.`;
  },
};

console.log(person.greet()); // Output: "Hello, my name is John."
```

### Object Constructors and Classes:
In more advanced scenarios, you may want to create multiple objects with similar properties and methods. For this, you can use object constructors or ES6 classes.

#### a. Object Constructor:
A constructor is just a function called using the `new` keyword. When you call a constructor, it will:

+ create a new object
+ bind `this` to the new object, so you can refer to `this` in your constructor code
+ run the code in the constructor
+ return the new object.

Constructors, by convention, start with a capital letter and are named for the type of object they create.

```javascript
function Person(name, age, profession) {
  this.name = name;
  this.age = age;
  this.profession = profession;
}

Person.prototype.greet = function () {
  return `Hello, my name is ${this.name}.`;
};

// To call Person() as a constructor, we use new:
const john = new Person("John", 30, "Engineer");
console.log(john.greet()); // Output: "Hello, my name is John."
```

#### b. ES6 Class:

```javascript
class Person {
  constructor(name, age, profession) {
    this.name = name;
    this.age = age;
    this.profession = profession;
  }

  greet() {
    return `Hello, my name is ${this.name}.`;
  }
}

const john = new Person("John", 30, "Engineer");
console.log(john.greet()); // Output: "Hello, my name is John."
```

Both approaches achieve the same result, but classes provide a more concise and familiar syntax for creating objects.

In summary, objects in JavaScript are versatile data structures that store related data and functionality using key-value pairs. They are the foundation of many programming patterns in JavaScript, including Object-Oriented Programming.

## A Further Dive into "Arrays" in JavaScript
Now that we have an idea about what objects are in JavaScript, it's time to understand arrays more accurately.

In JavaScript, arrays are a specific type of object. Arrays are a special kind of object designed to store and manage ordered collections of data, typically indexed by numerical values (0-based index).

In JavaScript, objects are collections of key-value pairs, where the keys are strings (or Symbols) and the values can be any data type, including other objects. Arrays, on the other hand, are a specific type of object with additional features specifically tailored for handling ordered collections of data.

The key difference between a regular object and an array is how they are internally implemented and how they handle the data:

1. **Arrays use numeric indices:** Arrays use integer indices to access and store elements, starting from 0. They also provide built-in methods for adding, removing, and manipulating elements, such as push, pop, splice, etc. Though, like a regular object, values stored inside an array can be of any data type.

2. **Objects use string keys:** Objects use strings (or Symbols) as keys to access and store properties. They are more suitable for storing named properties and are often used for key-value mappings.

However, it's essential to understand that, despite being a type of object, arrays have specific behaviors and methods that distinguish them from regular objects. When using arrays, you get access to array-specific methods and properties, like `length`, `push`, `pop`, `splice`, `forEach`, and more, which makes working with ordered collections of data more convenient.

### Array methods and properties
Arrays are fundamental data structures in JavaScript that allow us to store and manipulate collections of elements. They are widely used to manage and manipulate data efficiently. JavaScript provides a rich set of built-in methods and properties that make it easier to work with arrays. Here are some of the most commonly used methods in JavaScript:

#### 1. `push()` Method

The `push()` method adds one or more elements to the end of an array and returns the new length of the array. It is a simple way to append elements to an existing array.

```javascript
const fruits = ['apple', 'banana', 'orange'];
fruits.push('grape', 'kiwi');
// fruits is now ['apple', 'banana', 'orange', 'grape', 'kiwi']
```

#### 2. `pop()` Method

The `pop()` method removes the last element from an array and returns that element. It is used to efficiently remove elements from the end of an array.

```javascript
const numbers = [1, 2, 3, 4, 5];
const removedNumber = numbers.pop();
// numbers is now [1, 2, 3, 4], and removedNumber is 5
```

#### 3. `shift()` Method

The `shift()` method removes the first element from an array and shifts all remaining elements to a lower index. It returns the removed element.

```javascript
const colors = ['red', 'blue', 'green'];
const removedColor = colors.shift();
// colors is now ['blue', 'green'], and removedColor is 'red'
```

#### 4. `unshift()` Method

The `unshift()` method adds one or more elements to the beginning of an array and returns the new length of the array. It is often used to prepend elements to an array.

```javascript
const animals = ['dog', 'cat', 'rabbit'];
const newLength = animals.unshift('elephant', 'lion');
// animals is now ['elephant', 'lion', 'dog', 'cat', 'rabbit']
```

#### 5. `concat()` Method

The `concat()` method is used to merge two or more arrays together, creating a new array containing all the elements of the combined arrays.

```javascript
const array1 = [1, 2, 3];
const array2 = [4, 5, 6];
const combinedArray = array1.concat(array2);
// combinedArray is [1, 2, 3, 4, 5, 6]
```

#### 6. `slice()` Method

The `slice()` method returns a shallow copy of a portion of an array, specified by a starting and ending index. It does not modify the original array.

```javascript
const originalArray = [1, 2, 3, 4, 5];
const slicedArray = originalArray.slice(1, 4);
// slicedArray is [2, 3, 4], originalArray is unchanged
```

#### 7. `splice()` Method

The `splice()` method changes the contents of an array by removing or replacing existing elements and/or adding new elements. It can be used for various array manipulation tasks.

```javascript
const months = ['January', 'February', 'June'];
months.splice(2, 0, 'March', 'April', 'May');
// months is now ['January', 'February', 'March', 'April', 'May', 'June']
```

#### 8. `forEach()` Method

The `forEach()` method iterates over each element in an array and executes a provided function for each element. It is often used for side-effect operations.

```javascript
const numbers = [1, 2, 3, 4, 5];
numbers.forEach(function(number) {
  console.log(number * 2);
});
// Output: 2, 4, 6, 8, 10
```

#### 9. `map()` Method

The `map()` method creates a new array by applying a provided function to each element of the calling array. It is commonly used to transform data.

```javascript
const numbers = [1, 2, 3, 4, 5];
const doubledNumbers = numbers.map(function(number) {
  return number * 2;
});
// doubledNumbers is [2, 4, 6, 8, 10]
```

#### 10. `filter()` Method

The `filter()` method creates a new array with all elements that pass a test implemented by the provided function. It is used to filter out elements based on certain conditions.

```javascript
const ages = [18, 25, 30, 16, 22];
const adults = ages.filter(function(age) {
  return age >= 18;
});
// adults is [18, 25, 30, 22]
```

#### 11. `indexOf()` Method

The `indexOf()` method searches the array for a specified element and returns the first index at which the element is found. If the element is not found, it returns -1.

```javascript
const animals = ['dog', 'cat', 'rabbit'];
const catIndex = animals.indexOf('cat');
// catIndex is 1
```

#### 12. `includes()` Method

The `includes()` method determines whether an array includes a certain element. It returns `true` if the element is found, otherwise `false`.

```javascript
const numbers = [1, 2, 3, 4, 5];
const includesThree = numbers.includes(3);
// includesThree is true
```


#### 13. `length` Property

The `length` property of an array returns the number of elements in the array. It can be used to determine the size of an array.

```javascript
const fruits = ['apple', 'banana', 'orange'];
const numberOfFruits = fruits.length;
// numberOfFruits is 3
```


## [A comprehensive guide from javascript.info that goes over all Array methods in JavaScript](https://javascript.info/array-methods "javascript.info")


### Array Methods Cheat Sheet

#### To add/remove elements:

- `push(...items)`: adds items to the end.
- `pop()`: extracts an item from the end.
- `shift()`: extracts an item from the beginning.
- `unshift(...items)`: adds items to the beginning.

#### To modify elements:

- `splice(pos, deleteCount, ...items)`: deletes `deleteCount` elements at index `pos` and inserts `items`.
- `slice(start, end)`: creates a new array and copies elements from index `start` to `end` (not inclusive) into it.
- `concat(...items)`: returns a new array by copying all members of the current array and adding `items` to it. If any item is an array, its elements are included.

#### To search among elements:

- `indexOf/lastIndexOf(item, pos)`: looks for `item` starting from position `pos` and returns the index or -1 if not found.
- `includes(value)`: returns `true` if the array contains `value`, otherwise `false`.
- `find/filter(func)`: filters elements through the function and returns the first/all values that make it return true.
- `findIndex(func)`: similar to `find`, but returns the index instead of a value.

#### To iterate over elements:

- `forEach(func)`: calls `func` for every element, does not return anything.

#### To transform the array:

- `map(func)`: creates a new array from results of calling `func` for every element.
- `sort(func)`: sorts the array in-place and returns it.
- `reverse()`: reverses the array in-place and returns it.
- `split/join`: converts a string to an array and back.
- `reduce/reduceRight(func, initial)`: calculates a single value over the array by calling `func` for each element and passing an intermediate result between the calls.

**Additionally**;

- `Array.isArray(value)`: checks if `value` is an array, returning `true` or `false`.

**Note**: Methods `sort`, `reverse`, and `splice` modify the array itself.

These methods are the most used ones, they cover 99% of use cases. But there are few others:

#### Other methods:

- `arr.some(fn)/arr.every(fn)`: checks the array using the function `fn`. If any/all results are `true`, `some` returns `true`, and `every` returns `false`. These methods are similar to the `||` and `&&` operators.

```javascript
// We can use every(fn) to compare arrays:
function arraysEqual(arr1, arr2) {
  return arr1.length === arr2.length && arr1.every((value, index) => value === arr2[index]);
}

alert(arraysEqual([1, 2], [1, 2])); // true
```

- `arr.fill(value, start, end)`: fills the array with the repeating `value` from index `start` to `end`.

- `arr.copyWithin(target, start, end)`: copies its elements from position `start` to `end` into itself, at position `target` (overwriting existing elements).

- `arr.flat(depth)/arr.flatMap(fn)`: creates a new flat array from a multidimensional array.

---
### Knowledge Check

**Q1.** What is the difference between objects and arrays?

**A1.** In javascript, arrays are a special type of object. With objects, values are indexed with strings (as key-value pairs). With arrays on the other hand, numbered indexes are used. Arrays also have their own methods and properties.

**Q2.** How do you access object properties?

**A2.** Object properties are accessed with either dot(.) notation or bracket([]) notation. For example:

```javascript
const obj = {
  name: "John",
  age: "30",
};

console.log(obj.name); // "John"
console.log(obj["age"]); // "30"
```

**Q3.** What is Array.prototype.map() useful for?

**A3.** `Array.prototype.map()` method iterates over the every item of the array, runs the function passed as the argument for every item iterated, then returns a new array with the modified items. `Array.prototype.forEach()` on the other hand, walks every item, runs the callback function for every item but modifies the items of the array and does not return anything(returns undefined).

**Q4.** What is Array.prototype.reduce() useful for?

**A4.** `Array.prototype.reduce()` takes a function as a parameter, this function has also two of it's own parameters, an "accumulator" parameter and an "item" parameter. "item" parameter represents the current item of the array that function is currently handling, the "accumulator" parameter on the other hand represents the value returned by the reduce() methods previous iteration. After the last iteration, reduce() method returns the value of the "accumulator" parameter.


