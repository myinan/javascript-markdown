# Fundamentals Part 1

## Introduction to JavaScript
JavaScript, often abbreviated as JS, is a programming language that is one of the core technologies of the World Wide Web, alongside HTML and CSS. As of 2022, 98% of websites use JavaScript on the client-side for webpage behaviour, often incorporating third-party libraries. All major web browsers have a dedicated JavaScript engine to execute the code on users' devices.

JavaScript is a high-level programming language that is primarily used for creating interactive web pages and applications. It is one of the core technologies of the World Wide Web and is supported by all major web browsers. JavaScript can also be used on the server-side with the help of frameworks like Node.js.

Key features and concepts of JavaScript:

1. _**Syntax:**_ JavaScript has a C-style syntax, which means it uses semicolons to seperate statements and curly braces to define block of code.

2. _**Variables:**_ JavaScript uses the 'var', 'let', or 'const' keywords to declare variables. 'var' and 'let' allow reassignment, while 'const' creates a read-only constant.

3. _**Control Flow (Conditionals and Loops):**_ JavaScript provides control flow statements such as "if-else" statements, "switch" statements, "for" loops and "while" loops to control the execution flow based on conditions or iterate over data.

4. _**Data Types:**_ JavaScript has 8 built-in data types. These are: string, number, bigint, boolean, undefined, null, symbol and object. The "object" data type can also contain an array, a date or another object.

5. _**Functions:**_ Functions in JavaScript are blocks of reusable code that can be invoked using a function name followed by parentheses. They can acceot parameters and return values.

6. _**Objects:**_ JavaScript is an object-oriented language and objects are key to it's structure. Objects are collections of key-value pairs, where values can be any data type, including other objects.

7. _**Event-driven programming:**_ JavaScript allows you to respond to events triggered by user interactions or other sources. Event handlers can be attached to HTML elements to perform actions when events occur, such as button click or mouse movement.

8. _**DOM Manipulation:**_ The Document Object Model (DOM) is a programming interface that represent the structure of an HTML document. JavaScript can be used to manipulate the DOM, adding, modifying or deleting elements dynamically.

9. _**Asynchronous Programming:**_ JavaScript supports asynchronous programming using callbacks, promises, and async/await syntax. This allows non-blocking execution, making it possible to handle time-consuming operations without blocking the execution of other code.

10. _**Libraries and Frameworks:**_ JavaScript has a vast ecosystem of libraries and frameworks that extend its functionality and make development easier. Some popular libraries and frameworks include React, Angular, Vue.js, and jQuery.

11. _**Integration with HTML and CSS:**_ JavaScript can be embedded directly into HTML documents using the `<script>` tag or included as an external file. It can interact with HTML elements and modify their styles using CSS.

JavaScript is a versatile language that can be used for various purposes beyond web development. It has expanded its reach into areas like server-side development, mobile app development, game development, and even desktop applications with the help of frameworks and platforms like Electron.

### Implementation of JavaScript code inside HTML code
There are three ways to include JavaScript code in an HTML document.

+ **Inline JavaScript:** You can include JavaScript code directly within the HTML file by using the `<script>`tag. The `<script>` tag can be placed anywhere within the `<head>`or `<body>`section of the HTML document.

+ **External JavaScript File:** You can also link an external JavaScript file to your HTML document using the `<script>`tag's `**src**`attribute. The external JavaScript file should a '.js' extension and contain your JavaScript code.

+ **Asynchronous Loading:** To improve page loading performance, you can load JavaScript code asynchronously using the `**async**`attribute in the `<script>`tag. This allows the HTML page to continue loading without waiting for the JavaScript file to be fully loaded and executed.


## Variables
A variable is a “named storage” for data.

To create a variable in JavaScript, use the let keyword.

The statement below creates (in other words: declares) a variable with the name “message”:

```javascript
let message;
```

Now, we can put some data into it by using the assignment operator =:

