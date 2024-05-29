# Measuring Algorithm Efficiency
The very first step in mastering efficient code is to understand how to measure it.

In computer science algorithm efficiency is typically measured in terms of time complexity and space complexity. These metrics help evaluate how well an algorithm or a piece of code performs in terms of execution time and memory usage.

Let’s take a look at a little program that prints out all odd numbers between 1 and 10.

```js
function oddNumbersLessThanTen() {
  let currentNumber = 1;

  while (currentNumber < 10) {
    if (currentNumber % 2 !== 0) {
      console.log(currentNumber);
    }

    currentNumber += 1;
  }
}
```

If you were to run this in your terminal, you should get the numbers 1, 3, 5, 7 and 9 printed to the console. It probably took a fraction of a second to run. If you were to run it again, it might take the same time, or it might be faster or slower depending on what else your computer is doing. If you were to run it on a different computer, it would again run faster or slower. Therefore it’s important to understand that you never measure the efficiency of an algorithm by how long it takes to execute.

So how do we measure it?

The way to measure code efficiency is to evaluate how many ‘steps’ it takes to complete. If you know that one algorithm you write takes 5 steps and another one takes 20 steps to accomplish the same task, then you can say that the 5-step algorithm will always run faster than the 20-step algorithm on the same computer.

Let’s go back to our `oddNumbersLessThanTen` function. How many steps does our algorithm take?

1. We assign the number 1 to a variable. That’s one step.

2. We have a loop. For each iteration of the loop, we do the following:<br>
  2.1 Compare currentNumber to see if it is less than 10. That is 1 step.<br>
  2.2 We then check if currentNumber is odd. That is 1 step.<br>
  2.3 If it is then we output it to the terminal. That’s 1 step every 2 iterations.<br>
  2.4 We increase currentNumber by 1. That is 1 step.<br>

3. To exit the loop, we need to compare currentNumber one last time to see that it is not less than ten any more. That is one last step.

So there are 3 steps for every loop iteration and it iterates 9 times which is 27 steps. Then we have one step which iterates for only half the loop iteration which is 5 steps. Assigning an initial value to currentNumber and checking the exit condition of the loop is one step each. 27 + 5 + 1 + 1 = 34 steps.

Therefore, we can say our algorithm takes 34 steps to complete.

While this is useful to know, it isn’t actually helpful for comparing algorithms. To see why, let’s slightly modify our initial algorithm to take in a number instead of setting a hard default of 10.

```js
function oddNumbers(maxNumber) {
  let currentNumber = 1;

  while (currentNumber < maxNumber) {
    if (currentNumber % 2 !== 0) {
      console.log(currentNumber);
    }

    currentNumber += 1;
  }
}
```

How many steps does this algorithm take?

You’ve probably realised the answer is it depends. If you set maxNumber to be 10, like we did before, the number of steps is 34, but if you enter another number then the number of steps changes. There is no concrete number we can use to measure the efficiency of our code because it changes based on an external input.

So what we really want to be able to measure is how the number of steps of our algorithm changes when the data changes. This helps us answer the question of whether the code we write will scale.

To do that, we need to delve into a new concept: **Asymptotic Notations** and, in particular, **Big O**.

## Asymptotic Notations
Asymptotic notations are mathematical notations used in computer science and mathematics to describe the growth rate of functions, particularly in the context of algorithm analysis. They provide a way to express the performance of algorithms in terms of their efficiency as the input size grows to infinity. Three commonly used asymptotic notations are Big O (O), Omega (Ω), and Theta (Θ):

1. **Big O (O) Notation:**
   - **Definition:** O(g(n)) is the set of functions that grow at most as fast as the function g(n) for sufficiently large n.
   - **Usage:** It provides an upper bound on the growth rate of a function, representing the worst-case scenario.

   Example: If an algorithm has a time complexity of O(n^2), it means that the running time grows no faster than a quadratic function of the input size (n).

2. **Omega (Ω) Notation:**
   - **Definition:** Ω(g(n)) is the set of functions that grow at least as fast as the function g(n) for sufficiently large n.
   - **Usage:** It provides a lower bound on the growth rate of a function, representing the best-case scenario.

   Example: If an algorithm has a time complexity of Ω(n), it means that the running time grows at least linearly with the input size (n).

