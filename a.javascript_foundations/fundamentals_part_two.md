# Fundamentals Part 2
There are 8 basic data types in JavaScript.

+ Seven primitive data types:
    + **number** for numbers of any kind: integer or floating-point, integers are limited by ±(253-1).
    + **bigint** for integer numbers of arbitrary length.
    + **string** for strings. A string may have zero or more characters, there’s no separate single-character type.
    + **boolean** for true/false.
    + **null** for unknown values – a standalone type that has a single value null.
    + **undefined** for unassigned values – a standalone type that has a single value undefined.
    + **symbol** for unique identifiers.
+ And one non-primitive data type:
    + **object** for more complex data structures.

The **typeof** operator allows us to see which type is stored in a variable.
+ Usually used as typeof x, but typeof(x) is also possible.
+ Returns a string with the name of the type, like "string".
+ "typeof null" returns "object" – this is an error in the language, it’s not actually an object.

## JavaScript Data Type: String
In JavaScript, a string is a data type used to represent a sequence of characters. It is one of the fundamental data types in the language and is commonly used to store and manipulate textual data. Strings are enclosed in either single quotes (''), double quotes ("") or backticks (``). For example:

```javascript
let message = "Hello, World!";
let name = 'John Doe';
let template = `My name is ${name}.`;
```

In the above code snippet, we have declared three variables (`message`, `name`, and `template`) that store strings. The `message` variable is assigned the string "Hello, World!", the `name` variable stores the string 'John Doe', and the `template` variable is assigned a string using backticks and includes a variable interpolation using `${}`.

Strings in JavaScript are immutable, which means that once a string is created, its content cannot be changed. However, you can perform various operations on strings to create new strings or manipulate their content. Here are some common operations and methods used with strings in JavaScript:

1. Concatenation: You can concatenate (combine) strings using the `+` operator or the `concat()` method. For example:

```javascript
let firstName = 'John';
let lastName = 'Doe';
let fullName = firstName + ' ' + lastName;
console.log(fullName); // Output: John Doe

let str1 = 'Hello,';
let str2 = ' World!';
let result = str1.concat(str2);
console.log(result); // Output: Hello, World!
```

2. String length: You can obtain the length of a string using the `length` property. For example:

```javascript
let message = 'Hello';
console.log(message.length); // Output: 5
```

3. Accessing characters: You can access individual characters within a string using square brackets (`[]`) and the character's index. In JavaScript, strings are zero-indexed, meaning the first character is at index 0. For example:

```javascript
let message = 'Hello';
console.log(message[0]); // Output: H
console.log(message[1]); // Output: e
console.log(message[4]); // Output: o
```

4. String methods: JavaScript provides various built-in methods to manipulate strings. Some commonly used methods include `toUpperCase()`, `toLowerCase()`, `substring()`, `split()`, `replace()`, and `indexOf()`. Here's an example:

```javascript
let message = 'Hello, World!';
console.log(message.toUpperCase()); // Output: HELLO, WORLD!
console.log(message.toLowerCase()); // Output: hello, world!
console.log(message.substring(0, 5)); // Output: Hello
console.log(message.split(',')); // Output: ['Hello', ' World!']
console.log(message.replace('Hello', 'Hi')); // Output: Hi, World!
console.log(message.indexOf('World')); // Output: 7
```

These are just a few examples of the operations and methods you can use with strings in JavaScript. Strings are widely used in JavaScript for a variety of purposes, including manipulating and displaying text, working with user input, and interacting with APIs and databases.

**Note:** Normally, strings like "John Doe", cannot have methods or properties because they are not objects. But with JavaScript, methods and properties are also available to strings, because JavaScript treats strings as objects when executing methods and properties.

**Note:** All string methods return a new value. They don't modify the original string, since strings are immutable.

