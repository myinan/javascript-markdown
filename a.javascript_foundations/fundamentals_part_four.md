# Fundamentals Part 4

## Arrays
Arrays in JavaScript are fundamental data structures used to store multiple values in a single variable. They are a type of object that allows you to store and manipulate a collection of elements, which can be of any data type, such as numbers, strings, objects, or even other arrays. Arrays are commonly used for organizing and working with lists of related data.

1. **Creating an Array:**
You can create an array in JavaScript using two methods: array literals and the `Array` constructor.

- Using array literals:
```javascript
const fruits = ['apple', 'banana', 'orange'];
```

- Using the `Array` constructor:
```javascript
const numbers = new Array(1, 2, 3, 4, 5);
```

The two examples above do exactly the same.
<br>There is no need to use new Array().
<br>For simplicity, readability and execution speed, use the array literal method.

2. **Accessing Elements:**
Array elements are accessed using zero-based indexing, meaning the first element is at index 0, the second element is at index 1, and so on.

JavaScript does not support arrays with named indexes. In JavaScript, arrays always use numbered indexes.  

```javascript
const fruits = ['apple', 'banana', 'orange'];
console.log(fruits[0]); // Output: 'apple'
console.log(fruits[1]); // Output: 'banana'
console.log(fruits[2]); // Output: 'orange'
```

3. **Array Length:**
The `length` property of an array returns the number of elements it contains.

```javascript
const fruits = ['apple', 'banana', 'orange'];
console.log(fruits.length); // Output: 3
```

4. **Modifying Elements:**
You can modify array elements by assigning new values to specific indices.

```javascript
const fruits = ['apple', 'banana', 'orange'];
fruits[1] = 'grape';
console.log(fruits); // Output: ['apple', 'grape', 'orange']
```

5. **Adding and Removing Elements:**
JavaScript provides several methods to add and remove elements from an array.

- Adding elements:
  - `push`: Adds one or more elements to the end of the array.
  - `unshift`: Adds one or more elements to the beginning of the array.

```javascript
const fruits = ['apple', 'banana'];
fruits.push('orange');
fruits.unshift('grape');
console.log(fruits); // Output: ['grape', 'apple', 'banana', 'orange']
```

- Removing elements:
  - `pop`: Removes the last element from the array and returns it.
  - `shift`: Removes the first element from the array and returns it.

```javascript
const fruits = ['apple', 'banana', 'orange'];
const removedElement = fruits.pop();
console.log(removedElement); // Output: 'orange'
console.log(fruits); // Output: ['apple', 'banana']
```

6. **Array Methods:**
Arrays come with numerous built-in methods that allow you to manipulate and transform their elements efficiently. Some commonly used array methods include:
   - `slice`: Returns a new array containing a portion of the original array.
   - `splice`: Adds or removes elements from an array at a specific index.
   - `concat`: Joins two or more arrays and returns a new array.
   - `indexOf`: Returns the index of the first occurrence of a specified element.
   - `includes`: Checks if the array includes a certain element.
   - `map`: Creates a new array by applying a function to each element of the original array.
   - `filter`: Creates a new array with elements that pass a certain condition.
   - `reduce`: Reduces an array to a single value by applying a function to each element.

7. **Multidimensional Arrays:**
JavaScript allows you to create arrays of arrays, forming multidimensional arrays.

```javascript
const matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]];
console.log(matrix[1][2]); // Output: 6
```

8. **Array Iteration:**
You can loop through the elements of an array using various iteration methods, such as `for`, `for...of`, and `forEach`.

```javascript
const fruits = ['apple', 'banana', 'orange'];

// Using for loop
for (let i = 0; i < fruits.length; i++) {
  console.log(fruits[i]);
}

// Using for...of loop
for (const fruit of fruits) {
  console.log(fruit);
}

// Using forEach method
fruits.forEach(fruit => console.log(fruit));
```

9. **Array Destructuring:**
ES6 introduced array destructuring, which allows you to extract values from arrays easily.