3. **Theta (Θ) Notation:**
   - **Definition:** Θ(g(n)) is the set of functions that grow at the same rate as the function g(n) for sufficiently large n. It essentially combines the upper and lower bounds.
   - **Usage:** It provides a tight bound on the growth rate of a function.

   Example: If an algorithm has a time complexity of Θ(n), it means that the running time grows linearly with the input size (n) and no faster.

These notations are particularly useful for expressing the efficiency of algorithms in terms of time and space complexity. Asymptotic notations abstract away constant factors and focus on the dominant term of a function, providing a high-level understanding of how an algorithm's performance scales with input size. When analyzing algorithms, Big O notation is commonly used to describe the upper bound, while Omega notation describes the lower bound, and Theta notation is used when the upper and lower bounds match closely.

Big O is the one you’ll most commonly see referenced because you need to be sure the worst-case scenario for any code you write is scalable as the inputs grow in your application.

## `Big O notation (O)`
Big O notation (O) is a mathematical notation used to describe the upper bound or worst-case scenario of the growth rate of a function. In the context of computer science and algorithm analysis, it is commonly used to express the time complexity or space complexity of an algorithm.

Here's a more detailed explanation of Big O notation:

1. **Definition:**
   - Big O notation, denoted as O(g(n)), represents the set of functions that grow no faster than a constant multiple of the function g(n) for sufficiently large n(input).
   - It describes an upper limit on the rate of growth of a function. In other words, it provides an upper bound on the worst-case time or space complexity of an algorithm.

2. **Formal Definition:**
   - A function f(n) is said to be O(g(n)) if there exist positive constants c and n₀ such that 0 ≤ f(n) ≤ c * g(n) for all n ≥ n₀.
   - Essentially, for sufficiently large n, the function f(n) is bounded above by a constant multiple of g(n).

3. **Interpretation:**
   - When we say "f(n) is O(g(n))," it means that, asymptotically, the growth rate of f(n) is not faster than the growth rate of g(n) for large enough input sizes.

4. **Example:**
   - If an algorithm has a time complexity of O(n^2), it means that the running time of the algorithm grows quadratically with the input size (n), but it does not grow faster than some constant times n^2 for sufficiently large n.

5. **Common Time Complexities and Examples:**
   - O(1): Constant time complexity (e.g., accessing an element in an array).
   - O(log n): Logarithmic time complexity (e.g., binary search in a sorted array).
   - O(n): Linear time complexity (e.g., linear search in an unsorted array).
   - O(n log n): Linearithmic time complexity (e.g., efficient sorting algorithms like merge sort and heap sort).
   - O(n^2): Quadratic time complexity (e.g., simple nested loops).
   - O(2^n): Exponential time complexity (e.g., exhaustive search algorithms).

6. **Ignoring Constants and Lower Order Terms:**
   - Big O notation focuses on the dominant term of a function, ignoring constant factors and lower-order terms. This abstraction allows for a simplified analysis that captures the essential growth behavior.

In summary, Big O notation provides a way to express the upper bound on the worst-case growth rate of algorithms. It is a tool for comparing and analyzing the efficiency of algorithms without getting bogged down in specific implementation details or constant factors.

Big O notation focuses on the upper bound or worst-case scenario, which is often of primary concern when analyzing algorithms. In practice, developers and engineers are typically more interested in understanding the upper limit of an algorithm's performance, especially when dealing with time or space constraints. And this is why the Big O notation is often considered more useful than Theta notation or Omega notation.

### The Big O is focused on the dominant term
1. **Dominant Term Focus:**
   - Big O notation is concerned with identifying the term in an algorithm's time or space complexity expression that grows the fastest as the input size (n) becomes large. This dominant term often determines the overall growth rate of the function.
   - For example, in the expression `3n^2 + 5n + 2`, the dominant term is `3n^2`. In Big O notation, this would be expressed as O(n^2), and the constant factors (3, 5, 2) and lower-order terms (5n, 2) are ignored.

2. **Ignoring Constant Factors:**
   - Constant factors are numerical coefficients in front of the dominant term. Big O notation abstracts away these constants because they don't significantly impact the overall growth rate as the input size becomes large.
   - For example, whether an algorithm takes 2n^2 or 100n^2 operations is not crucial for the analysis. Both are represented as O(n^2).