[Most commonly used JavaScript string methods](https://www.w3schools.com/jsref/jsref_obj_string.asp)

## Conditionals
Step one in learning about conditionals is making sure we have a good grasp on comparisons first.

### Comparison operators in JavaScript
In JavaScript, comparisons are used to evaluate the relationship between values and determine whether one value is greater than, less than, equal to, or not equal to another value.

1. **Comparison operators return a boolean value:**
   In JavaScript, comparison operators ( `>`, `<`, `>=`, `<=`, `==`, `!=`, `===`, and `!==` ) return a boolean value, which is either `true` or `false`, depending on the result of the comparison. For example, `5 > 3` returns `true` because 5 is greater than 3.

2. **Strings are compared letter-by-letter in the "dictionary" order:**
   When comparing strings using comparison operators, JavaScript compares them letter-by-letter based on their Unicode code points. The comparison is performed in lexicographical order, similar to a dictionary. For example, `"apple" > "banana"` returns `false` because "apple" comes before "banana" in lexicographical order.

3. **Values of different types are converted to numbers during comparison:**
   When comparing values of different types (e.g., a string and a number) using comparison operators other than strict equality (`===` and `!==`), JavaScript converts the values to numbers before making the comparison. For example, `"10" > 5` returns `true` because the string "10" is converted to the number 10 for the comparison.

   However, strict equality (`===`) and strict inequality (`!==`) operators do not perform type conversion. They compare both the values and types of the operands. For example, `"10" === 10` returns `false` because the string "10" is not strictly equal to the number 10.

4. **The values `null` and `undefined` are equal to each other and not equal to any other value:**
   In JavaScript, the values `null` and `undefined` are considered equal to each other when using the loose equality operator (`==`). For example, `null == undefined` returns `true`.

   However, when using strict equality (`===`), `null` and `undefined` are not considered equal. For example, `null === undefined` returns `false`.

5. **Be careful when comparing with variables that can be null/undefined:**
   When comparing variables that can occasionally be `null` or `undefined`, it is important to be cautious. Comparisons using operators like `>`, `<`, `>=`, and `<=` may produce unexpected results if the variable is `null` or `undefined`. In such cases, it is recommended to check for `null` or `undefined` separately before performing the comparison. This helps avoid errors or unintended behavior.

### Conditionals in JavaScript
Conditional statements are used to perform different actions based on different conditions.

Very often when you write code, you want to perform different actions for different decisions.

You can use conditional statements in your code to do this.

In JavaScript we have the following conditional statements:

+ Use `if` to specify a block of code to be executed, if a specified condition is true.
+ Use `else` to specify a block of code to be executed, if the same condition is false.
+ Use `else if` to specify a new condition to test, if the first condition is false.
+ Use `switch` to specify many alternative blocks of code to be executed.

Conditional statements in JavaScript allow you to control the flow of your code based on certain conditions. They enable your code to make decisions and execute different blocks of code depending on whether a condition is true or false. Conditional statements in JavaScript are:

1. **`if` statement:** 

The `if` statement is the most basic conditional statement. It executes a block of code only if the specified condition is true.

```javascript
const age = 25;

if (age >= 18) {
  console.log("You are an adult.");
} else {
  console.log("You are a minor.");
}
```

2. **`if...else` statement:**

The `if...else` statement allows you to execute one block of code if the condition is true and another block of code if the condition is false.

```javascript
const temperature = 28;

if (temperature > 30) {
  console.log("It's hot outside.");
} else {
  console.log("It's not too hot.");
}
```

3. **`if...else if...else` statement:**

You can use multiple conditions and blocks of code with the `if...else if...else` statement. It checks each condition one by one and executes the corresponding block of code for the first true condition.

```javascript
const score = 75;

if (score >= 90) {
  console.log("You got an A.");
} else if (score >= 80) {
  console.log("You got a B.");
} else if (score >= 70) {
  console.log("You got a C.");
} else {
  console.log("You need to improve.");
}
```

4. **`switch` statement:**

The `switch` statement is used when you have multiple cases and want to execute different blocks of code based on the value of a variable.

```javascript
const day = "Monday";

switch (day) {
  case "Monday":
    console.log("It's the start of the week.");
    break;
  case "Friday":
    console.log("It's almost the weekend.");
    break;
  default:
    console.log("It's an ordinary day.");
}
```

It's essential to remember that `break` statements are used within `switch` cases to prevent fall-through behavior, where execution continues to the next case without stopping.

These conditional statements allow you to build flexible and dynamic code that reacts to changing conditions, making your JavaScript programs more powerful and versatile.

#### Ternary operator (conditional operator):

The ternary operator, also known as the conditional operator, is a concise way of writing simple conditional expressions in JavaScript. It provides an alternative syntax to the traditional `if...else` statement for cases where you need to make a decision based on a single condition. The ternary operator takes the following form:

```javascript
condition ? expressionIfTrue : expressionIfFalse;
```

Here's a breakdown of each part:

1. `condition`: This is the expression that you want to evaluate. It can be any expression that returns a boolean value (i.e., true or false).

2. `expressionIfTrue`: This is the value or expression that gets returned if the condition evaluates to true.

3. `expressionIfFalse`: This is the value or expression that gets returned if the condition evaluates to false.

The ternary operator is particularly useful when you need to assign a value to a variable based on a condition. It allows you to write this logic in a single line, making the code more concise and readable.

Example 1: Assigning a value based on a condition

```javascript
const age = 20;
const isAdult = age >= 18 ? true : false;

console.log(isAdult); // Output: true
```

In this example, the `isAdult` variable will be assigned `true` if the `age` is greater than or equal to 18, and `false` otherwise.

Example 2: Returning a value from a function based on a condition

```javascript
function getDiscountPercentage(isPremiumMember) {
  return isPremiumMember ? 15 : 5;
}

const customer1 = { isPremiumMember: true };
const customer2 = { isPremiumMember: false };

console.log(getDiscountPercentage(customer1.isPremiumMember)); // Output: 15
console.log(getDiscountPercentage(customer2.isPremiumMember)); // Output: 5
```

In this example, the `getDiscountPercentage` function takes a boolean parameter `isPremiumMember`, and based on its value, it returns a different discount percentage.

It's important to use the ternary operator judiciously. While it can improve code readability for simple cases, using it excessively or nesting ternary operators can make the code harder to understand. In more complex scenarios, it's often better to use the traditional `if...else` statements for better clarity and maintainability.

## Logical operators in JavaScript
Although they are called “logical”, they can be applied to values of any type, not only boolean. Their result can also be of any type.

### OR (||)

Most of the time, `OR ||` is used in an `if` statement to test if any of the given conditions is true.

The "OR" operator is represented with two vertical line symbols:

```javascript
result = a || b;
```

In classical programming, the logical OR is meant to manipulate boolean values only. If any of its arguments are true, it returns true; otherwise, it returns false.

In JavaScript, the operator is a little bit trickier and more powerful. But first, let's see what happens with boolean values.

There are four possible logical combinations:

```javascript
alert(true || true);    // true
alert(false || true);   // true
alert(true || false);   // true
alert(false || false);  // false
```

As we can see, the result is always true except for the case when both operands are false.

If an operand is not a boolean, it's converted to a boolean for the evaluation.

**OR "||" finds the first truthy value**

The logic described above is somewhat classical. Now, let's bring in the "extra" features of JavaScript.

The extended algorithm works as follows:

Given multiple OR'ed values:

```javascript
result = value1 || value2 || value3;
```

The OR `||` operator does the following:

1. Evaluates operands from left to right.
2. For each operand, converts it to a boolean. If the result is true, stops and returns the original value of that operand.
3. If all operands have been evaluated (i.e., all were false), returns the last operand.

A value is returned in its original form, without the conversion.

**In other words, a chain of OR `||` returns the first truthy value or the last one if no truthy value is found.**

For instance:

```javascript
alert(1 || 0);           // 1 (1 is truthy)
alert(null || 1);        // 1 (1 is the first truthy value)
alert(null || 0 || 1);   // 1 (the first truthy value)
alert(undefined || null || 0);   // 0 (all falsy, returns the last value)
```

**Short-circuit evaluation:**

Another feature of the OR `||` operator is the so-called "short-circuit" evaluation.

It means that `||` processes its arguments until the first truthy value is reached, and then the value is returned immediately, without even touching the other argument.

The importance of this feature becomes obvious if an operand isn't just a value, but an expression with a side effect, such as a variable assignment or a function call.

In the example below, only the second message is printed:

```javascript
true || alert("not printed");
false || alert("printed");
```

In the first line, the OR `||` operator stops the evaluation immediately upon seeing `true`, so the alert isn't run.

Sometimes, people use this feature to execute commands only if the condition on the left part is falsy.


### AND (&&)

The AND operator is represented with two ampersands `&&`:

```
result = a && b;
```

In classical programming, AND returns true if both operands are truthy and false otherwise:

```javascript
alert( true && true );   // true
alert( false && true );  // false
alert( true && false );  // false
alert( false && false ); // false
```

An example with `if`:

```javascript
let hour = 12;
let minute = 30;

if (hour == 12 && minute == 30) {
  alert( 'The time is 12:30' );
}
```

Just as with OR, any value is allowed as an operand of AND:

```javascript
if (1 && 0) { // evaluated as true && false
  alert( "won't work, because the result is falsy" );
}
```

**AND `&&` finds the first falsy value:**

Given multiple AND'ed values:

```
result = value1 && value2 && value3;
```

The AND `&&` operator does the following:

1. Evaluates operands from left to right.
2. For each operand, converts it to a boolean. If the result is false, stops and returns the original value of that operand.
3. If all operands have been evaluated (i.e. all were truthy), returns the last operand.

In other words, AND returns the first falsy value or the last value if none were found.

The rules above are similar to OR. The difference is that AND returns the first falsy value while OR returns the first truthy one.

**Examples:**

```javascript
// if the first operand is truthy,
// AND returns the second operand:
alert( 1 && 0 ); // 0
alert( 1 && 5 ); // 5

// if the first operand is falsy,
// AND returns it. The second operand is ignored
alert( null && 5 ); // null
alert( 0 && "no matter what" ); // 0
```

#### Precedence of AND `&&` is higher than OR `||`

The precedence of AND `&&` operator is higher than OR `||`.

So the code `a && b || c && d` is essentially the same as if the `&&` expressions were in parentheses: `(a && b) || (c && d)`.

#### Don't replace `if` with `||` or `&&`

Sometimes, people use the AND `&&` operator as a "shorter way to write if".

For instance:

```javascript
let x = 1;

(x > 0) && alert( 'Greater than zero!' );
```

The action in the right part of `&&` would execute only if the evaluation reaches it. That is, only if `(x > 0)` is true.

So we basically have an analogue for:

```javascript
let x = 1;

if (x > 0) alert( 'Greater than zero!' );
```

Although the variant with `&&` appears shorter, using `if` is more obvious and tends to be a little bit more readable. So we recommend using each construct for its purpose: use `if` if we want a conditional statement and use `&&` if we want to perform logical AND operations.


### ! (NOT)

The boolean NOT operator is represented with an exclamation sign `!`.

The syntax is pretty simple:

```
result = !value;
```

The operator accepts a single argument and does the following:

1. Converts the operand to boolean type: true/false.
2. Returns the inverse value.

For instance:

```javascript
alert( !true ); // false
alert( !0 ); // true
```

A double NOT `!!` is sometimes used for converting a value to boolean type:

```javascript
alert( !!"non-empty string" ); // true
alert( !!null ); // false
```

That is, the first NOT converts the value to boolean and returns the inverse, and the second NOT inverses it again. In the end, we have a plain value-to-boolean conversion.

There's a little more verbose way to do the same thing - a built-in `Boolean` function:

```javascript
alert( Boolean("non-empty string") ); // true
alert( Boolean(null) ); // false
```

The precedence of NOT `!` is the highest of all logical operators, so it always executes first, before `&&` or `||`.

---
### Truthy and Falsy Values in Javascript

In JavaScript, values that are considered truthy are any values that evaluate to `true` when used in a boolean context.

Here's a list of some common truthy values in JavaScript:

- All non-empty strings (e.g., "hello", "false", "0", "-1")
- All numbers except 0 (e.g., -1, 1, 0.5)
- All objects (including arrays and functions)
- The special value `true`

Conversely, values that are considered falsy are any values that evaluate to `false` when used in a boolean context. Some common falsy values in JavaScript include:

- The empty string `""`
- The number 0 (zero)
- `null`
- `undefined`
- `NaN`
- The special value `false`

When using a value in a boolean context, like in an if statement, JavaScript implicitly converts the value to a boolean using the truthy and falsy rules. For example:

```javascript
if ("-1") {
  // This block will be executed because "-1" is truthy
}

if (0) {
  // This block will NOT be executed because 0 is falsy
}
```

---

### Knowledge Check

**Q1.** What are the eight data types in JavaScript?

**A1.** Data types in javascript are: 1- Number, 2- String, 3- Boolean, 4- Undefined, 5- Null, 6- Symbol, 7-Object, 8- Bigint.

**Q2.** Which data type is NOT primitive?

**A2.** Object datatype in JavaScript is not primitive.

**Q3.** What is the relationship between null and undefined?

**A3.** `null` represents an "empty" value, while `undefined` is the default value of a variable which is declared but not yet assigned a value. Both null and undefined are falsy values in the boolean context. Also, loose comparison of null and undefined (null == undefined) returns true while a strict comparison (null === undefined) returns false.

**Q4.** What is the difference between single, double, and backtick quotes for strings?

**A4.** In JavaScript, strings can be enclosed in three different types of quotes: single quotes (' '), double quotes (" "), and backtick quotes (``). Each type of quote serves a specific purpose and has some unique features. Here's an explanation of the differences between them:

1. **Single quotes (' '):**
Single quotes are the most common way to define a string in JavaScript. They are used to represent a sequence of characters. For example:

```javascript
let singleQuotedString = 'This is a single-quoted string.';
```

- You can include double quotes within a single-quoted string without any issues:
```javascript
let stringWithinSingleQuotes = 'He said, "Hello!"';
```

- If you want to include an apostrophe within a single-quoted string, you can do so without escaping:
```javascript
let apostropheString = 'I\'m going to the park.';
```

2. **Double quotes (" "):**
Double quotes are also used to define strings in JavaScript, and they are functionally equivalent to single quotes. For example:

```javascript
let doubleQuotedString = "This is a double-quoted string.";
```

- You can include single quotes within a double-quoted string without any problems:
```javascript
let stringWithinDoubleQuotes = "She said, 'Hi!'";
```

- Similarly, if you want to include a double quote within a double-quoted string, you can do so without escaping:
```javascript
let quoteString = "He said, \"Hello!\"";
```

3. **Backtick quotes (``):**
Backtick quotes, also known as template literals, were introduced in ECMAScript 6 (ES6). They provide more functionality compared to single and double quotes:

```javascript
let backtickString = `This is a backtick-quoted string.`;
```

- One of the key features of backtick quotes is that they allow for multiline strings without the need for concatenation or escape characters:
```javascript
let multilineString = `
  This is a
  multiline
  string.
`;
```

- Backticks also support string interpolation, which means you can embed expressions directly into the string using `${}`:
```javascript
let name = "John";
let interpolatedString = `Hello, ${name}!`;
```

- Additionally, you can include single and double quotes within a backtick-quoted string without escaping:
```javascript
let stringWithinBackticks = `He said, "Hi!" and I said, 'Hello!'`;
```

The choice of which type of quote to use largely depends on your preference and specific use case. Single and double quotes are more traditional and work in all JavaScript versions, while backticks provide more powerful features, such as multiline strings and string interpolation, but are only available in modern JavaScript environments that support ECMAScript 6 (ES6) and later. 

**Q5.** What is the term for joining strings together?

**A5.** The term used for joining strings together is "concatenation". "+" is used to concatenate strings.

**Q6.** Which type of quote lets you embed variables/expressions in a string?

**A6.** Backtick quotes (` `` `) are used to embed expressions into strings with the use of `${}`.

**Q7.** How do you embed variables/expressions in a string?

**A7.** To embed an expression into a string, we need to interpolate the expression we want to embed into the string between `${}` while also using backtick quotes for the string.

**Q8.** How do you use escape characters in a string?

**A8.** In JavaScript, escape characters are used to include special characters in a string that might otherwise be difficult to include directly. These characters are preceded by a backslash (`\`) to indicate that they have a special meaning.

Here are some commonly used escape characters in JavaScript:

1. `\'` - Single Quote
2. `\"` - Double Quote
3. `\\` - Backslash
4. `\n` - Newline
5. `\r` - Carriage Return
6. `\t` - Tab
7. `\b` - Backspace
8. `\f` - Form Feed

Here's an example of how to use escape characters in JavaScript:

```javascript
// Using single quotes within a single-quoted string
let singleQuotedString = 'This is a single-quoted string with a \'single quote\' in it.';
console.log(singleQuotedString);

// Using double quotes within a double-quoted string
let doubleQuotedString = "This is a double-quoted string with a \"double quote\" in it.";
console.log(doubleQuotedString);

// Using backslash to escape a special character
let escapedString = "This string has a backslash \\ in it.";
console.log(escapedString);

// Newline and tab characters
let multiLineString = "This is a multi-line\nstring with a\ttab.";
console.log(multiLineString);
```

When you run the above code, you will get the following output:

```
This is a single-quoted string with a 'single quote' in it.
This is a double-quoted string with a "double quote" in it.
This string has a backslash \ in it.
This is a multi-line
string with a   tab.
```

Using escape characters is particularly useful when you want to include special characters or formatting in your strings.

**Q9.** What is the difference between the slice/substring/substr string methods?

**A9.** In JavaScript, the slice, substring, and substr are string methods used to extract substrings from a given string. They have some differences in terms of how they work and handle certain scenarios:

1. **`slice(startIndex, endIndex)`**

   - The `slice()` method extracts a portion of the string and returns it as a new string.
   - It takes two arguments: `startIndex` (required) and `endIndex` (optional).
   - The `startIndex` is the starting index of the substring to be extracted. If negative, it represents the index from the end of the string (-1 being the last character).
   - The `endIndex` is the ending index (exclusive) of the substring. If not provided, the method extracts up to the end of the string.
   - It does not modify the original string.

   Example:
   ```js
   const str = "Hello, world!";
   const sliced = str.slice(0, 5); // "Hello"
   const sliced2 = str.slice(7);   // "world!"
   ```

2. **`substring(startIndex, endIndex)`**

   - The `substring()` method is similar to `slice()` but with different behavior regarding negative indices.
   - It takes two arguments: `startIndex` (required) and `endIndex` (optional).
   - If `startIndex` is greater than `endIndex`, the method swaps the two arguments before extracting the substring.
   - If negative indices are used, it treats them as 0.
   - Like `slice()`, it returns a new string without modifying the original.

   Example:
   ```js
   const str = "Hello, world!";
   const sub = str.substring(0, 5); // "Hello"
   const sub2 = str.substring(7);   // "world!"
   const sub3 = str.substring(5, 0); // "Hello" (startIndex > endIndex is swapped)
   ```

3. **`substr(startIndex, length)`**

   - The `substr()` method extracts a substring from the given string, starting from the `startIndex` and going for a specified `length`.
   - It takes two arguments: `startIndex` (required) and `length` (optional).
   - The `startIndex` is the starting index of the substring. If negative, it represents an offset from the end of the string.
   - The `length` parameter defines the number of characters to extract from the string. If not provided, it extracts until the end of the string.
   - Unlike `slice()` and `substring()`, `substr()` uses a length-based approach rather than an end index.

   Example:
   ```js
   const str = "Hello, world!";
   const sub = str.substr(0, 5); // "Hello"
   const sub2 = str.substr(7);   // "world!"
   ```

In summary, the primary differences between these methods are how they handle negative indices and the parameters they accept. The `slice()` method uses start and end indices, `substring()` uses start and end indices (swapping if necessary), and `substr()` uses a start index and length.

**Q10.** What are the three logical operators and what do they stand for?

**A10.** Logical operators in JavaScript are as follows :

1. **OR (` || `)**:

The " || " logical operator is used to find the first "truthy" value in a set of expressions, if none of the operands are truthy, "OR" returns the last falsy value instead.

2. **AND (` && `)**:

The " && " logical operator is used to find the first "falsy" value in a set of expressions, if none of the operands are falsy, "AND" returns the last truthy value instead.

3. **NOT (` ! `)**:

The " ! " operator first converts the operand to boolean type: true/false, and then returns the inverse value.

**Q11.** What are the comparison operators?

**A11.** In JavaScript, comparison operators are used to evaluate the relationship between values and determine whether one value is greater than, less than, equal to, or not equal to another value.

In JavaScript, comparison operators ( `>`, `<`, `>=`, `<=`, `==`, `!=`, `===`, and `!==` ) always return a boolean value, which is either `true` or `false`, depending on the result of the comparison. For example, `5 > 3` returns `true` because 5 is greater than 3.

**Q12.** What are truthy and falsy values?

**A12.** In JavaScript, values that are considered truthy are any values that evaluate to `true` when used in a boolean context.

Here's a list of some common truthy values in JavaScript:

- All non-empty strings (e.g., "hello", "false", "0", "-1")
- All numbers except 0 (e.g., -1, 1, 0.5)
- All objects (including arrays and functions)
- The special value `true`

Conversely, values that are considered falsy are any values that evaluate to `false` when used in a boolean context. Some common falsy values in JavaScript include:

- The empty string `""`
- The number 0 (zero)
- `null`
- `undefined`
- `NaN`
- The special value `false`

**When using a value in a boolean context, like in an if statement, JavaScript implicitly converts the value to a boolean using the truthy and falsy rules. For example:**

```javascript
if ("-1") {
  // This block will be executed because "-1" is truthy
}

if (0) {
  // This block will NOT be executed because 0 is falsy
}
```

**Q13.** What are the falsy values in JavaScript?

**A13.** Values that are considered falsy are any values that evaluate to `false` when used in a boolean context. Some common falsy values in JavaScript include:

- The empty string `""`
- The number 0 (zero)
- `null`
- `undefined`
- `NaN`
- The special value `false`

**Q14.** What are conditionals?

**A14.** Conditional statements in JavaScript allow us to control the flow of our code based on certain conditions. They enable our code to make decisions and execute different blocks of code depending on whether a condition is true or false. Conditional statements in JavaScript are:

+ `if` to specify a block of code to be executed, if a specified condition is true.
+ `else` to specify a block of code to be executed, if the same condition is false.
+ `else if` to specify a new condition to test, if the first condition is false.
+ `switch` to specify many alternative blocks of code to be executed.

**Q15.** What is the syntax for an if/else conditional?

**A15.** 
```javascript
const num1 = 5;
const num2 = 3;

if (num1 > num2) {
  console.log("First number is greater than the second number."); // This block of code will execute because the expression in the conditional evaluates to true.
}

else {
  console.log("This block of code will not execute.");
}
```

**Q16.** What is the syntax for a switch statement?

**A16.**
```javascript
const dayOfWeek = 1; // 1 corresponds to Monday

switch (dayOfWeek) {
  case 1:
    console.log("It's Monday.");
    break;

  case 2:
    console.log("It's Tuesday.");
    break;

  case 3:
    console.log("It's Wednesday.");
    break;

  case 4:
    console.log("It's Thursday.");
    break;

  case 5:
    console.log("It's Friday.");
    break;

  case 6:
    console.log("It's Saturday.");
    break;

  case 7:
    console.log("It's Sunday.");
    break;

  default:
    console.log("Invalid day of the week.");
}
```
In this example, we have a variable dayOfWeek which represents the day of the week. We use the switch statement to check the value of dayOfWeek and display the corresponding message in the console. The break statements are used to exit the switch block after each case is matched. If the value of dayOfWeek doesn't match any of the specified cases, the default case will be executed, printing "Invalid day of the week.

It's also important to note that, the case statements in a switch block should contain constant values, not expressions or conditions.

**Q17.** What is the syntax for a ternary operator?

**A17.** 
```javascript
const number = 5;
let result = (number > 0) ? true : false;
console.log(result); // true
```

```javascript
const number = 5;
let result = (number > 0) ? console.log("Number is greater than zero.") : console.log("Number is less than zero."); // Number is greater than zero.
```

**Q18.** What is nesting?

**A18.** Nesting in javascript, is placing a block of code inside an another block of code to be executed.