```javascript
let message;

message = 'Hello'; // store the string 'Hello' in the variable named message
```

The string is now saved into the memory area associated with the variable. We can access it using the variable name:

```javascript
let message;
message = 'Hello!';

alert(message); // shows the variable content
```

To be concise, we can combine the variable declaration and assignment into a single line:

```javascript
let message = 'Hello!'; // define the variable and assign the value

alert(message); // Hello!
```

We can also declare multiple variables in one line:

```javascript
let user = 'John', age = 25, message = 'Hello';
```

That might seem shorter, but we don’t recommend it. For the sake of better readability, please use a single line per variable.

The multiline variant is a bit longer, but easier to read:

```javascript
let user = 'John';
let age = 25;
let message = 'Hello';
```
Some people also define multiple variables in this multiline style:

```javascript
let user = 'John',
  age = 25,
  message = 'Hello';
```

…Or even in the “comma-first” style:

```javascript
let user = 'John'
  , age = 25
  , message = 'Hello';
```

Technically, all these variants do the same thing. So, it’s a matter of personal taste and aesthetics.

### Variable naming
There are two limitations on variable names in JavaScript:

The name must contain only letters, digits, or the symbols $ and _.
The first character must not be a digit.
Examples of valid names:

```javascript
let userName;
let test123;
```

When the name contains multiple words, camelCase is commonly used. That is: words go one after another, each word except first starting with a capital letter: myVeryLongName.

What’s interesting – the dollar sign '$' and the underscore '_' can also be used in names. They are regular symbols, just like letters, without any special meaning.

These names are valid:

```javascript
let $ = 1; // declared a variable with the name "$"
let _ = 2; // and now a variable with the name "_"

alert($ + _); // 3
```

Examples of incorrect variable names:

```javascript
let 1a; // cannot start with a digit

let my-name; // hyphens '-' aren't allowed in the name
```

### Constants
To declare a constant (unchanging) variable, use const instead of let:

```javascript
const myBirthday = '18.04.1982';
```

Variables declared using const are called “constants”. They cannot be reassigned. An attempt to do so would cause an error:

```javascript
const myBirthday = '18.04.1982';

myBirthday = '01.01.2001'; // error, can't reassign the constant!
```

When a programmer is sure that a variable will never change, they can declare it with const to guarantee and clearly communicate that fact to everyone.

#### Uppercase constants
There is a widespread practice to use constants as aliases for difficult-to-remember values that are known prior to execution.

Such constants are named using capital letters and underscores.

For instance, let’s make constants for colors in so-called “web” (hexadecimal) format:

```javascript
const COLOR_RED = "#F00";
const COLOR_GREEN = "#0F0";
const COLOR_BLUE = "#00F";
const COLOR_ORANGE = "#FF7F00";

// ...when we need to pick a color
let color = COLOR_ORANGE;
alert(color); // #FF7F00
```

Benefits:

COLOR_ORANGE is much easier to remember than "#FF7F00".
It is much easier to mistype "#FF7F00" than COLOR_ORANGE.
When reading the code, COLOR_ORANGE is much more meaningful than #FF7F00.
When should we use capitals for a constant and when should we name it normally? Let’s make that clear.

Being a “constant” just means that a variable’s value never changes. But there are constants that are known prior to execution (like a hexadecimal value for red) and there are constants that are calculated in run-time, during the execution, but do not change after their initial assignment.

For instance:

```javascript
const pageLoadTime = /* time taken by a webpage to load */;
```

The value of pageLoadTime is not known prior to the page load, so it’s named normally. But it’s still a constant because it doesn’t change after assignment.

In other words, capital-named constants are only used as aliases for “hard-coded” values.

### Name variables the right way
Some good-to-follow rules are:

+ Use human-readable names like userName or shoppingCart.
+ Stay away from abbreviations or short names like a, b, c, unless you really know what you’re doing.
+ Make names maximally descriptive and concise. Examples of bad names are data and value. Such names say nothing. It’s only okay to use them if the context of the code makes it exceptionally obvious which data or value the variable is referencing.
+ Agree on terms within your team and in your own mind. If a site visitor is called a “user” then we should name related variables currentUser or newUser instead of currentVisitor or newManInTown.

## JavaScript is a dynamically typed language
In JavaScript, a variable is a named container that stores a value. It is essentially a symbolic name for a value that can be used to refer to and manipulate that value throughout your program. Variables allow you to store and manipulate data, making them a fundamental concept in programming.

Unlike some other programming languages, JavaScript is a dynamically typed language, which means you do not need to explicitly declare the data type of a variable when you create it. Instead, the data type of a variable is determined automatically based on the value assigned to it. This is often referred to as "type inference."

For example, consider the following JavaScript code:

```javascript
let age = 25;
```

In this code, `age` is a variable that is assigned the value `25`. JavaScript will automatically determine that the data type of `age` is a number based on the value assigned to it.

The advantage of dynamic typing is that it allows for more flexibility and ease of use. You can assign values of different types to the same variable without explicitly specifying the data type. For instance, you can later assign a string value to the `age` variable:

```javascript
age = "twenty-five";
```

Now, the data type of `age` is a string. This flexibility makes JavaScript versatile and suitable for a wide range of tasks.

It's important to note that variables in JavaScript are not bound to a specific data type. They can change their data type during the execution of a program. This dynamic behavior allows you to perform operations and transformations on variables without worrying about explicitly converting their types.

In summary, variables in JavaScript are named containers that store values. JavaScript is a dynamically typed language, which means you don't need to specify the data type of a variable explicitly. The data type of a variable is determined automatically based on the value assigned to it. This dynamic typing provides flexibility and simplifies programming tasks.

## Data Types and Values
JavaScript has several built-in data types that you can use to store different kinds of values. The main data types in JavaScript are as follows:

1. **Number**: Represents numeric values, both integers and floating-point numbers. For example, `5`, `3.14`, and `-10`.

2. **String**: Represents sequences of characters enclosed in single quotes (`'`) or double quotes (`"`). For example, `'Hello'` and `"JavaScript"`.

3. **Boolean**: Represents a logical value that can be either `true` or `false`. It is commonly used for conditional statements and comparisons.

4. **Undefined**: Represents a variable that has been declared but has not been assigned a value. If you try to access the value of an uninitialized variable, it will have the value `undefined`.

5. **Null**: Represents the intentional absence of any object value. It is often used to indicate that a variable does not have a meaningful value.

6. **Object**: Represents a collection of key-value pairs, where values can be of any data type. Objects are a fundamental concept in JavaScript and can be used to create complex data structures.

7. **Symbol**: Represents unique and immutable values that can be used as property keys of objects. Symbols are primarily used to avoid naming conflicts in object properties.

8. **BigInt**: Represents arbitrary precision integers. It can be used to store and operate on numbers larger than the maximum representable by the `Number` data type.

These data types allow you to store and manipulate different kinds of values in JavaScript.

Now, let's discuss the difference between a data type and a value. 

A **data type** is a classification or category of data that determines the operations that can be performed on it and the values it can hold. It defines the set of values that a variable of that type can represent and the operations that can be performed on those values. Examples of data types include numbers, strings, booleans, etc.

On the other hand, a **value** is an actual piece of data assigned to a variable. It is an instance or representation of a specific data type. For instance, the number `42`, the string `"Hello"`, and the boolean value `true` are all values that belong to their respective data types.

In summary, data types in JavaScript categorize values and determine the operations that can be performed on them. Values, on the other hand, are the actual data assigned to variables and represent instances of specific data types.

## Operators in JavaScript
In JavaScript, operators are symbols or keywords that perform operations on one or more operands (values) and produce a result. They allow you to perform various calculations, comparisons, and manipulations on data. JavaScript provides a wide range of operators to handle different types of operations. Here are the most commonly used operator types in JavaScript:

1. **Arithmetic Operators**: These operators perform mathematical calculations on numeric operands. Common arithmetic operators include:
   - `+`: Addition operator, which adds two values together.
   - `-`: Subtraction operator, which subtracts the second value from the first.
   - `*`: Multiplication operator, which multiplies two values.
   - `/`: Division operator, which divides the first value by the second.
   - `%`: Modulus operator, which returns the remainder of the division between two values.

2. **Assignment Operators**: These operators assign a value to a variable. The most basic assignment operator is `=`, which assigns the value on the right to the variable on the left. For example, `x = 5` assigns the value `5` to the variable `x`. There are also compound assignment operators that combine an arithmetic operation with assignment, such as `+=`, `-=`, `*=`, and `/=`.

3. **Comparison Operators**: These operators compare two values and return a boolean result (`true` or `false`). Common comparison operators include:
   - `==`: Equal to operator, which checks if two values are equal, performing type coercion if necessary.
   - `===`: Strict equal to operator, which checks if two values are equal without performing type coercion.
   - `!=`: Not equal to operator, which checks if two values are not equal, performing type coercion if necessary.
   - `!==`: Strict not equal to operator, which checks if two values are not equal without performing type coercion.
   - `>`: Greater than operator, which checks if the value on the left is greater than the value on the right.
   - `<`: Less than operator, which checks if the value on the left is less than the value on the right.
   - `>=`: Greater than or equal to operator, which checks if the value on the left is greater than or equal to the value on the right.
   - `<=`: Less than or equal to operator, which checks if the value on the left is less than or equal to the value on the right.

4. **Logical Operators**: These operators are used to combine or manipulate boolean values. Common logical operators include:
   - `&&`: Logical AND operator, which returns `true` if both operands are `true`.
   - `||`: Logical OR operator, which returns `true` if at least one of the operands is `true`.
   - `!`: Logical NOT operator, which negates the boolean value of an operand.

5. **Unary Operators**: These operators operate on a single operand. Some common unary operators are:
   - `++`: Increment operator, which increases the value of an operand by 1.
   - `--`: Decrement operator, which decreases the value of an operand by 1.
   - `!`: Unary NOT operator, which negates the boolean value of an operand.
   - `+`: Unary plus operator, which attempts to convert an operand to a number and returns the numeric value.
   - `-`: Unary negation operator, which negates the numeric value of an operand.

6. **Ternary Operator**: The ternary operator (`? :`) is a conditional operator that takes three operands. It evaluates a condition and returns one of two values based on the result of the condition. Its syntax is `condition ? expression1 : expression2`. If the condition is true, `expression1` is returned; otherwise, `expression2` is returned.

Its worth noting that the unary plus operator (`+`) is used to convert its operand into a number. If the operand is already a number, it remains unchanged. If the operand is a string that represents a valid numeric value, the unary plus operator converts it into a numeric value.

These are just a few examples of the many operators available in JavaScript. There are also bitwise operators, string operators, type operators, and more, each serving a specific purpose. Understanding and utilizing operators effectively is crucial for performing computations, making decisions, and manipulating data in JavaScript.

## Operator precedence
If an expression has more than one operator, the execution order is defined by their **precedence**, or, in other words, the default priority order of operators.

There are many operators in JavaScript. Every operator has a corresponding precedence number. The one with the larger number executes first. If the precedence is the same, the execution order is from left to right.

For example, unary "+" and "-" operators have a priority of 14 while addition(+) and subtraction(-) operators have a priority of 11, so unary "+" and "-" operators are executed before addition(+) and subtraction(-) operators.

### The Assignment Operator
Let’s note that an assignment = is also an operator. It is listed in the precedence table with the very low priority of 2.