3. **Ignoring Lower-Order Terms:**
   - Lower-order terms are terms that have a lower exponent than the dominant term. In Big O analysis, these terms are neglected because, as n becomes large, their impact on the overall growth becomes negligible compared to the dominant term.
   - For example, in the expression `3n^2 + 5n + 2`, the terms `5n` and `2` are lower-order terms. In Big O notation, they are ignored, and the focus is on the dominant term, leading to O(n^2).

4. **Simplified Analysis:**
   - By focusing on the dominant term and neglecting constant factors and lower-order terms, Big O notation provides a simplified analysis. This abstraction allows for a high-level understanding of an algorithm's efficiency without getting bogged down in detailed calculations.
   - It enables practitioners to compare and choose between algorithms based on their essential growth behavior rather than specific implementation details.

5. **Potential Effects on Algorithm Efficiency Analysis:**
   - The abstraction provided by Big O notation is powerful for making broad comparisons and informed decisions about algorithm selection.
   - Algorithms with the same Big O notation are expected to exhibit similar growth rates for large input sizes, making it easier to choose an algorithm that meets specific performance requirements.
   - However, it's important to note that Big O notation does not capture constant factors or fine-grained details of performance. In some cases, algorithms with different constant factors or lower-order terms might perform similarly for practical input sizes.

### [Step-by-Step Big O Complexity Analysis Guide, using Javascript](https://www.sahinarslan.tech/posts/step-by-step-big-o-complexity-analysis-guide-using-javascript)

# Time Complexity
Time complexity is a measure used in computer science to analyze the efficiency of an algorithm in terms of the amount of time it takes to run, based on the size of the input to the algorithm. It provides an estimate of the total time an algorithm would take for its worst-case, average-case, or best-case scenario.

The time complexity is usually expressed using big O notation, which describes the upper bound of the growth rate of an algorithm's running time as a function of the input size. In big O notation, common time complexities are denoted by expressions like O(1), O(log n), O(n), O(n log n), O(n^2), and so on.

Analyzing the time complexity of an algorithm helps in understanding how the algorithm's performance scales with increasing input sizes and allows developers to choose the most efficient algorithm for a given problem.

**Common Time Complexities and Examples:**
   - O(1): Constant time complexity (e.g., accessing an element in an array).
   - O(log n): Logarithmic time complexity (e.g., binary search in a sorted array).
   - O(n): Linear time complexity (e.g., linear search in an unsorted array).
   - O(n log n): Linearithmic time complexity (e.g., efficient sorting algorithms like merge sort and heap sort).
   - O(n^2): Quadratic time complexity (e.g., simple nested loops).
   - O(2^n): Exponential time complexity (e.g., exhaustive search algorithms).
   - O(n!): Factorial time complexity.

## O(1): Constant time complexity
In algorithm analysis, O(1) represents constant time complexity, which means that the time required to perform an operation remains constant regardless of the size of the input data. This is often considered the most efficient time complexity because the execution time does not depend on the size of the input.

Accessing an element in an array is a classic example of an operation with O(1) time complexity. In an array, elements are stored in contiguous memory locations, and accessing a specific element involves calculating the memory address directly based on the index. Since this operation does not involve iterating through the entire array or performing any additional computations related to the size of the array, the time required to access an element is constant.

In mathematical terms, if T(n) represents the time required for an operation on an input of size n, and T(n) is O(1), it means that there exists a constant c such that T(n) is always less than or equal to c, regardless of the input size. This constant time complexity is desirable in situations where quick and predictable execution times are crucial, especially for operations that need to be performed frequently.

## O(log n): Logarithmic time complexity
O(log n) represents logarithmic time complexity in algorithm analysis. This time complexity is commonly associated with algorithms that divide the input data in each step, leading to a significant reduction in the problem size with each iteration. Binary search in a sorted array is a classic example of an algorithm with O(log n) time complexity.

In binary search, the algorithm repeatedly divides the search interval in half. It compares the middle element of the interval with the target value and eliminates half of the remaining elements based on this comparison. By dividing the search space in half with each iteration, binary search efficiently narrows down the possible locations of the target element.