```javascript
const fruits = ['apple', 'banana', 'orange'];
const [firstFruit, secondFruit] = fruits;
console.log(firstFruit); // Output: 'apple'
console.log(secondFruit); // Output: 'banana'
```

Arrays are powerful and versatile data structures that play a crucial role in JavaScript programming. They are used extensively to handle collections of data and simplify many tasks, including sorting, filtering, and processing data in web development and other JavaScript applications.

### Arrays are Objects in JavaScript
In JavaScript, arrays are a specific type of object. The typeof operator in JavaScript returns "object" for arrays. Arrays are considered a special kind of object because they inherit from the `Array` constructor, which is itself a built-in constructor function in JavaScript.

In JavaScript, arrays use numbered indexes, while objects use named indexes.
Arrays are a special kind of objects, with numbered indexes.

The key difference between arrays and regular objects lies in how they store and manage their data:

1. **Indexed Properties:** Arrays use numerical indices to access and manage elements. Each element in the array is associated with an index, starting from 0 for the first element, 1 for the second element, and so on. The indices represent the order of elements in the array.

```javascript
const fruits = ['apple', 'banana', 'orange'];
console.log(fruits[0]); // Output: 'apple'
console.log(fruits[1]); // Output: 'banana'
console.log(fruits[2]); // Output: 'orange'
```

2. **Length Property:** Arrays have a `length` property that automatically updates based on the number of elements in the array. When you add or remove elements, the `length` property adjusts accordingly.

```javascript
const numbers = [1, 2, 3, 4];
console.log(numbers.length); // Output: 4

numbers.push(5);
console.log(numbers.length); // Output: 5

numbers.pop();
console.log(numbers.length); // Output: 4
```

3. **Array Methods:** Arrays come with several built-in methods (e.g., `push`, `pop`, `slice`, `map`, `forEach`, etc.) that allow you to manipulate and interact with the array elements easily.

```javascript
const numbers = [1, 2, 3, 4];
numbers.push(5); // Adds an element to the end of the array
numbers.pop(); // Removes the last element from the array
numbers.forEach(num => console.log(num)); // Iterates through the array
```

4. **Array-Specific Prototypes:** Arrays inherit additional methods and properties from `Array.prototype`, which regular objects don't have. These array-specific prototypes make array manipulation more convenient.

```javascript
const fruits = ['apple', 'banana', 'orange'];
console.log(fruits.join(', ')); // Output: 'apple, banana, orange'
console.log(fruits.indexOf('banana')); // Output: 1
```

Although arrays are objects in JavaScript, they have additional behaviors and functionalities that are specific to arrays, making them a useful and versatile data structure for managing collections of data in an ordered manner.

### Arrays are the primary data structure for handling collections of data in JavaScript
The versatility of arrays and objects provide a wide range of options for handling collections of data in JavaScript.

1. **Arrays:** As we discussed earlier, arrays are the primary data structure for handling collections of data in JavaScript. They are versatile and widely used for storing ordered collections of elements.

2. **Objects:** JavaScript objects can be used to represent collections of key-value pairs. While objects are not ordered like arrays, they are useful when you want to access data using descriptive keys.

```javascript
const person = {
  name: 'John',
  age: 30,
  city: 'New York'
};
```

3. **Maps:** ES6 introduced the `Map` data structure, which allows you to create collections of key-value pairs similar to objects, but with some key differences. Maps can have any data type as keys and maintain the insertion order.

```javascript
const myMap = new Map();
myMap.set('name', 'John');
myMap.set('age', 30);
myMap.set('city', 'New York');
```

4. **Sets:** ES6 also introduced the `Set` data structure, which allows you to store unique values. Sets can be used to eliminate duplicates from arrays.

```javascript
const mySet = new Set([1, 2, 3, 3, 4, 5]);
console.log(mySet); // Output: Set { 1, 2, 3, 4, 5 }
```

5. **Typed Arrays:** JavaScript has typed arrays that are used to work with binary data and manipulate raw memory. They provide more efficient storage and manipulation of large amounts of numerical data.