That’s why, when we assign a variable, like x = 2 * 2 + 1, the calculations are done first and then the = is evaluated, storing the result in x.
The "operator precedence" is the reason why this also works:

```javascript
let n = 2;
n = n + 5;     // n = 7
n = n * 2;     // n = 14
```

## JavaScript Data Type: Number
JavaScript Numbers are Always 64-bit Floating Point

Unlike many other programming languages, JavaScript does not define different types of numbers, like integers, short, long, floating-point etc.

JavaScript numbers are always stored as double precision floating point numbers, following the international IEEE 754 standard.

This format stores numbers in 64 bits, where the number (the fraction) is stored in bits 0 to 51, the exponent in bits 52 to 62, and the sign in bit 63.

#### Important!
JavaScript uses the + operator for both addition and concatenation.

Numbers are added. Strings are concatenated.

+ If you add two numbers, the result will be a number.
+ If you add two strings, the result will be a string concatenation.
+ If you add a number and a string, the result will be a string concatenation.
+ If you add a string and a number, the result will be a string concatenation.

### Numeric Strings
JavaScript strings can have numeric content:

```javascript
let x = 100;         // x is a number

let y = "100";       // y is a string
```

JavaScript will try to convert strings to numbers in all numeric operations:

This will work:

```javascript
let x = "100";
let y = "10";
let z = x / y;      // 10
let t = x * y;      // 1000
let k = x - y;      // 90
```

But this will not work:

```javascript
let x = "100";
let y = "10";
let z = x + y;      // "10010"
```

**In the last example JavaScript uses the + operator to concatenate the strings.**

### NaN - Not a Number
NaN is a JavaScript reserved word indicating that a number is not a legal number.

Trying to do arithmetic with a non-numeric string will result in NaN (Not a Number):

```javascript
let x = 100 / "Apple";      // NaN
```

However, if the string is numeric, the result will be a number:

```javascript
let x = 100 / "10";        // 10
```

### Creating Number objects
In JavaScript, numbers are considered primitive values. A primitive value is a data type that is not an object and has no methods or properties associated with it. When you define a number using a numeric literal, such as `5` or `3.14`, JavaScript creates a primitive value to represent that number.

For example:
```javascript
let age = 25; // age is a variable assigned the primitive value 25
```

In this case, `age` is a variable that holds a primitive number value of `25`.

However, JavaScript also provides a way to create numbers as objects using the `new` keyword. The `new` keyword is used to create instances of objects from a constructor function, which is a special function used to create and initialize objects.

When you create a number object using the `new` keyword, JavaScript treats the number as an object with additional methods and properties associated with it. This allows you to perform operations and access functionalities specific to number objects.

Here's an example of creating a number object using the `new` keyword:
```javascript
let num = new Number(42); // num is an object representing the number 42
```

In this case, `num` is a variable assigned to a number object created using the `Number` constructor. The `Number` constructor is a built-in function in JavaScript that creates a number object based on the provided argument (`42` in this case).

Number objects have certain methods and properties that can be accessed using dot notation, such as `num.toFixed(2)` to round the number to 2 decimal places or `num.toString()` to convert the number to a string representation.

**However, it's important to note that using number objects with the `new` keyword is generally not recommended in JavaScript unless you specifically require the additional functionalities provided by number objects. For most cases, using the primitive number values is more efficient and simpler.**

## Increment/Decrement Operators
The "++" and "--" operators in JavaScript are known as increment and decrement operators, respectively. They are used to increase or decrease the value of a numeric variable by 1.

The increment operator "++" adds 1 to the variable's value, while the decrement operator "--" subtracts 1. These operators can be applied to both integer and floating-point numbers.

The position of the "++" or "--" operator in relation to the operand affects when the increment or decrement operation is applied. There are two possibilities: prefix and postfix.

1. **Prefix Increment/Decrement**: When the "++" or "--" operator is placed before the variable (e.g., "++x" or "--x"), it is called the prefix increment or decrement operator. In this case, the increment or decrement operation is performed before the variable is evaluated or used in any expression.