The logarithmic behavior arises because, with each step, the problem size is reduced by a constant factor. In the case of binary search, the search space is halved at each iteration. The logarithmic base in O(log n) is typically 2, reflecting the division of the problem size by 2 in each step.

In mathematical terms, if T(n) represents the time required for an operation on an input of size n, and T(n) is O(log n), it means that there exists a constant c such that T(n) is always less than or equal to c * log(n), where log denotes the logarithm with base 2. This logarithmic time complexity is highly efficient and desirable for scenarios where the input size can be quite large, as the algorithm's performance improves as the problem size increases.

## O(n): Linear time complexity
O(n) represents linear time complexity in algorithm analysis. In linear time complexity, the execution time of an algorithm grows linearly with the size of the input data. This means that as the input size increases, the time required to perform the operation also increases at a proportional rate.

Linear search in an unsorted array is a typical example of an algorithm with O(n) time complexity. In linear search, each element in the array is examined one by one until the target element is found or the entire array has been traversed. The time taken to perform the search is directly proportional to the size of the array.

In mathematical terms, if T(n) represents the time required for an operation on an input of size n, and T(n) is O(n), it means that there exists a constant c such that T(n) is always less than or equal to c * n. The linear relationship indicates that the time complexity grows linearly with the input size.

Linear time complexity is considered less efficient than constant or logarithmic time complexities, but it is still acceptable for many practical applications. Algorithms with linear time complexity may be suitable for smaller input sizes or situations where the problem inherently requires examining each element in the input. However, for larger datasets or scenarios where efficiency is critical, algorithms with lower time complexities (such as O(1) or O(log n)) are often preferred.

## O(n log n): Linearithmic time complexity
O(n log n) represents linearithmic time complexity in algorithm analysis. This time complexity is often associated with algorithms that combine linear and logarithmic behavior. Efficient sorting algorithms like merge sort and heap sort are examples of algorithms with O(n log n) time complexity.

In the context of sorting algorithms, achieving O(n log n) time complexity is considered quite efficient. Merge sort, for example, divides the input array into two halves, recursively sorts each half, and then merges the sorted halves. The key to the O(n log n) time complexity is that the array is repeatedly divided into halves, resulting in a logarithmic factor, and each element is eventually compared and processed, contributing to a linear factor.

The efficiency of these algorithms makes them suitable for handling large datasets compared to algorithms with O(n^2) time complexity, such as bubble sort or insertion sort, which become impractical for larger input sizes.

In mathematical terms, if T(n) represents the time required for an operation on an input of size n, and T(n) is O(n log n), it means that there exists a constant c such that T(n) is always less than or equal to c * n log n. The combination of linear and logarithmic factors indicates a more balanced growth in execution time as the input size increases, making these algorithms well-suited for a variety of sorting and searching applications in practice.

## O(n^2): Quadratic time complexity
O(n^2) represents quadratic time complexity in algorithm analysis. This time complexity is characterized by an algorithm whose execution time grows quadratically with the size of the input data. In other words, for each additional element in the input, the time required to perform the operation increases quadratically.

Simple nested loops are a common example of algorithms with O(n^2) time complexity. In such loops, each element in the input may be compared or processed with every other element, resulting in a total number of comparisons or operations proportional to the square of the input size.

For example, consider the following pseudocode for a simple nested loop:

```python
for i in range(n):
    for j in range(n):
        # Some operation involving i and j
```

In this code snippet, the inner loop runs 'n' times for every iteration of the outer loop, resulting in a total of 'n * n' iterations or operations, leading to a quadratic time complexity of O(n^2).

In mathematical terms, if T(n) represents the time required for an operation on an input of size n, and T(n) is O(n^2), it means that there exists a constant c such that T(n) is always less than or equal to c * n^2.

Quadratic time complexity is generally less desirable than linear (O(n)) or linearithmic (O(n log n)) time complexities for larger input sizes, as the execution time can grow rapidly. Algorithms with quadratic time complexity may become impractical for large datasets, and efforts are often made to optimize or replace them with more efficient algorithms when dealing with sizable inputs.