```javascript
const intArray = new Int32Array([1, 2, 3, 4, 5]);
console.log(intArray); // Output: Int32Array [1, 2, 3, 4, 5]
```

6. **Arrays of Objects:** You can use arrays to store objects, effectively creating collections of objects.

```javascript
const students = [
  { name: 'Alice', age: 22 },
  { name: 'Bob', age: 25 },
  { name: 'Carol', age: 21 }
];
```

## Loops
Loops are an essential programming construct in JavaScript (and many other programming languages) that allow you to execute a block of code repeatedly. Loops are used to efficiently perform repetitive tasks, iterate over collections of data, and process elements one by one. In JavaScript, there are several types of loops, but the most commonly used ones are the "for loop," "while loop," and "do-while loop."

### 1. For Loop
The `for` loop is the most common type of loop in JavaScript. It has a compact syntax and is well-suited for iterating over a fixed number of elements or for specifying a specific range.

The general syntax of a `for` loop looks like this:

```javascript
for (initialization; condition; update) {
  // code to be executed in each iteration
}
```

- **Initialization:** This part is executed only once before the loop starts. It's usually used to set up a loop control variable.

- **Condition:** The loop will continue to execute as long as this condition is true. If the condition evaluates to `false` at the beginning, the loop will not execute at all.

- **Update:** This part is executed after each iteration and is used to update the loop control variable. It helps to control the loop's termination.

Example: Printing numbers from 1 to 5 using a `for` loop:

```javascript
for (let i = 1; i <= 5; i++) {
  console.log(i); // Output: 1 2 3 4 5
}
```

#### "for...of" loop

In JavaScript, the "for...of" loop is a convenient and concise way to iterate over the elements of an iterable object, such as arrays, strings, maps, sets, and more. It provides a simpler syntax compared to the traditional "for" loop and is particularly useful when you need to perform a specific operation for each item in the collection.

The basic syntax of the "for...of" loop is as follows:

```javascript
for (const element of iterable) {
  // Code to be executed for each element
}
```

Here's a breakdown of the components:

1. `element`: This is a variable that will take the value of each element in the iterable as the loop iterates. You can choose any valid variable name to represent the current element.

2. `of`: The keyword "of" is used to specify that you want to iterate over the elements of the iterable.

3. `iterable`: This is the object that you want to loop through. It could be an array, a string, a map, a set, or any other iterable object.

Let's look at some examples:

1. Iterating over an array:

```javascript
const numbers = [1, 2, 3, 4, 5];

for (const num of numbers) {
  console.log(num);
}
```

Output:
```
1
2
3
4
5
```

2. Iterating over a string:

```javascript
const message = "Hello, World!";

for (const char of message) {
  console.log(char);
}
```

Output:
```
H
e
l
l
o
,
 
W
o
r
l
d
!
```

Of course, we can also use the standart `for loop` to iterate through an iterable.

```javascript
const cats = ["Leopard", "Serval", "Jaguar", "Tiger", "Caracal", "Lion"];

for (let i = 0; i < cats.length; i++) {
  console.log(cats[i]);
}
```

### 2. While Loop
The `while` loop is used when you want to repeat a block of code as long as a certain condition remains true. Unlike the `for` loop, the `while` loop doesn't require an explicit initialization and update, making it more flexible for certain scenarios.

The general syntax of a `while` loop is as follows:

```javascript
initializer
while (condition) {
  // code to run

  final-expression
}
```

- **Condition:** The loop will execute repeatedly as long as this condition evaluates to `true`. If the condition is `false` at the beginning, the loop will not execute at all.

Example: Print numbers from 1 to 5 using a `while` loop:

```javascript
let i = 1;
while (i <= 5) {
  console.log(i); // Output: 1 2 3 4 5
  i++;
}
```

### 3. Do-While Loop
The `do-while` loop is similar to the `while` loop but with a small difference: the code inside the loop will execute at least once before checking the loop condition. This ensures that the loop runs at least once, regardless of whether the condition is initially true or false.