For example:
```javascript
let x = 5;
let y = ++x;

console.log(x); // Output: 6
console.log(y); // Output: 6
```

In this code, the prefix increment operator is used to increase the value of `x` by 1 before assigning it to `y`. So, both `x` and `y` have the value of 6.

2. **Postfix Increment/Decrement**: When the "++" or "--" operator is placed after the variable (e.g., "x++" or "x--"), it is called the postfix increment or decrement operator. In this case, the increment or decrement operation is performed after the variable is evaluated or used in an expression.

For example:
```javascript
let x = 5;
let y = x++;

console.log(x); // Output: 6
console.log(y); // Output: 5
```

In this code, the postfix increment operator is used. The value of `x` is assigned to `y` first, and then `x` is incremented by 1. Therefore, `y` holds the original value of `x` (5), while `x` is incremented to 6.

In general, it is recommended to use the prefix form (`++x`, `--x`) when the intention is to increment or decrement the variable before its value is used. The postfix form (`x++`, `x--`) is useful when you want to use the current value of the variable and then increment or decrement it.

## Block-level Variables and Global Variables
1. Block-level variables:
   Block-level variables are declared within a block of code, which is typically defined by a pair of curly braces `{}`. In JavaScript, variables declared with the `let` and `const` keywords have block-level scope. This means that they are only accessible within the block in which they are declared, as well as any nested blocks within that block.

   For example:
   ```javascript
   function myFunction() {
     if (true) {
       let blockVar = 10; // block-level variable
       const blockConst = 20; // block-level variable
       console.log(blockVar); // 10
       console.log(blockConst); // 20
     }

     console.log(blockVar); // ReferenceError: blockVar is not defined
     console.log(blockConst); // ReferenceError: blockConst is not defined
   }

   myFunction();
   ```

   In the above example, `blockVar` and `blockConst` are block-level variables because they are declared with `let` and `const` inside the `if` block. They are accessible within that block, but if you try to access them outside of the block, you'll get a `ReferenceError` because they are out of scope.

2. Global variables:
   Global variables, as the name suggests, are declared outside of any function or block. They have global scope, meaning they can be accessed from anywhere within the JavaScript program, including all functions and blocks.

   For example:
   ```javascript
   var globalVar = 10; // global variable

   function myFunction() {
     console.log(globalVar); // 10
   }

   myFunction();
   console.log(globalVar); // 10
   ```

   In this example, `globalVar` is a global variable because it is declared outside of any function or block. It can be accessed from within the `myFunction` function as well as outside of it.

Global variables can be accessed and modified from multiple functions and blocks, which can make them convenient but also potentially risky. It's generally recommended to use global variables sparingly to avoid naming conflicts and maintain better control over variable scope and data encapsulation.

## var vs let/const
There are two main differences of var compared to let/const:

1. var variables have no block scope, their visibility is scoped to current function, or global, if declared outside function.
2. var declarations are processed at function start (script start for globals).

These differences make var worse than let most of the time. Block-level variables is such a great thing. That’s why let was introduced in the standard long ago, and is now a major way (along with const) to declare a variable.

---

### Knowledge Check

**Q1.** Name the three ways to declare a variable

**A1.** We can declare a variable with either "let", "const" or "var".

**Q2.** Which of the three variable declarations should you avoid and why?

**A2.** Declaring variables with "var" should be avoided because variables that are declared with "var" has no block scope, meaning they will be accessible outside of the block they were declared. Also var declarations are processed at function start, meaning they will have an undeclared value before their initilization.

**Q3.** What rules should you follow when naming variables?

**A3.** Variable names should be concise and provide meaning to what they do, while not being too long. Also variables names like "a", "b", "c" should be avoided because they provide no meaning to the variable. Variable naming convention is as "variableName".