## O(2^n): Exponential time complexity
O(2^n) represents exponential time complexity in algorithm analysis. This time complexity is characterized by an algorithm whose execution time grows exponentially with the size of the input data. In other words, for each additional element in the input, the time required to perform the operation doubles, resulting in a rapidly increasing execution time.

Exponential time complexity is often associated with exhaustive search algorithms, where the algorithm explores all possible combinations or subsets of the input. The "brute force" approach to solving certain problems may involve checking all possible solutions, leading to an exponential growth in the number of operations.

A classic example is the recursive computation of the Fibonacci sequence using the naive approach:

```python
def fibonacci(n):
    if n <= 1:
        return n
    else:
        return fibonacci(n - 1) + fibonacci(n - 2)
```

The time complexity of this algorithm is O(2^n), as each call to `fibonacci` results in two recursive calls.

In mathematical terms, if T(n) represents the time required for an operation on an input of size n, and T(n) is O(2^n), it means that there exists a constant c such that T(n) is always less than or equal to c * 2^n.

Exponential time complexity is generally considered inefficient for larger input sizes. Algorithms with this time complexity may become impractical or even infeasible for inputs of moderate size due to the rapid increase in computational requirements. Efforts are often made to optimize or find alternative algorithms that offer better time complexities for such problems.

## O(n!): Factorial time complexity
O(n!) represents factorial time complexity in algorithm analysis. Factorial time complexity is associated with algorithms whose execution time grows at a rate proportional to the factorial of the input size. Factorial time complexity is highly inefficient and is generally impractical for large input sizes.

The factorial of a positive integer 'n' (denoted as n!) is the product of all positive integers up to 'n'. For example:

\[ n! = n \times (n-1) \times (n-2) \times \ldots \times 3 \times 2 \times 1 \]

An algorithm with O(n!) time complexity involves exploring all possible permutations or combinations of the input, resulting in a number of operations proportional to n!.

A common example of an algorithm with factorial time complexity is the brute-force solution to the traveling salesman problem, where the goal is to find the shortest possible route that visits a set of cities and returns to the starting city. The number of possible routes grows factorially with the number of cities, making it impractical for large instances.

In mathematical terms, if T(n) represents the time required for an operation on an input of size n, and T(n) is O(n!), it means that there exists a constant c such that T(n) is always less than or equal to c * n!.

Factorial time complexity is considered highly inefficient, and efforts are usually made to find alternative algorithms or heuristics that provide more manageable time complexities for solving combinatorial problems.

---
### Knowledge Check

**Q1.** What is Big O?

**A1.** Big O notation (O) is a mathematical notation used to describe the upper bound or worst-case scenario of the growth rate of a function. In the context of computer science and algorithm analysis, it is commonly used to express the time complexity or space complexity of an algorithm.

**Q2.** What are the Big O Notations?

**A2.**<br>
**Common Time Complexities and Examples:**
   - O(1): Constant time complexity (e.g., accessing an element in an array).
   - O(log n): Logarithmic time complexity (e.g., binary search in a sorted array).
   - O(n): Linear time complexity (e.g., linear search in an unsorted array).
   - O(n log n): Linearithmic time complexity (e.g., efficient sorting algorithms like merge sort and heap sort).
   - O(n^2): Quadratic time complexity (e.g., simple nested loops).
   - O(2^n): Exponential time complexity (e.g., exhaustive search algorithms).
   - O(n!): Factorial time complexity.

**Q3.** Why use Big O?

**A3.** Big O notation focuses on the upper bound or worst-case scenario, which is often of primary concern when analyzing algorithms. In practice, developers and engineers are typically more interested in understanding the upper limit of an algorithm's performance, especially when dealing with time or space constraints. And this is why the Big O notation is often considered more useful than Theta notation or Omega notation.

**Q4.** What is Omega notation and why isn’t it as useful?

**A4.**<br>
**Omega (Ω) Notation:**
   - **Definition:** Ω(g(n)) is the set of functions that grow at least as fast as the function g(n) for sufficiently large n.
   - **Usage:** It provides a lower bound on the growth rate of a function, representing the best-case scenario.

We are usually not interested in the best case scenario of our algorithms efficiency because even if our algorithm performs in constant time in best case, if it performs in quadratic or factorial time in the worst case scenario, our program will not perform very well with large inputs.