The general syntax of a `do-while` loop is as follows:

```javascript
initializer
do {
  // code to run

  final-expression
} while (condition)
```

- **Condition:** The loop will continue to execute as long as this condition remains `true`. If the condition is `false` at the beginning, the loop will still execute once.

Example: Print numbers from 1 to 5 using a `do-while` loop:

```javascript
let i = 1;
do {
  console.log(i); // Output: 1 2 3 4 5
  i++;
} while (i <= 5);
```

### Breaking and Continuing
Inside loops, you can use the `break` statement to exit the loop prematurely, even if the loop condition is still true. The `continue` statement can be used to skip the rest of the current iteration and jump to the next iteration.

Example: Using `break` and `continue` in a loop:

```javascript
for (let i = 1; i <= 10; i++) {
  if (i === 5) {
    continue; // Skip the rest of the iteration when i is 5
  }
  if (i === 8) {
    break; // Exit the loop when i is 8
  }
  console.log(i); // Output: 1 2 3 4 6 7
}
```

In summary, loops in JavaScript provide a powerful mechanism to execute code repeatedly based on certain conditions, enabling you to efficiently work with collections of data and perform iterative tasks. The choice between `for`, `while`, or `do-while` loops depends on the specific requirements of the task at hand.

---

### Knowledge Check

**Q1.** What is an array?

**A1.** Arrays in JavaScript are fundamental data structures used to store multiple values in a single variable. They are a type of object that allows you to store and manipulate a collection of elements, which can be of any data type, such as numbers, strings, objects, or even other arrays. Arrays are commonly used for organizing and working with lists of related data. Arrays are objects and they have their own spesific properties and methods.

**Q2.** What are arrays useful for?

**A2.** Arrays are useful to store multiple values in a single variable in the memory. The fact that they can store a collection of elements which can be of any data type such as numbers,strings, objects or even other arrays and manipulate these items with its built in methods, is a powerful feature of the JavaScript language.

**Q3.** How do you access an array element?

**A3.** Array elements are indexed, so we can access the individual elements using their index numbers. Array elements are indexed starting from number 0.

**Q4.** How do you change an array element?

**A4.** After we access an array element using it's index number, we can assign a new value to that element using the `=` operator.

```js
let myArr = [6, 7, 8, 9];

myArr[0] = 5;
console.log(myArr); // [5, 7, 8, 9]
```

**Q5.** What are some useful array properties?

**A5.** 
+ `array.length` : Sets or returns the number of elements in an array.
+ `array.prototype` : Allows you to add properties and methods to an Array object.

**Q6.** What are some useful array methods?

**A6.** 
+ `array.map()` :	Creates a new array with the result of calling a function for each array element.
+ `array.reverse()` :	Reverses the order of the elements in an array.
+ `array.sort()` :	Sorts the elements of an array.
+ `array.splice()` :	Adds/Removes elements from an array.

**Q7.** What are loops useful for?

**A7.** Loops are useful for performing a task multiple times, over and over again. Loops are used to efficiently perform repetitive tasks, iterate over collections of data, and process elements one by one.

**Q8.** What is the break statement?

**A8.** `break` statement is used to break out of a loop immediately. Whenever a break statement is used, the loop will stop executing and transfer the control of the program to the code that comes after the loop.

**Q9.** What is the continue statement?

**A9.** `continue` statement is used to cease the current iteration of the loop. Whenever a continue statement is used, the loop will jump to the next iteration of the loop and continue from there.

**Q10.** What is the advantage of writing automated tests?

**A10.** Primary advantages of writing automated tests are:

+ **Bug Detection and Prevention**: Automated tests help identify bugs and issues in the code early in the development process. They can catch errors that might not be apparent during manual testing, preventing those bugs from reaching production and impacting users.

+ **Regression Testing**: As projects evolve and new features are added, there's a risk of introducing regressions—previously functional code breaking due to new changes. Automated tests help catch such regressions, ensuring that old functionalities still work as expected even after significant changes.