**Q4.** What happens when you add numbers and strings together?

**A4.** "+" operator is used for both addition of numbers and concatenation of strings. If we use the "+" operator with a number and a string, JavaScript will see the number as a string and concatanate the values of those variables. For example : 

```javascript
let number = 10;
let string = "10";
let final = number + string;
alert(final);     /// "1010"
```

**Q5.** How does the Modulo (%), or Remainder, operator work?

**A5.** Modulo operator returns the remainder of a division. For example: "10 % 5" will return 0 because 10 divided by 5 gives us a remainder of 0.

**Q6.** Explain the difference between == and ===.

**A6.** Both `==` and `===`are comparison operators. These operators compare two values and return a boolean result (`true` or `false`). 

- `==`: Equal to operator, checks if two values are equal, performs type coercion if necessary.
- `===`: Strict equal to operator, checks if two values are equal without performing type coercion.

**Q7.** When would you receive a NaN result?

**A7.** If we tried to perform an arithmetic operation on a non-numeric string, we would get a "NaN result, NaN meaning "Not a Number" in this case.

**Q8.** How do you increment and decrement a number?

**A8.** Incrementation operator is `++` while decrementation operator is `--`.

**Q9.** Explain the difference between prefixing and postfixing increment/decrement operators.

**A9.** The "++" and "--" operators in JavaScript are known as increment and decrement operators, respectively. They are used to increase or decrease the value of a numeric variable by 1.

The increment operator "++" adds 1 to the variable's value, while the decrement operator "--" subtracts 1. These operators can be applied to both integer and floating-point numbers.

The position of the "++" or "--" operator in relation to the operand affects when the increment or decrement operation is applied. There are two possibilities: prefix and postfix.

1. **Prefix Increment/Decrement**: When the "++" or "--" operator is placed before the variable (e.g., "++x" or "--x"), it is called the prefix increment or decrement operator. In this case, the increment or decrement operation is performed before the variable is evaluated or used in any expression.

For example:
```javascript
let x = 5;
let y = ++x;

console.log(x); // Output: 6
console.log(y); // Output: 6
```

In this code, the prefix increment operator is used to increase the value of `x` by 1 before assigning it to `y`. So, both `x` and `y` have the value of 6.

2. **Postfix Increment/Decrement**: When the "++" or "--" operator is placed after the variable (e.g., "x++" or "x--"), it is called the postfix increment or decrement operator. In this case, the increment or decrement operation is performed after the variable is evaluated or used in an expression.

For example:
```javascript
let x = 5;
let y = x++;

console.log(x); // Output: 6
console.log(y); // Output: 5
```

In this code, the postfix increment operator is used. The value of `x` is assigned to `y` first, and then `x` is incremented by 1. Therefore, `y` holds the original value of `x` (5), while `x` is incremented to 6.

In general, it is recommended to use the prefix form (`++x`, `--x`) when the intention is to increment or decrement the variable before its value is used. The postfix form (`x++`, `x--`) is useful when you want to use the current value of the variable and then increment or decrement it.

**Q10.** What is operator precedence and how is it handled in JS?

**A10.** "Operator precedence" is the or the of which operation will be executed before any other. Every operator in javascript has a precedence value, so the order of which operator will be executed is determined by comparing these values. If the precedence values of the operators are equal to each other, then the code is executed from left to right.

**Q11.** How do you access developer tools and the console?

**A11.** In the browser, we can access developer tools by right clicking on the web page and selecting "inspect" from the menu. In the developer tools, there is the console bar which can be used to inspect the terminal and execute code directly in the browser.

**Q12.** How do you log information to the console?

**A12.** The `console.log()`method can be used to log information to the console.

**Q13.** What does unary plus operator do to string representations of integers? eg. +”10”

**A13.** Unary plus operator converts a numeric string to a number. For example:

```javascript
let string = "10";
let final = +string + 5;
alert(final);      // 15
```

