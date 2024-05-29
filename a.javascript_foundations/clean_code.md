# Clean Code
Clean code principles in JavaScript aim to enhance code readability, maintainability, and overall quality. Writing clean code makes it easier for developers to understand, modify, and collaborate on projects. Several principles contribute to clean code in JavaScript:

1. **Meaningful Variable and Function Names:**
   <br>A good name is descriptive: Use descriptive and meaningful names for variables, functions, and classes. Avoid single-letter or ambiguous names that make code difficult to comprehend. Meaningful names convey the purpose and intention of the code.

   ```javascript
   // Bad: 
   const x = 10; // What does 'x' represent?
   
   // Good:
   const numberOfStudents = 10; // Clearly states the purpose of the variable.
   ```
   Use a consistent vocabulary: Variables of the same type should have consistent naming.

   ```javascript
    // Good
    function getPlayerScore();
    function getPlayerName();
    function getPlayerTag();

    // Bad
    function getUserScore();
    function fetchPlayerName();
    function retrievePlayer1Tag(); 
   ```
   In the bad example, three different names are used to refer to the player and the actions taken. Additionally, three different verbs are used to describe these actions. The good example maintains consistency in both variable naming and the verbs used.

   Variables should always begin with a noun or an adjective (that is, a noun phrase) and functions with a verb.

   ```javascript
    // Good
    const numberOfThings = 10;
    const myName = "Thor";
    const selected = true;

    // Bad (these start with verbs, could be confused for functions)
    const getCount = 10;
    const isSelected = true;

    // Good
    function getCount() {
    return numberOfThings;
    }

    // Bad (it's a noun)
    function myName() {
    return "Thor";
    }
   ```

   camelCase: camelCase is a naming convention that allows writing multiple words together without spaces or punctuation. In camelCase, when a variable name consists of multiple words like our setTimeout example, the first word is written completely in lowercase, while the second word (and any subsequent words) are capitalized.

2. **Function Length and Complexity:**
   Keep functions short and focused, adhering to the Single Responsibility Principle (SRP). Each function should do one thing and do it well. This makes functions easier to understand and maintain.

3. **Use Constants and Enums:**
   Use constants for fixed values and enums for representing a set of related values. This avoids "magic numbers" and improves code readability.

   ```javascript
   // Bad:
   if (status === 1) { ... } // What does '1' mean?
   
   // Good:
   const STATUS = {
     ACTIVE: 1,
     INACTIVE: 2,
   };
   
   if (status === STATUS.ACTIVE) { ... } // Clearly indicates the status being checked.
   ```

4. **Avoid Nested Callbacks (Callback Hell):**
   Use modern JavaScript features like Promises, async/await, or use libraries like `async.js` to avoid deep nesting of callbacks, which can lead to difficult-to-read code.

   ```javascript
   // Bad (Callback Hell):
   fetchData((data) => {
     process(data, (processedData) => {
       save(processedData, (response) => {
         // More code...
       });
     });
   });
   
   // Good (using Promises):
   fetchData()
     .then(process)
     .then(save)
     .then((response) => {
       // More code...
     })
     .catch((error) => {
       // Error handling...
     });
   ```

5. **Use ES6+ Features:**
   Utilize modern JavaScript features like arrow functions, template literals, destructuring, and spread operators. These features make the code concise and more expressive.

   ```javascript
   // Bad:
   function multiply(a, b) {
     return a * b;
   }
   
   // Good:
   const multiply = (a, b) => a * b;
   ```

6. **Consistent Formatting and Indentation:**
   Maintain consistent formatting and indentation throughout the codebase. Tools like ESLint can help enforce a consistent coding style.

   Line length: Generally your code will be easier to read if you manually break lines that are longer than about 80 characters. Many code editors have a line in the display to show when you have crossed this threshold. When manually breaking lines, you should try to break immediately after an operator or comma.

   Semicolons: Semicolons are mostly optional in JavaScript because the JS compiler will automatically insert them if they are omitted. This functionality CAN break in certain situations leading to bugs in your code so it is better to get used to adding semi-colons. Again, consistency is the main thing.

