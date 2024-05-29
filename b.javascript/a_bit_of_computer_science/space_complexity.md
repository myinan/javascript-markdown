# Space Complexity
Space complexity is a term used in computer science to describe the amount of memory or storage space that an algorithm or a program requires to complete its execution. It is a measure of how efficiently an algorithm utilizes memory resources as the input size increases. The space complexity of an algorithm is typically expressed as a function of the input size.

Space Complexity of an algorithm is total space taken by the algorithm with respect to the input size. Space complexity includes both auxiliary space and space used by input. Auxiliary Space is the extra space or temporary space used by an algorithm.

The total space complexity of an algorithm is the sum of its input space and working space. When expressing space complexity using Big O notation, the focus is on the growth of the working space as a function of the input size.

We can break down the memory consumption of an algorithm into three different parts that mainly affect the space complexity:

+ **variables and constants**

Any function or algorithm that is based purely in variables or constants that are fixed and do not change over time will be measured as O(1) or constant space. These variables or constants will always take up the same amount of memory and thus do not need to be re-calculated for space after the program finishes running.

+ **inputs**

The initial parameters we are given to begin the function are important for space complexity. If we are given an array then we already know that there will need to be space allocated for the amount of elements in the array.

+ **execution**

Some functions will run and be completed right away, whereas some functions could be recursive or call other functions inside of itself. These functions could hold other functions on the stack waiting to be executed while it finishes. Space complexity is different for both of these situations. If a function completes as soon as it is called, no extra space is needed for it to be done. But in the case of a recursive function or a function calling another function inside of itself, extra space is needed in order to hold the values that are waiting to be executed.

### Space complexity and recursive functions
Recursive functions have a significant impact on space complexity, and understanding this relationship is crucial for analyzing the overall efficiency of an algorithm.

When a function is called recursively, a new instance of the function is created for each recursive call. Each instance of the function has its own set of local variables and parameters. These local variables and parameters are stored in the call stack, which is a region of memory dedicated to keeping track of function calls and their associated data.

The space complexity of a recursive algorithm depends on the depth of the recursion and the amount of space required for each recursive call. There are two key factors to consider:

1. **Depth of Recursion:**
   - The depth of recursion refers to how many times the function calls itself. Each recursive call adds a new frame to the call stack. The space complexity is directly proportional to the maximum depth of the recursion.

2. **Space Required per Call:**
   - The space required for each recursive call includes local variables, parameters, and any additional data structures used within the function. This space is multiplied by the number of active calls on the call stack.

The space complexity of a recursive algorithm can often be expressed using the following formula:

**{Space Complexity} = O(\text{Depth of Recursion} \times \text{Space per Call})**

It's important to be aware of potential issues like stack overflow when dealing with deep recursion, as excessive recursion can lead to a stack overflow error due to the limited size of the call stack.

However, some recursive algorithms can be optimized to reduce space complexity. Tail recursion, for example, is a special case where the recursive call is the last operation in the function, allowing for tail call optimization, which can potentially eliminate the need for additional stack frames.


```ruby
def get_sum(array)
  size = array.length
  if size == 1
    return array[0]
  else
    return (array[0] + get_sum(array[1...size]))
  end
end
```

This last example I wanted to include because it brings up the issue of recursion and space complexity. We can see here that the function is calling itself multiple times and what would you guess is the space complexity? It's actually O(n) because each time the function calls itself again, space needs to be made for the value to being stored on the stack, waiting for execution. Compared to its iterative counterpart, this takes up much more space where an iterative approach would use the same variable space over and over again, thus being only O(1).

---
### Knowledge Check

**Q1.** What is space complexity?

**A1.** Space complexity is a term used in computer science to describe the amount of memory or storage space that an algorithm or a program requires to complete its execution. It is a measure of how efficiently an algorithm utilizes memory resources as the input size increases. The space complexity of an algorithm is typically expressed as a function of the input size.

Space Complexity of an algorithm is total space taken by the algorithm with respect to the input size. Space complexity includes both auxiliary space and space used by input. Auxiliary Space is the extra space or temporary space used by an algorithm.

The total space complexity of an algorithm is the sum of its input space and working space. When expressing space complexity using Big O notation, the focus is on the growth of the working space as a function of the input size.

**Q2.** How do we measure space complexity?

**A2.** The total space complexity of an algorithm is the sum of its input space and working space. When expressing space complexity using Big O notation, the focus is on the growth of the working space as a function of the input size.

When measuring space complexity usually the O(Big-oh) notation is preferred because most of the time, we are more interested in the worst possible case for our algorithm.

We can break down the memory consumption of an algorithm into three different parts that mainly affect the space complexity:

+ **variables and constants**

Any function or algorithm that is based purely in variables or constants that are fixed and do not change over time will be measured as O(1) or constant space. These variables or constants will always take up the same amount of memory and thus do not need to be re-calculated for space after the program finishes running.

+ **inputs**

The initial parameters we are given to begin the function are important for space complexity. If we are given an array then we already know that there will need to be space allocated for the amount of elements in the array.

+ **execution**

Some functions will run and be completed right away, whereas some functions could be recursive or call other functions inside of itself. These functions could hold other functions on the stack waiting to be executed while it finishes. Space complexity is different for both of these situations. If a function completes as soon as it is called, no extra space is needed for it to be done. But in the case of a recursive function or a function calling another function inside of itself, extra space is needed in order to hold the values that are waiting to be executed.

**Q3.** What are the main considerations we should take into account when optimising code?

**A3.**<br>
+ Consider trade-offs between different data structures. For instance, using an array might be more memory-efficient than a linked list due to lower overhead.
+ Recursive algorithms can lead to stack overflow errors if not managed carefully. Consider tail recursion or converting the recursive approach to an iterative one to reduce stack space usage.
+ Use memoization techniques to store and reuse previously computed results, which can save memory in dynamic programming problems.