7. **Avoid Global Variables:**
   Minimize the use of global variables as they can lead to naming conflicts and make it challenging to reason about the code. Instead, use modules and encapsulate functionality.

8. **Error Handling:**
   Properly handle errors and exceptions. Use try-catch blocks to catch and handle errors gracefully, providing helpful error messages or logging them for debugging purposes.

   ```javascript
   try {
     // Code that might throw an error
   } catch (error) {
     console.error('An error occurred:', error);
   }
   ```

9. **Comments and Documentation:**
   Add comments to explain complex logic, algorithms, or any code that might be unclear to other developers. Write self-documenting code, but when necessary, provide clear and concise comments.

   Having said that; though comments are indeed a great tool, like any good tool, they can be misused. Especially for someone early in their coding journey, it might be tempting to have comments that explain everything the code is doing. This is not a good practice.

   Don’t comment when you should be using git: It might be tempting to have comments in your code that explain the changes or additions you have made. The problem is that you already have a tool to track changes - git! Keeping track of these comments will become a chore and you will have an incomplete picture of what has happened. Your files will also contain bloat that doesn’t belong there.

   Tell why, not how: The purpose of comments is not to provide pseudo code that duplicates your code. Good comments explain the reasons behind a piece of code. The code already tells us how it works; we need the comments to tell us why it works.

   ```javascript
    // Bad Example - comment doesn't tell why, only what and how

    // This function increments the value of i by 1
    function incrementI(i) {
        i = i + 1; // Add one to i
        return i;
    }

    // Better Example - comment tells a why

    // This function increments the value of index to move to the next element
    function incrementI(i) {
        i = i + 1;
        return i;
    }

    // Good Example - the code tells all that is needed

    function moveToNextElement(index) {
        index = index + 1;
        return index;
    }
   ```

   In the bad example, the comments explain twice what the code does. But for this, you could’ve just read the code, so the comments are redundant.

   In the better example, the comment clarifies the purpose of the function: moving to the next element. That’s good but we can do even better.

   In the good example, no comments are needed at all. The use of descriptive function and variable names eliminates the need for additional explanations.

   This doesn’t mean good code should lack comments. In many situations, well-placed comments are priceless. While comments are neither inherently good or bad, they are frequently used as a crutch. You should always write your code as if comments didn't exist. This forces you to write your code in the simplest, plainest, most self-documenting way you can humanly come up with.

10. **Avoid Code Duplication:**
    Repeating code increases maintenance efforts and introduces more opportunities for bugs. Extract common functionality into functions or modules and reuse them.

11. **Testing and Refactoring:**
    Write unit tests to verify the correctness of your code. Refactor code regularly to improve its structure and readability without changing its behavior. Continuous refactoring keeps the codebase clean and maintainable.

12. **Follow a Style Guide:**
    Consider using established style guides like Airbnb, Google, or StandardJS. A consistent style across the project helps with code maintenance and collaboration.

Clean code is not just a one-time effort; it's a continuous process of improvement. It is a skill that comes with experience, code reviews, and learning from others.

---

### Knowledge Check

**Q1.** Why is it important to write clean code?

**A1.** We write programs for the machines to execute but the humans to understand. Adhering to clean code principles makes it easier for other programmers, and our future-self, to understand the code we've written.

**Q2.** Name 5 clean code principles previously mentioned.

**A2.**
1. Use meaningful variable and function names.
2. Functions should be short and focused. They should do one thing and do it well.
3. Use constants for fixed values and uppercase to name the fixed value variables.
4. Maintain consistent formatting and indentation throughout the codebase.
5. Add comments to explain complex logic, algorithms, or any code that might be unclear to other developers. Write self-documenting code, but when necessary, provide clear and concise comments.

**Q3.** What is the difference between good comments and bad comments?

**A3.** Good comments explains "why" the code works. Bad comments explains "how" the code works. The code itself should explain how it works, not the comments.
<br>Good comments are precise and clear. Bad comments are bloated and tries to explain everything regarding the code.