# Algorithms
Since we have already touched the subject of algorithms, here we will be discussing some of the most commonly used algorithms.

## Sorting Algorithms
Sorting algorithms are a fundamental concept in computer science and are used to organize a collection of elements in a specific order. The goal of sorting is to arrange the elements in a sequence, often in ascending or descending order, making it easier to search for specific elements or perform other operations efficiently. There are various sorting algorithms, each with its own advantages, disadvantages, and use cases.

Since they can often reduce the complexity of a problem, sorting algorithms are very important in computer science. These algorithms have direct applications in searching algorithms, database algorithms, divide and conquer methods, data structure algorithms, and many more.

### Classification of a Sorting Algorithm
Sorting algorithms can be categorized based on the following parameters:

**1- The number of swaps or inversions required:**<br> This is the number of times the algorithm swaps elements to sort the input. Selection sort requires the minimum number of swaps.

**2- The number of comparisons:**<br> This is the number of times the algorithm compares elements to sort the input. Using Big-O notation, the sorting algorithm examples listed belove require at least O(nlogn) comparisons in the best case, and O(n^2) comparisons in the worst case for most of the outputs.

**3- Whether or not they use recursion:**<br> Some sorting algorithms, such as quick sort, use recursive techniques to sort the input. Other sorting algorithms, such as selection sort or insertion sort, use non-recursive techniques. Finally, some sorting algorithms, such as merge sort, make use of both recursive as well as non-recursive techniques to sort the input.

**4- Whether they are stable or unstable:**<br> Stable sorting algorithms maintain the relative order of elements with equal values, or keys. Unstable sorting algorithms do not maintain the relative order of elements with equal values / keys.

For example, imagine you have the input array [1, 2, 3, 2, 4]. And to help differentiate between the two equal values, 2, let's update them to 2a and 2b, making the input array [1, 2a, 3, 2b, 4].

Stable sorting algorithms will maintain the order of 2a and 2b, meaning the output array will be [1, 2a, 2b, 3, 4]. Unstable sorting algorithms do not maintain the order of equal values, and the output array may be [1, 2b, 2a, 3, 4].

Insertion sort, merge sort, and bubble sort are stable. Heap sort and quick sort are unstable.

**5- The amount of extra space required:**<br> Some sorting algorithms can sort a list without creating an entirely new list. These are known as in-place sorting algorithms, and require a constant O(1) extra space for sorting. Meanwhile, out of place sorting algorithms create a new list while sorting.

Insertion sort and quick sort are in place sorting algorithms, as elements are moved around a pivot point, and do not use a separate array.

Merge sort is an example of an out of place sorting algorithm, as the size of the input must be allocated beforehand to store the output during the sort process, which requires extra memory.

### `Merge Sort`
Merge Sort is a popular sorting algorithm that follows the Divide and Conquer paradigm. It efficiently sorts an array or list by dividing it into two halves, sorting each half recursively, and then merging the sorted halves. The key idea is to repeatedly divide the array into smaller subproblems until the base case is reached, and then merge the sorted solutions to build the final sorted array.

Here's a step-by-step explanation of the Merge Sort algorithm:

1. **Divide**: Split the unsorted array into two halves.

2. **Conquer**: Recursively sort each half. This step involves applying the same Merge Sort algorithm to the two halves of the array.

3. **Merge**: Combine the two sorted halves to produce a single sorted array. This is the crucial step that distinguishes Merge Sort from other sorting algorithms.

Let's delve deeper into each step:

#### 1. Divide
Divide the unsorted array into two halves. This process continues until the base case is reached, i.e., the array size becomes 1 or 0. The division can be done by finding the middle index of the array.

#### 2. Conquer
Recursively sort each half of the array. This is achieved by applying the Merge Sort algorithm to both the left and right halves. The recursion continues until the base case is reached, **where an array of size 1 is considered sorted**.

#### 3. Merge
The merging step is crucial in Merge Sort. It involves combining the two sorted halves into a single sorted array. The merging process compares elements from the two halves, selects the smaller (or larger, depending on the sorting order), and places it in the correct position in the merged array. This process continues until all elements are merged.

Here's a more detailed breakdown of the merge operation:

- Create temporary arrays to hold the two halves during the merging process.
- Initialize three indices: one for the main array and one for each temporary array.
- Compare elements from the two halves and select the smaller (or larger) element to be placed in the main array.
- Move the respective index in the temporary array to the next position.
- Repeat this process until all elements from both halves are merged into the main array.

Merge Sort has a time complexity of O(n log n) for all cases, making it efficient for large datasets. However, it does require additional space for the temporary arrays used in the merging process, making it a "divide-and-conquer" algorithm with a space complexity of O(n).

### `Quick Sort`
Quick Sort is another widely used sorting algorithm that also follows the Divide and Conquer paradigm. It is known for its efficiency and is often faster in practice than other sorting algorithms, especially for large datasets. Quick Sort works by selecting a pivot element from the array, partitioning the other elements into two sub-arrays according to whether they are less than or greater than the pivot, and then recursively sorting the sub-arrays.

Here's a step-by-step explanation of the Quick Sort algorithm:

1. **Pivot Selection**: Choose a pivot element from the array. There are different strategies for selecting the pivot, but a common approach is to pick the last element in the array.

2. **Partitioning**: Rearrange the array elements such that all elements smaller than the pivot are placed to its left, and all elements greater than the pivot are placed to its right. The pivot itself will be in its final sorted position. This process is called partitioning.

3. **Recursion**: Recursively apply the Quick Sort algorithm to the sub-arrays on the left and right of the pivot. This process continues until the base case is reached, typically when a sub-array has one or zero elements, as such an array is already considered sorted.

Here's a more detailed breakdown of each step:

#### 1. Pivot Selection
Choose a pivot element. As mentioned earlier, a common strategy is to select the last element in the array. Other strategies include choosing the first element, a random element, or even selecting the median of three randomly chosen elements.

#### 2. Partitioning
Reorder the array elements so that elements smaller than the pivot are on the left, and elements greater than the pivot are on the right. This is achieved using two pointers: one starting from the left end and another from the right end. The pointers move towards each other until an inversion is found (an element on the left is greater than the pivot and an element on the right is smaller than the pivot), at which point the elements are swapped. This process continues until the pointers meet. At this point, the pivot is in its final sorted position.

#### 3. Recursion
Recursively apply the Quick Sort algorithm to the sub-arrays on the left and right of the pivot. The pivot is already in its sorted position, so it does not need to be included in the subsequent recursive calls.

#### Example
Consider an array: [38, 27, 43, 3, 9, 82, 10]
1. Pivot Selection: Choose the last element, 10, as the pivot.
2. Partitioning: Rearrange the array to get [3, 9, 10, 27, 43, 82, 38].
3. Recursion: Apply Quick Sort to the left sub-array [3, 9, 10, 27] and the right sub-array [43, 82, 38].

Repeat the process until all sub-arrays have one or zero elements, resulting in a fully sorted array.

#### Time Complexity
Quick Sort has an average and best-case time complexity of O(n log n), making it very efficient for large datasets. However, in the worst case, when the pivot selection consistently results in poorly balanced partitions, the time complexity can degrade to O(n^2). Randomized pivot selection and other optimizations are often used to mitigate this issue.

#### Space Complexity
Quick Sort typically has an in-place implementation, meaning it doesn't require additional memory proportional to the size of the input. This results in a space complexity of O(log n) due to the recursive call stack.

### `Bubble Sort`
Bubble Sort is a simple sorting algorithm that repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. The pass through the list is repeated until the list is sorted. This algorithm gets its name because smaller elements "bubble" to the top of the list.

Here's a step-by-step explanation of the Bubble Sort algorithm:

1. **Pass through the List**: The algorithm iterates over the list multiple times, with each iteration referred to as a "pass" through the list.

2. **Comparisons and Swaps**: During each pass, the algorithm compares adjacent elements in the list. If the elements are in the wrong order (i.e., the current element is greater than the next one), they are swapped. This process is repeated until the end of the list is reached.

3. **Repeat Until Sorted**: Steps 1 and 2 are repeated until no more swaps are needed. At this point, the list is considered sorted.

Here's a more detailed breakdown of each step:

#### 1. Initial List
Consider an unsorted list: [5, 2, 9, 1, 5, 6]

#### 2. First Pass
- Compare 5 and 2 (swap as 5 > 2): [2, 5, 9, 1, 5, 6]
- Compare 5 and 9 (no swap needed): [2, 5, 9, 1, 5, 6]
- Compare 9 and 1 (swap as 9 > 1): [2, 5, 1, 9, 5, 6]
- Compare 9 and 5 (swap as 9 > 5): [2, 5, 1, 5, 9, 6]
- Compare 9 and 6 (swap as 9 > 6): [2, 5, 1, 5, 6, 9]

#### 3. Second Pass
- Compare 2 and 5 (no swap needed): [2, 5, 1, 5, 6, 9]
- Compare 5 and 1 (swap as 5 > 1): [2, 1, 5, 5, 6, 9]
- Compare 5 and 5 (no swap needed): [2, 1, 5, 5, 6, 9]
- Compare 5 and 6 (no swap needed): [2, 1, 5, 5, 6, 9]

#### 4. Third Pass
- Compare 2 and 1 (swap as 2 > 1): [1, 2, 5, 5, 6, 9]
- Compare 2 and 5 (no swap needed): [1, 2, 5, 5, 6, 9]
- Compare 5 and 5 (no swap needed): [1, 2, 5, 5, 6, 9]

#### 5. Fourth Pass
- Compare 1 and 2 (no swap needed): [1, 2, 5, 5, 6, 9]
- Compare 2 and 5 (no swap needed): [1, 2, 5, 5, 6, 9]

#### 6. Fifth Pass
- Compare 1 and 2 (no swap needed): [1, 2, 5, 5, 6, 9]

The list is now sorted. Notice that after each pass, the largest unsorted element "bubbles up" to its correct position at the end of the list.

#### Time Complexity
The time complexity of Bubble Sort is O(n^2) in the worst and average cases, where n is the number of elements in the list. This is because, in the worst case, each element must be compared and swapped with every other element. The best-case time complexity is O(n) when the list is already sorted, as no swaps are needed.

#### Space Complexity
Bubble Sort is an in-place sorting algorithm, meaning it doesn't require additional memory space proportional to the size of the input. Therefore, its space complexity is O(1).

### `Selection Sort`
Selection Sort is a simple and intuitive sorting algorithm that works by dividing the input list into two parts: a sorted portion and an unsorted portion. The algorithm repeatedly finds the smallest (or largest) element from the unsorted portion and swaps it with the first element in the unsorted portion. This process is repeated until the entire list is sorted.

Here's a detailed breakdown of the Selection Sort algorithm:

1. **Initialization**: Start with the entire list considered as unsorted.

2. **Selection of Minimum (or Maximum) Element**: Iterate through the unsorted portion of the list to find the minimum (or maximum) element.

3. **Swap with First Element in Unsorted Portion**: Swap the minimum (or maximum) element found in step 2 with the first element in the unsorted portion of the list.

4. **Expand Sorted Portion and Repeat**: Move the boundary between the sorted and unsorted portions one element to the right, expanding the sorted portion. Repeat steps 2-3 until the entire list is sorted.

Here's a more detailed breakdown:

#### 1. Initial List
Consider an unsorted list: [5, 2, 9, 1, 5, 6]

#### 2. First Pass
Find the minimum element in the unsorted portion (which is the entire list) and swap it with the first element.

- Find the minimum: 1
- Swap with the first element: [1, 2, 9, 5, 5, 6]

#### 3. Second Pass
Move the boundary between the sorted and unsorted portions one element to the right (excluding the already sorted element). Find the minimum in the new unsorted portion and swap it with the first element of the unsorted portion.

- Find the minimum: 2
- Swap with the first element: [1, 2, 9, 5, 5, 6]

#### 4. Third Pass
Move the boundary again and repeat the process.

- Find the minimum: 5
- Swap with the first element: [1, 2, 5, 9, 5, 6]

#### 5. Fourth Pass
Continue the process.

- Find the minimum: 5
- Swap with the first element: [1, 2, 5, 5, 9, 6]

#### 6. Fifth Pass
Final pass to sort the last remaining element.

- Find the minimum: 6
- Swap with the first element: [1, 2, 5, 5, 6, 9]

The list is now sorted.

#### Time Complexity
The time complexity of Selection Sort is O(n^2) in the worst and average cases, where n is the number of elements in the list. This is because, for each element in the unsorted portion, the algorithm needs to iterate through the remaining unsorted elements to find the minimum (or maximum). The best-case time complexity is also O(n^2) since, regardless of the initial order of elements, the algorithm performs the same number of comparisons and swaps.

#### Space Complexity
Selection Sort is an in-place sorting algorithm, meaning it doesn't require additional memory space proportional to the size of the input. Therefore, its space complexity is O(1).

### `Insertion Sort`
Insertion Sort is a simple sorting algorithm that builds the final sorted array one element at a time. It is much less efficient on large lists than more advanced algorithms such as quicksort, heapsort, or merge sort. However, Insertion Sort has some advantages—it is a stable sorting algorithm, it can be implemented as an online algorithm, and it works well for small datasets or mostly sorted datasets. The basic idea of Insertion Sort is to divide the array into a sorted and an unsorted region. The algorithm repeatedly takes an element from the unsorted region, compares it with elements in the sorted region, and inserts it at the correct position in the sorted region.

Here's a step-by-step explanation of the Insertion Sort algorithm:

1. **Initialization**: Start with the first element of the array considered as a sorted region, and the rest of the elements as an unsorted region.

2. **Take an Element from the Unsorted Region**: Iterate through the unsorted region, taking one element at a time.

3. **Insert into the Sorted Region**: Compare the element from the unsorted region with elements in the sorted region. Move elements in the sorted region that are greater than the current element to the right. Insert the current element at the correct position in the sorted region.

4. **Repeat Until the Entire Array is Sorted**: Repeat steps 2-3 until all elements are considered and the entire array is sorted.

Here's a more detailed breakdown:

#### 1. Initial List
Consider an unsorted list: [5, 2, 9, 1, 5, 6]

#### 2. First Pass
Start with the first element considered as the sorted region.

- Take the second element (2) from the unsorted region.
- Compare with the first element (5) in the sorted region. Since 2 < 5, move 5 to the right and insert 2 at the correct position.
- Result: [2, 5, 9, 1, 5, 6]

#### 3. Second Pass
Expand the sorted region to include the first two elements.

- Take the third element (9) from the unsorted region.
- Compare with the second element (5) in the sorted region. Since 9 > 5, no need to move elements.
- Result: [2, 5, 9, 1, 5, 6]

#### 4. Third Pass
Expand the sorted region to include the first three elements.

- Take the fourth element (1) from the unsorted region.
- Compare with the third element (9) in the sorted region. Move 9 to the right, then compare with the second element (5) and move 5 to the right. Finally, insert 1 at the correct position.
- Result: [1, 2, 5, 9, 5, 6]

#### 5. Fourth Pass
Continue the process.

- Take the fifth element (5) from the unsorted region.
- Compare with the fourth element (9) in the sorted region. Move 9 to the right, then compare with the third element (5) and move 5 to the right. Insert 5 at the correct position.
- Result: [1, 2, 5, 5, 9, 6]

#### 6. Fifth Pass
Continue the process.

- Take the sixth element (6) from the unsorted region.
- Compare with the fifth element (9) in the sorted region. Since 6 < 9, move 9 to the right.
- Compare with the fourth element (5) in the sorted region. Since 6 > 5, insert 6 at the correct position between 5 and 9.
- Result: [1, 2, 5, 5, 6, 9]

The list is now sorted.

#### Time Complexity
The time complexity of Insertion Sort is O(n^2) in the worst and average cases, where n is the number of elements in the list. This is because, in the worst case, for each element in the unsorted region, the algorithm needs to compare and possibly move all elements in the sorted region. The best-case time complexity is O(n) when the list is already sorted, as no or minimal comparisons and movements are needed.

#### Space Complexity
Insertion Sort is an in-place sorting algorithm, meaning it doesn't require additional memory space proportional to the size of the input. Therefore, its space complexity is O(1).

## Searching Algorithms
A "search algorithm" refers to a step-by-step process or set of rules designed to find a specific piece of information or a solution to a problem within a given set of data.

In the context of computer science and data structures, search algorithms are often applied to locate a particular item or value in a collection of data, such as an array or a database. The efficiency of a search algorithm is measured by factors like time complexity and space complexity, which determine how quickly and with how much memory the algorithm can find the desired information.

Common search algorithms include linear search, binary search, depth-first search, and breadth-first search, each suited to different types of data structures and problem scenarios. The choice of a specific search algorithm depends on the characteristics of the data and the requirements of the task at hand.

### `Linear Search`
Linear search, also known as sequential search, is a simple searching algorithm that finds the position of a target value within a list or array. It sequentially checks each element in the list until a match is found or the entire list has been searched without finding the target value.

Here's a step-by-step explanation of the Linear Search algorithm:

1. **Initialization**: Start at the beginning of the list.

2. **Comparison**: Compare the target value with the current element in the list.

3. **Match Found?**: If the current element is equal to the target value, the search is successful, and the position/index of the element is returned.

4. **Move to the Next Element**: If the current element is not equal to the target value, move to the next element in the list.

5. **Repeat Until Match or End of List**: Steps 2-4 are repeated until either a match is found or the entire list has been searched.

6. **Result**: If a match is found, return the position/index of the target element. If the entire list is searched without finding a match, return a special value (e.g., -1) to indicate that the target element is not in the list.

#### Time Complexity
The time complexity of Linear Search is O(n) in the worst and average cases, where n is the number of elements in the list. This is because, in the worst case, the algorithm may need to traverse the entire list to find the target value.

#### Space Complexity
Linear Search is an in-place algorithm, meaning it doesn't require additional memory space proportional to the size of the input. Therefore, its space complexity is O(1).

### `Binary Search`
Binary search is a highly efficient searching algorithm that finds the position of a target value within a **sorted** array or list. The key idea behind binary search is to divide the array into two halves at each step and eliminate half of the remaining elements based on the comparison with the target value. This process continues until the target value is found or the search space is reduced to zero. 

Here's a step-by-step explanation of the Binary Search algorithm:

1. **Initialization**: Start with the entire **sorted** array.

2. **Define Search Space**: Identify the middle element of the current search space.

3. **Comparison with Target Value**: Compare the middle element with the target value.

4. **Three Possible Outcomes**:
   - If the middle element is equal to the target value, the search is successful, and the position/index of the middle element is returned.
   - If the middle element is greater than the target value, the target must be in the left half of the current search space. Repeat the search in the left half.
   - If the middle element is less than the target value, the target must be in the right half of the current search space. Repeat the search in the right half.

5. **Repeat Steps 2-4**: Continue dividing the search space and repeating the comparison until the target value is found or the search space is reduced to zero.

6. **Result**: If the target value is found, return the position/index of the target element. If the entire search space is exhausted without finding a match, return a special value (e.g., -1) to indicate that the target element is not in the list.

#### Time Complexity
The time complexity of Binary Search is O(log n) in the worst and average cases, where n is the number of elements in the sorted array. This is because, at each step, the search space is halved.

#### Space Complexity
Binary Search is an in-place algorithm, meaning it doesn't require additional memory space proportional to the size of the input. Therefore, its space complexity is O(1).

## Graph Algorithms
Graph algorithms are a category of algorithms designed to operate on graphs, which are mathematical structures representing relationships between entities. A graph consists of a set of vertices (or nodes) and a set of edges connecting pairs of vertices.

### `Depth-First Search (DFS)`
Depth-First Search (DFS) is a graph traversal algorithm used to explore all the vertices and edges in a graph. It starts at a specified source node and explores as far as possible along each branch before backtracking. DFS can be used to solve various graph-related problems, such as finding connected components, detecting cycles, and traversing graphs.

Here's a detailed explanation of the DFS algorithm:

### Basic Idea:

1. **Starting Point:**
   - Choose a starting node (or vertex) as the source.
   - Mark the source node as visited.

2. **Exploration:**
   - Explore as deeply as possible along each branch before backtracking.
   - For each unvisited neighbor of the current node, visit that neighbor and repeat the process.

3. **Backtracking:**
   - If a vertex has no unvisited neighbors, backtrack to the previous node.
   - Continue until all vertices are visited or there are no more unexplored paths.

### Pseudocode:

```plaintext
DFS(graph, start):
    stack = []  # Stack to keep track of vertices to visit
    mark start as visited
    push start into stack

    while stack is not empty:
        current_vertex = pop from stack
        process current_vertex

        for each neighbor in neighbors of current_vertex:
            if neighbor is not visited:
                mark neighbor as visited
                push neighbor into stack
```

### Implementation Details:

- **Visited Set:**
  - Maintain a set or array to keep track of visited vertices to avoid revisiting the same node.

- **Stack:**
  - Use a stack (either explicitly or via recursion) to keep track of vertices to visit.
  - Alternatively, you can use a recursive approach where each recursive call explores a neighbor.

- **Processing:**
  - Process the current vertex according to the problem requirements (e.g., print, store, or analyze the node).

### Example:

Let's consider the following graph:

```
   A
  / \
 B   C
 |   |
 D   E
```

Starting at node A:

1. Visit A, mark it as visited, and push it onto the stack.
2. Pop A from the stack, visit its unvisited neighbors (B and C), mark them, and push them onto the stack.
3. Pop C from the stack, visit its unvisited neighbor (E), mark it, and push it onto the stack.
4. Pop E from the stack, backtrack to C, and then visit D (the remaining unvisited neighbor of C).
5. Continue this process until all nodes are visited.

### Preorder, Inorder, and Postorder traversal
In depth-first search (DFS) algorithms, preorder, inorder, and postorder are three different strategies for visiting and processing nodes in a tree. These strategies define the order in which the nodes are traversed.

Let's consider a binary tree for illustration purposes:

```
    1
   / \
  2   3
 / \
4   5
```

1. **Preorder Traversal:**
   - In preorder traversal, the root node is visited first, followed by the left subtree and then the right subtree.
   - The order of operations in preorder traversal is Root-Left-Right.
   - For the example tree, the preorder traversal would be: 1, 2, 4, 5, 3.

2. **Inorder Traversal:**
   - In inorder traversal, the left subtree is visited first, then the root node, and finally the right subtree.
   - The order of operations in inorder traversal is Left-Root-Right.
   - For the example tree, the inorder traversal would be: 4, 2, 5, 1, 3.

3. **Postorder Traversal:**
   - In postorder traversal, the left subtree is visited first, followed by the right subtree, and finally the root node.
   - The order of operations in postorder traversal is Left-Right-Root.
   - For the example tree, the postorder traversal would be: 4, 5, 2, 3, 1.

### Time Complexity:

The time complexity of DFS is O(V + E), where V is the number of vertices and E is the number of edges in the graph. Each vertex and edge are visited once in the worst case.

### Applications:

- **Connected Components:** Identifying connected components in an undirected graph.
- **Cycles:** Detecting cycles in a graph.
- **Pathfinding:** Finding paths between two vertices.

### `Breadth-First Search (BFS)`
Breadth-First Search (BFS) is a graph traversal algorithm used to explore all the vertices and edges in a graph. Unlike Depth-First Search (DFS), BFS explores the graph level by level, visiting all neighbors of a node before moving on to the next level. BFS is often employed in problems where finding the shortest path or exploring the graph layer-wise is important.

### Basic Idea:

1. **Starting Point:**
   - Choose a starting node (or vertex) as the source.
   - Mark the source node as visited.

2. **Exploration:**
   - Explore all neighbors of the current node before moving on to their neighbors.
   - Use a queue data structure to maintain the order of traversal.

3. **Level-Order Traversal:**
   - Traverse the graph level by level, visiting all nodes at the current level before moving to the next level.

### Pseudocode:

```plaintext
BFS(graph, start):
    queue = []  # Queue to keep track of vertices to visit
    mark start as visited
    enqueue start into queue

    while queue is not empty:
        current_vertex = dequeue from queue
        process current_vertex

        for each neighbor in neighbors of current_vertex:
            if neighbor is not visited:
                mark neighbor as visited
                enqueue neighbor into queue
```

### Implementation Details:

- **Visited Set:**
  - Maintain a set or array to keep track of visited vertices to avoid revisiting the same node.

- **Queue:**
  - Use a queue to maintain the order of traversal.
  - Enqueue the starting node and continue dequeuing and enqueueing neighbors until the queue is empty.

- **Processing:**
  - Process the current vertex according to the problem requirements (e.g., print, store, or analyze the node).

### Example:

Let's consider the following graph:

```
   A
  / \
 B   C
 |   |
 D   E
```

Starting at node A:

1. Enqueue A into the queue and mark it as visited.
2. Dequeue A from the queue, enqueue its unvisited neighbors (B and C), and mark them as visited.
3. Dequeue B from the queue, enqueue its unvisited neighbor (D), and mark it as visited.
4. Dequeue C from the queue, enqueue its unvisited neighbor (E), and mark it as visited.
5. Continue this process until all nodes are visited.

### Time Complexity:

The time complexity of BFS is O(V + E), where V is the number of vertices and E is the number of edges in the graph. Each vertex and edge are visited once in the worst case.

### Applications:

- **Shortest Path:** Finding the shortest path between two vertices in an unweighted graph.
- **Connected Components:** Identifying connected components in an undirected graph.
- **Maze Solving:** Navigating a maze to find the shortest path.
- **Network Routing:** Discovering the optimal path in computer networks.

Breadth-First Search is a powerful algorithm with various applications, especially in scenarios where exploring a graph layer-wise is essential.

### `Dijkstra's Algorithm` (for finding the shortest paths in a graph)
Dijkstra's Algorithm is a popular algorithm in computer science used for finding the shortest path between two nodes in a graph, especially in weighted graphs where each edge has a numerical weight. The algorithm was conceived by Dutch computer scientist Edsger Dijkstra in 1956.

Here's a step-by-step explanation of Dijkstra's Algorithm:

1. **Initialization:**
   - Create a set of unvisited nodes and assign tentative distances to all nodes. Set the starting node's distance to 0 and all other nodes' distances to infinity.
   - Mark all nodes as unvisited.

2. **Set Current Node:**
   - Choose the initial node as the current node.

3. **Explore Neighbors:**
   - For the current node, consider all of its neighbors (nodes directly connected to it by an edge). Calculate their tentative distances through the current node. Compare the newly calculated tentative distance to the current assigned value and assign the smaller one. This step effectively updates the shortest distance to each neighboring node.

4. **Mark as Visited:**
   - After considering all neighbors of the current node, mark the current node as visited.

5. **Select Next Node:**
   - Select the unvisited node with the smallest tentative distance as the next "current node" and go back to step 3.

6. **Repeat:**
   - Repeat steps 3-5 until all nodes are visited or the destination node is reached.

The algorithm works on the principle of always choosing the node with the smallest tentative distance to visit next, ensuring that the shortest path to each node is found gradually. Once the destination node is marked as visited, the algorithm stops, and the shortest path can be reconstructed by backtracking from the destination node to the start.

Dijkstra's Algorithm guarantees the discovery of the shortest path in non-negative weighted graphs. However, it may not work correctly if the graph contains negative weights, as it assumes that once a node is marked as visited, its tentative distance is final. For graphs with negative weights, other algorithms like Bellman-Ford may be more suitable.

[**A more detailed explanation of the Dijkstra's Algorithm**](https://www.freecodecamp.org/news/dijkstras-shortest-path-algorithm-visual-introduction/)

### Differences between Dijkstra's Algorithm and Breadth-First Search (BFS) Algorithm
While Dijkstra's Algorithm and Breadth-First Search (BFS) share some similarities, they are distinct algorithms with different purposes and characteristics. Both algorithms explore a graph in a systematic way, but their goals and the manner in which they prioritize nodes differ.

Here are the key differences:

1. **Goal:**
   - Dijkstra's Algorithm is designed to find the shortest path from a source node to all other nodes in a weighted graph, where each edge has a non-negative weight.
   - BFS, on the other hand, is primarily used for exploring all the nodes at the same level of depth from the starting node and is often employed for graph traversal without considering edge weights.

2. **Priority:**
   - Dijkstra's Algorithm uses a priority queue or a min-heap to always select the node with the smallest tentative distance for exploration. It prioritizes nodes based on the current known distance from the source.
   - BFS explores nodes in layers, starting from the source node and moving outward to nodes at increasing depths. It doesn't consider edge weights and explores nodes in the order they are encountered.

3. **Edge Weights:**
   - Dijkstra's Algorithm is specifically designed for graphs with weighted edges, and it takes into account the weights to find the shortest paths.
   - BFS does not consider edge weights. It simply explores all neighbors of a node without distinguishing between different edge weights.

4. **Final Distances:**
   - Dijkstra's Algorithm provides the shortest path distances from the source to all other nodes in the graph.
   - BFS, when applied to an unweighted graph, provides the shortest path distances from the source to all other nodes in terms of the number of edges.

In summary, while Dijkstra's Algorithm and BFS both involve systematic exploration of a graph, Dijkstra's is tailored for finding the shortest paths in weighted graphs, whereas BFS is a general graph traversal algorithm that doesn't consider edge weights.

### Differences between Dijkstra's Algorithm and Depth-First Search (DFS) Algorithm
Dijkstra's Algorithm and Depth-First Search (DFS) are two different algorithms with distinct purposes and approaches in graph theory. Here are the key differences between Dijkstra's Algorithm and DFS:

1. **Goal:**
   - **Dijkstra's Algorithm:** Its primary goal is to find the shortest path from a source node to all other nodes in a weighted graph, where each edge has a non-negative weight.
   - **Depth-First Search:** DFS is primarily used for exploring all nodes in a graph, typically to traverse the entire graph or find specific paths. It doesn't consider edge weights.

2. **Edge Weights:**
   - **Dijkstra's Algorithm:** Specifically designed for graphs with weighted edges. It considers the weights to determine the shortest paths.
   - **Depth-First Search:** Does not consider edge weights. It explores the graph by moving as far as possible along each branch before backtracking.

3. **Path Finding:**
   - **Dijkstra's Algorithm:** Guarantees finding the shortest paths from the source node to all other nodes in a graph with non-negative edge weights.
   - **Depth-First Search:** Does not guarantee finding the shortest path. It may find any path from the source to a destination but doesn't necessarily find the shortest one.

4. **Exploration Strategy:**
   - **Dijkstra's Algorithm:** Uses a priority queue or min-heap to always select the node with the smallest tentative distance for exploration, ensuring that the shortest paths are discovered first.
   - **Depth-First Search:** Explores the graph by going as deep as possible along a branch before backtracking. It does not necessarily prioritize shorter paths.

5. **Applications:**
   - **Dijkstra's Algorithm:** Primarily used for network routing, finding the shortest path between two points in a map, and other scenarios where finding the optimal path is crucial.
   - **Depth-First Search:** Used for topological sorting, cycle detection, and connectivity analysis. It is also a fundamental building block for other algorithms, such as those used in solving puzzles or searching through game trees.

In summary, Dijkstra's Algorithm and Depth-First Search serve different purposes. Dijkstra's is specialized for finding shortest paths in weighted graphs, while DFS is a more general algorithm for exploring and traversing graphs.

## Hashing Algorithms (Hash functions (e.g., SHA-256, MD5))
Hashing algorithms are fundamental components of computer science and information security. They play a crucial role in various applications, including data integrity verification, password storage, digital signatures, and more. Here's a detailed explanation of hashing algorithms:

### 1. **Definition:**
A hashing algorithm is a mathematical function that takes an input (or 'message') and produces a fixed-size string of characters, which is typically a hash value or digest. The output, known as the hash code, is unique to the input data, meaning even a small change in the input should result in a significantly different hash.

### 2. **Key Characteristics:**
   - **Deterministic:** The same input will always produce the same hash.
   - **Efficient:** The hashing process should be fast and not computationally expensive.
   - **Irreversible:** It should be computationally infeasible to reverse the process and obtain the original input from the hash.
   - **Fixed Output Size:** Regardless of the input size, the hash function produces a fixed-size output.
   - **Avalanche Effect:** A small change in the input data should result in a significantly different hash value. This property ensures that similar inputs don't produce similar hash outputs.
   - **Collision Resistance:** It should be computationally infeasible to find two different inputs that produce the same hash value. Collisions weaken the security of hash functions.

### 3. **Common Hashing Algorithms:**
   - **MD5 (Message Digest Algorithm 5):**<br>
      + MD5 was popular in the past but is now considered insecure for cryptographic purposes due to vulnerabilities that allow for collision attacks.
      + It produces a fixed-size 128-bit (16-byte) hash value.
      + Despite its insecurity, MD5 is still used in non-cryptographic applications, such as checksums for file integrity.
   - **SHA-1 (Secure Hash Algorithm 1):** Deprecated due to vulnerabilities. It produces a 160-bit hash.
   - **SHA-256, SHA-384, SHA-512 (Secure Hash Algorithms):** Part of the SHA-2 family, widely used for security. They produce hash values of 256, 384, and 512 bits, respectively.
   - **bcrypt, scrypt, Argon2:** Specifically designed for password hashing, they incorporate techniques to slow down brute-force attacks.

### 4. **Applications:**
   - **Data Integrity:** Hashing is used to verify the integrity of data during transmission. If the received hash matches the computed hash, the data is likely intact.
   - **Digital Signatures:** Hash functions are an integral part of digital signatures, ensuring the authenticity and integrity of the signed data.
   - **Password Storage:** Hashing is used to store passwords securely. Instead of storing plain-text passwords, systems store the hash values, making it difficult for attackers to retrieve the original passwords.
   - **Hash Tables:** In computer science, hash functions are employed in hash tables to quickly locate a data record, given its search key.

### 5. **Collision and Security:**
   - **Collision:** When two different inputs produce the same hash output. Avoiding collisions is crucial for the effectiveness of hashing algorithms.
   - **Security:** A secure hash function should be resistant to collision attacks, pre-image attacks, and second pre-image attacks.

### 6. **Cryptographic Hash Functions:**
   - Cryptographic hash functions are a subset designed for use in security applications. They meet additional criteria, such as being resistant to various attacks.

### 7. **Example (SHA-256):**
   - If you input the string "Hello, World!" into a SHA-256 hash function, you'll get a fixed-size (256-bit) hexadecimal hash like `a591a6d40bf420404a011733cfb7b190d62c65bf0bcda32b57b277d9ad9f146e`.

### 8. **Secure Implementation:**
   - Always use established and well-reviewed hashing algorithms.
   - Utilize techniques like salting for password storage to add an extra layer of security.

It's important to choose the appropriate hashing algorithm based on the specific requirements of the application. For security-sensitive applications, SHA-256 or other members of the SHA-2 family are recommended due to their resistance to current cryptographic attacks.

## String Matching and Parsing Algorithms
Pattern matching/searching is one of the most important problem in Computer Science. There have been a lot of research on the topic but we’ll enlist only two basic necessities for any programmer.

### `KMP Algorithm` (String Matching)
The Knuth-Morris-Pratt algorithm is a linear time pattern matching algorithm used to find occurrences of a substring within another string. Its efficiency comes from the way it processes the input string, avoiding unnecessary comparisons. Knuth-Morris-Pratt algorithm is used in cases where we have to match a short pattern in a long string. For instance, when we Ctrl+F a keyword in a document, we perform pattern matching in the whole document.

Let's break down the algorithm step by step:

### 1. Motivation:

The naive approach for pattern matching involves sliding the pattern over the input string character by character and checking for a match at each position. However, this can lead to redundant comparisons.

### 2. Prefix Function:

The key insight in KMP is to preprocess the pattern to identify potential matches before the actual matching process begins. This is done by calculating the prefix function, which for each position in the pattern tells us the length of the longest proper prefix that is also a proper suffix ending at that position.

For example, for the pattern "ABABC", the prefix function is:

```
A  B  A  B  C
0  0  1  2  0
```

This means that at position 3, the longest proper prefix that is also a proper suffix is of length 1 ("A").

### 3. Partial Match Table (PMT):

The partial match table, also known as the failure function or the prefix function, is constructed based on the prefix function. It's an array that tells us how much we can jump ahead in the pattern when a mismatch occurs.

For example, using the prefix function above, the PMT is:

```
A  B  A  B  C
0  0  1  2  0
```

### 4. Matching Process:

Now, armed with the PMT, we can efficiently search for the pattern in the input string.

- Start with the leftmost characters of both the pattern and the input string.
- If there's a match, move to the next characters in both.
- If there's a mismatch at position `i` in the pattern, consult the PMT to determine how much we can jump ahead.

### 5. Example:

Let's say we are trying to match the pattern "ABABC" in the text "ABABABC":

```
Pattern:   A  B  A  B  C
Text:      A  B  A  B  A  B  C
PMT:       0  0  1  2  0
```

- Initially, there's a match at position 2.
- At position 5, there's a mismatch at the character 'A'. Using the PMT, we jump ahead by 2 positions.
- Continue this process until a match is found or the end of the text is reached.

### 6. Complexity:

The construction of the PMT takes O(m) time, where m is the length of the pattern. The matching process takes O(n) time, where n is the length of the text. Therefore, the overall time complexity is O(m + n).

### 7. Pseudocode:

Here's a simplified pseudocode for the KMP algorithm:

```python
def kmp_search(pattern, text):
    m = len(pattern)
    n = len(text)

    # Construct the PMT
    pmt = compute_pmt(pattern)

    # Matching process
    i, j = 0, 0
    while i < n:
        if pattern[j] == text[i]:
            i += 1
            j += 1
            if j == m:
                print("Pattern found at index", i - j)
                j = pmt[j - 1]  # Continue searching for more occurrences
        else:
            if j != 0:
                j = pmt[j - 1]
            else:
                i += 1

def compute_pmt(pattern):
    m = len(pattern)
    pmt = [0] * m
    j = 0

    for i in range(1, m):
        if pattern[i] == pattern[j]:
            j += 1
            pmt[i] = j
        else:
            if j != 0:
                j = pmt[j - 1]
                i -= 1  # Retry the current character in the next iteration

    return pmt
```

### 8. Applications:
+ Text Processing and Editing: KMP is widely used in text editors and word processors for find-and-replace functions.
+ Data Compression: It assists in finding repeated patterns, which is crucial in various data compression techniques.
+ Bioinformatics: In DNA and protein sequence analysis, KMP helps in pattern matching, which is fundamental in genetic research and diagnostics.
+ Network Security: It’s used in intrusion detection systems for matching patterns in network traffic.

The Knuth-Morris-Pratt algorithm revolutionized string searching in computer science. Its efficient use of previously matched character information to minimize unnecessary comparisons makes it a preferred choice in various applications that require fast and reliable pattern matching. The KMP algorithm remains a fundamental tool in the field of computer science, demonstrating the impact of algorithmic efficiency in solving real-world problems.

### `Regular Expression` (String Parsing)
A regular expression (regex or regexp) is a powerful tool for matching patterns in strings. It is a sequence of characters that forms a search pattern and is used for pattern matching within strings. Regex provides a concise and flexible way to search, match, and manipulate text based on specified patterns.

In a regular expression:

- **Literals:** Characters that match themselves.
- **Metacharacters:** Special characters with a symbolic meaning. For example, `.` represents any character, `*` represents zero or more occurrences of the preceding character, and `|` represents alternation (OR).

Regex is widely used in text processing tasks such as searching, extracting, and replacing text in a variety of applications, including programming languages, text editors, command-line tools, and data validation.

The algorithm for processing regular expressions involves several steps:

1. **Compilation:**
   - When you create a regular expression, it needs to be compiled into a data structure that represents the pattern. This compilation step involves parsing the regular expression and generating a finite automaton or a similar structure.
   - The regular expression is typically represented as a combination of characters and special symbols that define the pattern to be matched.

2. **Determining the Finite Automaton:**
   - A finite automaton is a theoretical machine that can recognize patterns in strings. It consists of states, transitions between states, and a set of accepting states.
   - The regular expression is transformed into an equivalent deterministic finite automaton (DFA) or a nondeterministic finite automaton (NFA). Both DFAs and NFAs can recognize the same set of regular languages.

3. **Matching Process:**
   - Once the finite automaton is determined, the matching process begins. This involves traversing the automaton based on the input string.
   - The automaton starts in an initial state, and for each character in the input string, it transitions to a new state based on the current state and the input character.
   - The goal is to reach an accepting state after processing the entire input string. If the automaton reaches an accepting state, the string is considered a match for the regular expression.

4. **Backtracking (for NFA):**
   - If the regular expression involves features like alternation (`|`) or quantifiers (`*`, `+`, `?`), and an NFA is used, backtracking may be required.
   - Backtracking involves exploring multiple paths in the automaton to find a valid match. If one path fails, the algorithm may backtrack to a previous decision point and try a different path.
   - This process continues until all possible paths are explored or a match is found.

5. **Optimizations (for DFA):**
   - DFAs, being deterministic, do not require backtracking. They follow a single path through the automaton for each input character.
   - DFAs can be more efficient than NFAs for certain types of regular expressions. The transition table in a DFA maps each state and input symbol to the next state, eliminating the need for repeated decision-making during matching.

6. **Capturing Groups and Other Features:**
   - Some regular expressions include capturing groups, which are portions of the match that are extracted for further use. The algorithm must keep track of these groups during the matching process.
   - Other features, such as assertions (`^`, `$`, `\b`) and character classes (`[a-z]`), require additional logic to enforce specific conditions during matching.

In summary, the regular expression algorithm involves compiling the pattern into a finite automaton and then traversing this automaton based on the input string. The use of NFAs may involve backtracking, while DFAs offer optimizations for certain types of patterns. The algorithm ensures efficient and accurate pattern matching for a wide range of string manipulation tasks.

### Difference Between Regular Expression Algorithm and KMP Algorithm:

#### 1. **Purpose:**
   - **Regular Expression Algorithm:**
     - Primarily used for pattern matching and manipulation in a broader sense. Regex provides a versatile and expressive way to define patterns.
   - Regex engines support a wide range of pattern-matching capabilities, including character classes, quantifiers, anchors, and more.

   - **KMP Algorithm:**
     - Specifically designed for pattern matching within strings.
     - Focuses on efficiently finding occurrences of a fixed pattern within a given text.

#### 2. **Flexibility:**
   - **Regular Expression Algorithm:**
     - Offers a high level of flexibility and expressiveness for defining complex patterns.
     - Suitable for scenarios where the pattern to be matched may have variations or where multiple patterns need to be matched simultaneously.

   - **KMP Algorithm:**
     - Specialized for a fixed pattern. It excels when the pattern is known in advance and remains constant.

#### 3. **Algorithm Complexity:**
   - **Regular Expression Algorithm:**
     - The underlying algorithms for regular expressions can vary based on the engine and the complexity of the pattern. Some regex engines use finite automata, while others use backtracking algorithms.
     - The time complexity of regular expression matching can be affected by the complexity of the pattern.

   - **KMP Algorithm:**
     - Specifically designed for linear time pattern matching. The time complexity is O(m + n), where m is the length of the pattern and n is the length of the text.

#### 4. **Use Cases:**
   - **Regular Expression Algorithm:**
     - Widely used in scenarios where flexible and complex pattern matching is required, such as searching for specific formats in text data or validating input based on patterns.

   - **KMP Algorithm:**
     - Suitable for scenarios where the goal is to efficiently find occurrences of a fixed pattern within a large body of text, such as substring search in text processing.

#### 5. **Implementation:**
   - **Regular Expression Algorithm:**
     - Implemented by regex engines in programming languages (e.g., Python, JavaScript, Java), and the implementation details can vary between engines.

   - **KMP Algorithm:**
     - Implemented as a specific algorithm for substring search. The KMP algorithm has a clear and standardized implementation based on the prefix function and partial match table.

In summary, regular expressions provide a general-purpose pattern-matching framework with high flexibility, while the KMP algorithm is a specialized algorithm tailored for efficient substring search within a fixed pattern. Both have their strengths and are used in different contexts based on the requirements of the task at hand.

## Compression Algorithms
### `Huffman Coding Algorithm`
Huffman coding is a widely used algorithm for lossless data compression. It was developed by David A. Huffman in 1952. The main idea behind Huffman coding is to assign variable-length codes to input characters, with shorter codes assigned to more frequently occurring characters and longer codes assigned to less frequently occurring characters. This results in a more efficient representation of the input data, reducing the overall size of the encoded message.

Here's a detailed explanation of the Huffman coding algorithm:

1. **Frequency Analysis:**
   - The first step is to analyze the input data and determine the frequency of each character. This involves counting the occurrences of each symbol (characters, in the case of text data) in the input.

2. **Create Nodes:**
   - Create a leaf node for each unique symbol in the input, where the weight or frequency of the node is set to the frequency of the corresponding symbol.

3. **Priority Queue (Min Heap):**
   - Put all the leaf nodes into a priority queue or a min-heap based on their frequencies. The node with the lowest frequency will have the highest priority.

4. **Build Huffman Tree:**
   - While there is more than one node in the priority queue, extract the two nodes with the lowest frequencies.
   - Create a new internal node with a frequency equal to the sum of the frequencies of the two nodes just extracted. This internal node becomes the parent of the two nodes.
   - Insert the new internal node back into the priority queue.
   - Repeat this process until there is only one node left in the priority queue. This node is the root of the Huffman tree.

5. **Assign Codes:**
   - Traverse the Huffman tree from the root to each leaf. Assign a binary code (0 or 1) to each branch, with 0 for the left branch and 1 for the right branch.
   - The binary code for each symbol is the sequence of 0s and 1s encountered during the traversal.

6. **Generate Huffman Codes:**
   - After traversing the tree and reaching each leaf node, the binary code assigned to that leaf node is the Huffman code for the corresponding symbol.

7. **Encode Data:**
   - Encode the input data by replacing each symbol with its corresponding Huffman code.

8. **Compression:**
   - The encoded data is now a compressed representation of the original input, with shorter codes assigned to more frequent symbols and longer codes to less frequent symbols.

Huffman coding is a variable-length prefix coding, meaning that no code is a prefix of another. This property allows for efficient decoding of the encoded data without the need for delimiters between codes. The efficiency of Huffman coding lies in the fact that frequently occurring symbols have shorter codes, resulting in a more compact representation of the data.

# Data Structures
## `Array`
In JavaScript, an array is a built-in data structure that allows you to store and organize multiple values under a single variable. These values can be of any data type, including numbers, strings, objects, or even other arrays. Arrays are especially useful when you need to work with a collection of similar or related data.

Here are some key characteristics and features of arrays in JavaScript:

1. **Declaration:**
   You can create an array in JavaScript using the `Array` constructor or the array literal notation (`[]`).

   ```javascript
   // Using Array constructor
   let myArray = new Array();

   // Using array literal notation
   let myArrayLiteral = [];
   ```

2. **Indexing:**
   Elements in an array are stored in a sequential order, and each element has an index. The index starts at 0 for the first element and increments by 1 for each subsequent element.

   ```javascript
   let colors = ['red', 'green', 'blue'];
   console.log(colors[0]); // Output: 'red'
   console.log(colors[1]); // Output: 'green'
   console.log(colors[2]); // Output: 'blue'
   ```

3. **Length Property:**
   Arrays have a `length` property that indicates the number of elements in the array.

   ```javascript
   let numbers = [1, 2, 3, 4, 5];
   console.log(numbers.length); // Output: 5
   ```

4. **Mutability:**
   Arrays in JavaScript are mutable, meaning you can change the values of individual elements, add new elements, or remove existing ones.

   ```javascript
   let fruits = ['apple', 'banana', 'orange'];
   fruits[1] = 'grape'; // Modify an element
   fruits.push('kiwi'); // Add an element to the end
   fruits.pop(); // Remove the last element
   ```

5. **Contiguous Memory Allocation(?):**

    In JavaScript, arrays are not guaranteed to have contiguous memory allocation like arrays in some low-level languages such as C. JavaScript arrays are implemented as objects, and their elements are stored in a way that allows for efficient random access but doesn't necessarily involve contiguous memory locations.

    JavaScript arrays are dynamic and can grow or shrink in size dynamically. This dynamic nature means that the underlying memory representation may change during the lifetime of the array. Elements in a JavaScript array can be sparse, meaning there may be "holes" (undefined values) between elements, and they do not necessarily occupy contiguous memory locations.

    For example:

    ```javascript
    let myArray = [];
    myArray[0] = 'first';
    myArray[2] = 'third';
    console.log(myArray); // Output: [ 'first', <1 empty item>, 'third' ]
    ```

    In this example, `myArray` is sparse because there is an empty slot between the first and third elements. This sparse structure allows for flexibility in managing arrays but does not guarantee contiguous memory allocation.

    If you need a data structure with contiguous memory allocation, you might need to use typed arrays (`Int8Array`, `Float64Array`, etc.) in JavaScript, which are part of the ECMAScript standard. Typed arrays provide a way to work with raw binary data in a contiguous block of memory. However, they have some limitations compared to regular arrays, as they are more specialized and have a fixed size and type for their elements.

6. **Methods:**
   Arrays come with a variety of built-in methods for performing common operations. Some commonly used array methods include `push`, `pop`, `shift`, `unshift`, `splice`, `slice`, `indexOf`, `forEach`, and more.

   ```javascript
   let numbers = [1, 2, 3, 4, 5];
   numbers.push(6); // Add 6 to the end
   numbers.pop(); // Remove the last element
   numbers.unshift(0); // Add 0 to the beginning
   numbers.shift(); // Remove the first element
   ```

7. **Nested Arrays:**
   Arrays can contain other arrays, allowing you to create nested or multidimensional structures.

   ```javascript
   let matrix = [
     [1, 2, 3],
     [4, 5, 6],
     [7, 8, 9]
   ];
   console.log(matrix[1][2]); // Access element at row 1, column 2 (Output: 6)
   ```

Arrays are versatile and widely used in JavaScript for various tasks, such as storing lists of items, representing matrices, implementing stacks and queues, and more. Understanding how to work with arrays is fundamental to effective JavaScript programming.

## `Linked List`
A linked list is a linear data structure in which elements are stored in nodes, and each node points to the next node in the sequence. Unlike arrays, linked lists do not require contiguous memory locations, and they can easily grow or shrink in size. Each node in a linked list consists of two components: data and a reference (or link) to the next node in the sequence. The last node in the list typically points to a null reference, indicating the end of the list.

In the context of JavaScript, you can implement a linked list using objects and references. Here's a basic explanation of linked lists and their implementation in JavaScript:

### Types of Linked Lists:

1. **Singly Linked List:**
   - In a singly linked list, each node contains data and a reference to the next node.
   - Traversing the list is straightforward, but going backward requires traversing the list from the beginning.
   - The last node's reference is null, indicating the end of the list.

   ```javascript
   class Node {
     constructor(data) {
       this.data = data;
       this.next = null;
     }
   }

   class SinglyLinkedList {
     constructor() {
       this.head = null;
     }

     // Methods to add, remove, and traverse nodes can be implemented here
   }
   ```

2. **Doubly Linked List:**
   - In a doubly linked list, each node contains data, a reference to the next node, and a reference to the previous node.
   - This allows for easier traversal in both directions but requires more memory.

   ```javascript
   class DoublyNode {
     constructor(data) {
       this.data = data;
       this.next = null;
       this.prev = null;
     }
   }

   class DoublyLinkedList {
     constructor() {
       this.head = null;
       this.tail = null;
     }

     // Methods to add, remove, and traverse nodes can be implemented here
   }
   ```

### Basic Operations on Linked Lists:

1. **Insertion:**
   - Adding a node to the linked list involves updating the references of the current node and the new node.

   ```javascript
   // Inserting at the end of a singly linked list
   function appendToLinkedList(linkedList, data) {
     const newNode = new Node(data);

     if (!linkedList.head) {
       linkedList.head = newNode;
     } else {
       let current = linkedList.head;
       while (current.next) {
         current = current.next;
       }
       current.next = newNode;
     }
   }
   ```

2. **Deletion:**
   - Removing a node involves updating the references of the previous and next nodes.

   ```javascript
   // Deleting a node from a doubly linked list
   function deleteNodeFromDoublyLinkedList(linkedList, node) {
     if (node.prev) {
       node.prev.next = node.next;
     } else {
       linkedList.head = node.next;
     }

     if (node.next) {
       node.next.prev = node.prev;
     }
   }
   ```

3. **Traversal:**
   - Traversing a linked list involves moving from one node to the next until the end is reached.

   ```javascript
   // Traversing a singly linked list
   function printLinkedList(linkedList) {
     let current = linkedList.head;
     while (current) {
       console.log(current.data);
       current = current.next;
     }
   }
   ```

Linked lists are useful in scenarios where dynamic memory allocation is preferred, and frequent insertions and deletions are expected. In JavaScript, while arrays are more commonly used, understanding linked lists can provide insights into different data structures and their trade-offs.

### JS Array vs Linked List
JavaScript arrays are dynamic and offer methods like `push`, `pop`, `shift`, and `unshift` that allow for efficient addition and removal of elements. These methods make arrays quite versatile and suitable for many use cases. In many scenarios, arrays in JavaScript are more convenient and performant than linked lists.

However, there are specific cases where a linked list might be more appropriate or offer advantages:

1. **Insertion and Deletion in the Middle:**
   - Linked lists can be more efficient than arrays when it comes to inserting or deleting elements in the middle of the list. This is because updating the references of neighboring nodes is often faster than shifting elements in an array.

2. **Dynamic Memory Allocation:**
   - Linked lists don't require contiguous memory allocation, making them suitable for situations where memory is allocated and deallocated frequently. This can be beneficial in environments where memory management is a critical concern.

3. **No Preallocation:**
   - Arrays in JavaScript are implemented as objects and have some overhead due to their dynamic nature. In contrast, linked lists don't require preallocation, and nodes can be created and linked together as needed.

4. **Learning and Understanding:**
   - Understanding how linked lists work can be beneficial for learning about fundamental data structures. It can help programmers grasp concepts like pointers, references, and dynamic memory management.

5. **Specific Algorithms:**
   - Some algorithms and data structures, especially in computer science education, are traditionally explained or implemented using linked lists. Familiarity with linked lists can make it easier to understand certain algorithms and their implementations.

It's important to note that in many practical scenarios, JavaScript arrays are sufficient and preferred due to their simplicity, ease of use, and performance characteristics. Linked lists are just one tool in the broader toolbox of data structures, and their use depends on the specific requirements of a given problem. For most everyday tasks, JavaScript arrays are likely the more appropriate choice.

## `Stack`
A stack is a fundamental data structure that follows the Last In, First Out (LIFO) principle. This means that the last element added to the stack is the first one to be removed. Think of it as a stack of plates: you add a plate to the top, and the plate you added last is the first one you pick up.

In JavaScript, we can implement a stack using an array or a linked list. Here, I'll provide an explanation of the stack data structure and show how it can be implemented using an array in JavaScript.

### Stack Operations:

1. **Push:**
   - Adds an element to the top of the stack.

   ```javascript
   // Using an array to implement a stack
   let stack = [];

   stack.push(1);
   stack.push(2);
   stack.push(3);

   console.log(stack); // Output: [1, 2, 3]
   ```

2. **Pop:**
   - Removes the element from the top of the stack.

   ```javascript
   let topElement = stack.pop();
   console.log(topElement); // Output: 3
   console.log(stack); // Output: [1, 2]
   ```

3. **Peek (or Top):**
   - Returns the element at the top of the stack without removing it.

   ```javascript
   let topElement = stack[stack.length - 1];
   console.log(topElement); // Output: 2
   ```

### Implementation using an Array:

```javascript
class Stack {
  constructor() {
    this.items = [];
  }

  push(element) {
    this.items.push(element);
  }

  pop() {
    if (this.isEmpty()) {
      return null;
    }
    return this.items.pop();
  }

  peek() {
    return this.isEmpty() ? null : this.items[this.items.length - 1];
  }

  isEmpty() {
    return this.items.length === 0;
  }

  size() {
    return this.items.length;
  }

  clear() {
    this.items = [];
  }
}
```

### Usage:

```javascript
let myStack = new Stack();

myStack.push(1);
myStack.push(2);
myStack.push(3);

console.log(myStack.peek()); // Output: 3
console.log(myStack.pop()); // Output: 3
console.log(myStack.size()); // Output: 2
console.log(myStack.isEmpty()); // Output: false

myStack.clear();
console.log(myStack.isEmpty()); // Output: true
```

### Use Cases:

1. **Function Calls:**
   - JavaScript uses a call stack to manage function calls. Each time a function is called, a new frame is added to the stack, and when the function completes, its frame is removed.

2. **Undo Mechanisms:**
   - Undo functionality in applications is often implemented using a stack. Each action is pushed onto the stack, and undoing an action involves popping the top element.

3. **Expression Evaluation:**
   - In certain algorithms, stacks are used to evaluate expressions, such as converting infix expressions to postfix or prefix form.

Stacks are a versatile data structure with various applications. The array-based implementation provided here is simple and suitable for many use cases in JavaScript.

## `Queue`
A queue is a fundamental data structure that follows the First In, First Out (FIFO) principle. In a queue, the first element added is the first one to be removed. Think of it like a line of people waiting for a bus: the person who arrived first is the first one to board the bus.

In JavaScript, you can implement a queue using an array or a linked list. I'll provide an explanation of the queue data structure and show how it can be implemented using an array in JavaScript.

### Queue Operations:

1. **Enqueue:**
   - Adds an element to the back of the queue.

   ```javascript
   // Using an array to implement a queue
   let queue = [];

   queue.push(1);
   queue.push(2);
   queue.push(3);

   console.log(queue); // Output: [1, 2, 3]
   ```

2. **Dequeue:**
   - Removes the element from the front of the queue.

   ```javascript
   let frontElement = queue.shift();
   console.log(frontElement); // Output: 1
   console.log(queue); // Output: [2, 3]
   ```

3. **Front:**
   - Returns the element at the front of the queue without removing it.

   ```javascript
   let frontElement = queue[0];
   console.log(frontElement); // Output: 2
   ```

### Implementation using an Array:

```javascript
class Queue {
  constructor() {
    this.items = [];
  }

  enqueue(element) {
    this.items.push(element);
  }

  dequeue() {
    if (this.isEmpty()) {
      return null;
    }
    return this.items.shift();
  }

  front() {
    return this.isEmpty() ? null : this.items[0];
  }

  isEmpty() {
    return this.items.length === 0;
  }

  size() {
    return this.items.length;
  }

  clear() {
    this.items = [];
  }
}
```

### Usage:

```javascript
let myQueue = new Queue();

myQueue.enqueue(1);
myQueue.enqueue(2);
myQueue.enqueue(3);

console.log(myQueue.front()); // Output: 1
console.log(myQueue.dequeue()); // Output: 1
console.log(myQueue.size()); // Output: 2
console.log(myQueue.isEmpty()); // Output: false

myQueue.clear();
console.log(myQueue.isEmpty()); // Output: true
```

### Use Cases:

1. **Breadth-First Search (BFS):**
   - Queues are commonly used in algorithms like BFS, where you explore all the neighbors of a node before moving on to the next level.

2. **Task Scheduling:**
   - Queues are useful for managing tasks in a first-come-first-served manner, such as processing jobs in a print queue, or the event queue in the context of web development.

3. **Messaging Systems:**
   - Queues can be used in messaging systems, where messages are added to the back of the queue and processed in the order they are received.

Queues are a versatile data structure with various applications. The array-based implementation provided here is simple and suitable for many use cases in JavaScript. If performance considerations are crucial, a linked list implementation might be more efficient for certain scenarios.

## `Hash Table`
A hash table is a data structure that allows for efficient insertion, deletion, and retrieval of values based on a key. It uses a hash function to map keys to indices in an array, allowing for constant-time average-case complexity for basic operations. Hash tables are widely used in computer science and programming due to their fast and efficient nature.

### Basic Components of a Hash Table:

1. **Hash Function:**
   - A hash function takes a key and produces a hash code, which is used as an index to store and retrieve the associated value. The goal is to distribute keys uniformly across the array.

2. **Array:**
   - The underlying data structure used to store key-value pairs. Each index in the array is often referred to as a "bucket."

### Hash Table Operations:

1. **Insert (or Set):**
   - The key and its associated value are hashed, and the value is stored in the corresponding bucket.

2. **Retrieve (or Get):**
   - The key is hashed, and the corresponding bucket is checked to retrieve the associated value.

3. **Delete:**
   - The key is hashed, and the value associated with that key is removed from the hash table.

### Collision Handling:

A collision occurs when two keys hash to the same index. Various techniques are used to handle collisions:

1. **Separate Chaining:**
   - Each bucket in the array contains a linked list or another data structure to handle multiple values that hash to the same index.

2. **Open Addressing:**
   - When a collision occurs, the algorithm searches for the next available slot in the array (probing). This can be done using techniques like linear probing, quadratic probing, or double hashing.

### Implementation in JavaScript:

Here's a basic example of a hash table implementation in JavaScript using separate chaining:

```javascript
class HashTable {
  constructor(size = 100) {
    this.size = size;
    this.buckets = new Array(size).fill(null).map(() => []);
  }

  hash(key) {
    let hash = 0;
    for (let i = 0; i < key.length; i++) {
      hash += key.charCodeAt(i);
    }
    return hash % this.size;
  }

  set(key, value) {
    const index = this.hash(key);
    const bucket = this.buckets[index];

    for (const pair of bucket) {
      if (pair[0] === key) {
        // Update value if key already exists
        pair[1] = value;
        return;
      }
    }

    // Insert a new key-value pair
    bucket.push([key, value]);
  }

  get(key) {
    const index = this.hash(key);
    const bucket = this.buckets[index];

    for (const pair of bucket) {
      if (pair[0] === key) {
        return pair[1];
      }
    }

    return null; // Key not found
  }

  delete(key) {
    const index = this.hash(key);
    const bucket = this.buckets[index];

    for (let i = 0; i < bucket.length; i++) {
      if (bucket[i][0] === key) {
        // Remove key-value pair from the bucket
        bucket.splice(i, 1);
        return;
      }
    }
  }
}
```

### Usage:

```javascript
let myHashTable = new HashTable();

myHashTable.set('name', 'John');
myHashTable.set('age', 25);
myHashTable.set('city', 'New York');

console.log(myHashTable.get('name')); // Output: John
console.log(myHashTable.get('age'));  // Output: 25

myHashTable.delete('age');
console.log(myHashTable.get('age'));  // Output: null (key not found)
```

Hash tables are commonly used in JavaScript for various purposes, including implementing object maps and sets, managing caches, and optimizing search and retrieval operations in applications. The native JavaScript `Map` and `Set` objects are examples of hash table implementations provided by the language.

### JS `Map` and `Set` objects
The `Map` and `Set` objects are native data structures introduced in ECMAScript 2015 (ES6) and later versions of JavaScript. They provide efficient ways to manage collections of values and keys, and under the hood, they are implemented using hash tables or similar structures.

### `Map` Object:

#### Usage:
```javascript
// Creating a Map
let myMap = new Map();

// Adding key-value pairs
myMap.set('name', 'John');
myMap.set('age', 25);

// Retrieving values
console.log(myMap.get('name')); // Output: John

// Checking if a key exists
console.log(myMap.has('age'));   // Output: true

// Deleting a key-value pair
myMap.delete('age');

// Iterating over key-value pairs
for (let [key, value] of myMap) {
  console.log(`${key}: ${value}`);
}
```

#### Key Features:
- **Any Data Type as Key:**
  - Unlike plain objects, `Map` allows you to use any data type (including objects and functions) as keys.

- **Order of Insertion Preserved:**
  - The order of key-value pairs is preserved, making it suitable for scenarios where the order of insertion matters.

- **Size Property:**
  - You can easily get the size of the `Map` using the `size` property.

### `Set` Object:

#### Usage:
```javascript
// Creating a Set
let mySet = new Set();

// Adding values
mySet.add(1);
mySet.add('apple');

// Checking if a value exists
console.log(mySet.has(1));       // Output: true

// Deleting a value
mySet.delete('apple');

// Iterating over values
for (let value of mySet) {
  console.log(value);
}
```

#### Key Features:
- **Uniqueness:**
  - A `Set` only allows unique values, making it useful for scenarios where you want to ensure a collection of distinct elements.

- **No Key-Value Pairs:**
  - Unlike `Map`, `Set` does not store key-value pairs; it only stores values.

- **Size Property:**
  - Similar to `Map`, you can get the size of the `Set` using the `size` property.

### Commonalities:

- Both `Map` and `Set` offer methods to clear all entries (`clear()`), check if they are empty (`size === 0`), and provide iterable methods (`forEach`, `entries`, `keys`, `values`).

- Both `Map` and `Set` are iterable, allowing you to use them with `for...of` loops.

- `Map` and `Set` objects are part of the ECMAScript standard, and they are widely supported in modern JavaScript environments.

In summary, `Map` is suitable for scenarios where you need to associate keys with values, while `Set` is useful when you want to maintain a collection of unique values. Their efficient implementations make them go-to choices for various tasks in JavaScript development.

## `Graph`
A graph is a collection of nodes (or vertices) and edges that connect pairs of nodes. Graphs are a versatile data structure used to model relationships between entities. In JavaScript, graphs can be implemented using various approaches, and there are different types of graphs, each with its characteristics.

### Basic Components of a Graph:

1. **Node (Vertex):**
   - Represents an entity in the graph. In a social network graph, nodes could be users, and in a network topology graph, nodes could be devices.

2. **Edge:**
   - Represents a relationship between two nodes. Edges may have a direction (directed graph) or not (undirected graph).

3. **Weight:**
   - An optional value assigned to edges to represent a quantitative measure (e.g., distance, cost).

### Types of Graphs:

1. **Undirected Graph:**
   - Edges have no direction, meaning the connection between nodes is bidirectional.

2. **Directed Graph (Digraph):**
   - Edges have a direction, indicating a one-way relationship from one node to another.

3. **Weighted Graph:**
   - Edges have weights or costs associated with them.

4. **Unweighted Graph:**
   - Edges have no weights; all edges are considered equal.

5. **Cyclic Graph:**
   - Contains at least one cycle (a closed path of edges with no repeated nodes).

6. **Acyclic Graph:**
   - Has no cycles.

### Graph Representation:

1. **Adjacency Matrix:**
   - A two-dimensional array where the presence or absence of an edge between nodes is indicated by a 1 or 0. Weighted edges can be represented by storing weights in the matrix.

   ```javascript
   // Example adjacency matrix for an undirected graph
   const adjacencyMatrix = [
     [0, 1, 1, 0],
     [1, 0, 1, 1],
     [1, 1, 0, 0],
     [0, 1, 0, 0]
   ];
   ```

2. **Adjacency List:**
   - Each node maintains a list of its neighbors. This is often implemented using an object or a Map in JavaScript.

   ```javascript
   // Example adjacency list for an undirected graph
   const adjacencyList = {
     0: [1, 2],
     1: [0, 2, 3],
     2: [0, 1],
     3: [1]
   };
   ```

### Graph Operations:

1. **Add Node:**
   - Adds a new node to the graph.

2. **Add Edge:**
   - Connects two nodes by adding an edge between them. For weighted graphs, the weight is specified.

3. **Remove Node:**
   - Removes a node and its associated edges from the graph.

4. **Remove Edge:**
   - Removes the edge between two nodes.

5. **Traversal:**
   - Visiting all nodes in the graph, often performed using Depth-First Search (DFS) or Breadth-First Search (BFS).

### Implementation in JavaScript:

Here's a basic example of an adjacency list representation for an undirected graph in JavaScript:

```javascript
class Graph {
  constructor() {
    this.adjacencyList = {};
  }

  addNode(node) {
    if (!this.adjacencyList[node]) {
      this.adjacencyList[node] = [];
    }
  }

  addEdge(node1, node2) {
    this.adjacencyList[node1].push(node2);
    this.adjacencyList[node2].push(node1);
  }

  removeNode(node) {
    delete this.adjacencyList[node];
    for (let adjacentNode in this.adjacencyList) {
      this.adjacencyList[adjacentNode] = this.adjacencyList[adjacentNode].filter(adjNode => adjNode !== node);
    }
  }

  removeEdge(node1, node2) {
    this.adjacencyList[node1] = this.adjacencyList[node1].filter(adjNode => adjNode !== node2);
    this.adjacencyList[node2] = this.adjacencyList[node2].filter(adjNode => adjNode !== node1);
  }
}
```

### Usage:

```javascript
let myGraph = new Graph();

myGraph.addNode(0);
myGraph.addNode(1);
myGraph.addNode(2);

myGraph.addEdge(0, 1);
myGraph.addEdge(1, 2);

console.log(myGraph.adjacencyList);
/*
{
  0: [1],
  1: [0, 2],
  2: [1]
}
*/
```

Graphs are a fundamental data structure with diverse applications, including network routing, social network analysis, recommendation systems, and more. In JavaScript, understanding and implementing graphs can be essential for solving problems in various domains.

## `Binary Search Tree`
A Binary Search Tree (BST) is a binary tree data structure with the following properties:

1. Each node in the tree has at most two children, commonly referred to as the left child and the right child.
2. For each node, all nodes in its left subtree have values less than the node's value, and all nodes in its right subtree have values greater than the node's value.
3. The left and right subtrees are also Binary Search Trees.

These properties ensure that a binary search tree allows for efficient search, insertion, and deletion operations.

### Binary Search Tree Operations:

1. **Search:**
   - Starting from the root, compare the target value with the current node's value.
   - If the target is less, go to the left subtree; if greater, go to the right subtree.
   - Repeat until finding the target or reaching a leaf node.

2. **Insertion:**
   - Search for the correct position to insert the new node.
   - Once the correct position is found (where a leaf node should be), insert the new node.

3. **Deletion:**
   - Three cases:
     - Node has no children: Simply remove the node.
     - Node has one child: Replace the node with its child.
     - Node has two children: Find the node's in-order successor (or predecessor), replace the node's value with the successor's value, and then recursively delete the successor.

### Implementation in JavaScript:
Here's a basic example of a Binary Search Tree in JavaScript:

```javascript
class TreeNode {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}

class BinarySearchTree {
  constructor() {
    this.root = null;
  }

  insert(value) {
    const newNode = new TreeNode(value);

    if (!this.root) {
      this.root = newNode;
    } else {
      this._insertRecursive(this.root, newNode);
    }
  }

  _insertRecursive(node, newNode) {
    if (newNode.value < node.value) {
      if (!node.left) {
        node.left = newNode;
      } else {
        this._insertRecursive(node.left, newNode);
      }
    } else {
      if (!node.right) {
        node.right = newNode;
      } else {
        this._insertRecursive(node.right, newNode);
      }
    }
  }

  search(value) {
    return this._searchRecursive(this.root, value);
  }

  _searchRecursive(node, target) {
    if (!node || node.value === target) {
      return node;
    }

    if (target < node.value) {
      return this._searchRecursive(node.left, target);
    } else {
      return this._searchRecursive(node.right, target);
    }
  }

  delete(value) {
    this.root = this._deleteRecursive(this.root, value);
  }

  _deleteRecursive(node, target) {
    if (!node) {
      return null;
    }

    if (target < node.value) {
      node.left = this._deleteRecursive(node.left, target);
    } else if (target > node.value) {
      node.right = this._deleteRecursive(node.right, target);
    } else {
      // Node to be deleted found

      // Case 1: Node has no children
      if (!node.left && !node.right) {
        return null;
      }

      // Case 2: Node has one child
      if (!node.left) {
        return node.right;
      } else if (!node.right) {
        return node.left;
      }

      // Case 3: Node has two children
      const successor = this._findMin(node.right);
      node.value = successor.value;
      node.right = this._deleteRecursive(node.right, successor.value);
    }

    return node;
  }

  _findMin(node) {
    while (node.left) {
      node = node.left;
    }
    return node;
  }
}
```

### Usage:

```javascript
let myBST = new BinarySearchTree();

myBST.insert(10);
myBST.insert(5);
myBST.insert(15);
myBST.insert(3);
myBST.insert(7);
myBST.insert(12);
myBST.insert(18);

console.log(myBST.search(7)); // Output: TreeNode { value: 7, left: null, right: null }

myBST.delete(15);
console.log(myBST.search(15)); // Output: null (not found)
```

Binary Search Trees are powerful data structures that provide efficient search, insertion, and deletion operations. In JavaScript, understanding and implementing BSTs can be useful for solving problems related to sorting, searching, and maintaining ordered data.

## `Trie`
A Trie (derived from retrieval), also known as a digital tree or prefix tree, is a tree-like data structure used for storing a dynamic set of strings where the keys are usually sequences, such as words in a dictionary or phone numbers. The structure of a trie allows for efficient searches and insertions of strings, making it especially useful for tasks like autocomplete functionality.

### Basic Components of a Trie:

1. **Node:**
   - Each node in a trie represents a character in a string.
   - Nodes may have links to other nodes, representing the next character in the string.

2. **Root:**
   - The topmost node in the trie, representing an empty string or the common prefix of all strings.

3. **Edges:**
   - Directed edges between nodes represent characters, forming the paths from the root to a particular string.

4. **Leaf Node:**
   - A node without outgoing edges, marking the end of a string.

### Trie Operations:

1. **Insertion:**
   - To insert a string into a trie, start from the root and traverse the tree, creating nodes for each character in the string.

2. **Search:**
   - To search for a string in a trie, start from the root and follow the edges corresponding to each character in the string. If the path exists, the string is present.

3. **Deletion:**
   - To delete a string from a trie, traverse the tree to find the string and remove the leaf node representing the end of the string. If this leaf node has no other children, remove the parent node as well.

### Implementation in JavaScript:

Here's a basic example of a Trie implementation in JavaScript:

```javascript
class TrieNode {
  constructor() {
    this.children = {};
    this.isEndOfWord = false;
  }
}

class Trie {
  constructor() {
    this.root = new TrieNode();
  }

  insert(word) {
    let node = this.root;

    for (let char of word) {
      if (!node.children[char]) {
        node.children[char] = new TrieNode();
      }
      node = node.children[char];
    }

    node.isEndOfWord = true;
  }

  search(word) {
    let node = this.root;

    for (let char of word) {
      if (!node.children[char]) {
        return false;
      }
      node = node.children[char];
    }

    return node.isEndOfWord;
  }

  startsWith(prefix) {
    let node = this.root;

    for (let char of prefix) {
      if (!node.children[char]) {
        return false;
      }
      node = node.children[char];
    }

    return true;
  }
}
```

### Usage:

```javascript
let myTrie = new Trie();

myTrie.insert("apple");
myTrie.insert("app");
myTrie.insert("banana");

console.log(myTrie.search("apple")); // Output: true
console.log(myTrie.search("apples")); // Output: false
console.log(myTrie.startsWith("ban")); // Output: true
```

### Use Cases:

1. **Autocomplete Suggestions:**
   - Tries are commonly used in autocomplete functionality, where the trie structure allows for efficient prefix matching.

2. **Spell Checking:**
   - Tries are useful for spell-checking algorithms, as they can quickly determine if a given word is in the dictionary.

3. **IP Routing:**
   - In computer networking, tries can be used in IP routers for efficient IP address matching.

4. **Symbol Tables in Compilers:**
   - Tries can be used in compilers to efficiently store and retrieve symbols.

While tries can be memory-intensive due to their structure, they offer fast and predictable lookup times, especially for scenarios involving string data. In JavaScript, understanding and implementing tries can be valuable for applications requiring efficient string-based operations.

## `Heap`
A Heap is a special Tree-based Data Structure in which the tree is a complete binary tree. A complete binary tree means all levels of the tree are fully filled except possibly for the last level, which is filled from left to right.

Generally, heaps are of two types.

**Max-Heap:**<br> 
In this heap, the value of the root node must be the greatest among all its child nodes and the same thing must be done for its left and right sub-tree also.

**Min-Heap:**<br>
In this heap, the value of the root node must be the smallest among all its child nodes and the same thing must be done for its left and right sub-tree also.

### Properties of Heap:
Heap has the following Properties:

+ **Complete Binary Tree:** A heap tree is a complete binary tree, meaning all levels of the tree are fully filled except possibly the last level, which is filled from left to right. This property ensures that the tree is efficiently represented using an array.

+ **Heap Property:** This property ensures that the minimum (or maximum) element is always at the root of the tree according to the heap type.

+ **Parent-Child Relationship:** The relationship between a parent node at index ‘i’ and its children is given by the formulas: left child at index 2i+1 and right child at index 2i+2 for 0-based indexing of node numbers.

+ **Efficient Insertion and Removal:** Insertion and removal operations in heap trees are efficient. New elements are inserted at the next available position in the bottom-rightmost level, and the heap property is restored by comparing the element with its parent and swapping if necessary. Removal of the root element involves replacing it with the last element and heapifying down.

+ **Efficient Access to Extremal Elements:** The minimum or maximum element is always at the root of the heap, allowing constant-time access.

### Operations Supported by Heap:

**Heapify:**<br>
It is the process to rearrange the elements to maintain the property of heap data structure. It is done when a certain node creates an imbalance in the heap due to some operations on that node. It takes O(log N) to balance the tree. 

+ For max-heap, it balances in such a way that the maximum element is the root of that binary tree and 
+ For min-heap, it balances in such a way that the minimum element is the root of that binary tree.

**Insertion:**<br>
If we insert a new element into the heap since we are adding a new element into the heap so it will distort the properties of the heap so we need to perform the heapify operation so that it maintains the property of the heap.
This operation also takes O(logN) time.

**Deletion:**<br>
If we delete the element from the heap it always deletes the root element of the tree and replaces it with the last element of the tree.
Since we delete the root element from the heap it will distort the properties of the heap so we need to perform heapify operations so that it maintains the property of the heap. 
It takes O(logN) time.

**getMax (For max-heap) or getMin (For min-heap):**<br>
It finds the maximum element or minimum element for max-heap and min-heap respectively and as we know minimum and maximum elements will always be the root node itself for min-heap and max-heap respectively. It takes O(1) time.

### Application:
**Priority Queues:** Priority queues can be efficiently implemented using Binary Heap because it supports insert(), delete() and extractmax(), decreaseKey() operations in O(log N) time. (A priority queue is a type of queue that arranges elements based on their priority values. Elements with higher priority values are typically retrieved before elements with lower priority values.)

**Order statistics:** The Heap data structure can be used to efficiently find the kth smallest (or largest) element in an array.

### Advantages of Heaps:
+ Fast access to maximum/minimum element (O(1))
+ Efficient Insertion and Deletion operations (O(log n))
+ Flexible size

### Disadvantages of Heaps:
+ Not suitable for searching for an element other than maximum/minimum (O(n) in worst case)
+ Extra memory overhead to maintain heap structure
+ Slower than other data structures like arrays and linked lists for non-priority queue operations.

## `Matrix (2D Array)`
A matrix is a two-dimensional data structure that consists of a collection of elements arranged in rows and columns. Each element in the matrix can be accessed using its row and column indices. Matrices find applications in various fields, such as mathematics, computer graphics, image processing, and scientific computing.

### Basic Concepts of a Matrix:

1. **Rows and Columns:**
   - A matrix has a specified number of rows and columns, denoted by `m x n`, where `m` is the number of rows, and `n` is the number of columns.

2. **Element:**
   - Each entry in a matrix is called an element. The location of an element is specified by its row and column indices.

3. **Dimensions:**
   - The dimensions of a matrix are given by the number of rows and columns. For example, a matrix with `m` rows and `n` columns is referred to as an "m x n" matrix.

### Representation in JavaScript:

In JavaScript, you can represent a matrix using arrays, nested arrays, or arrays of arrays. Each sub-array represents a row of the matrix, and the elements within the sub-array represent the columns.

```javascript
// Example: 3x3 matrix
const matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];
```

### Operations on Matrices:

1. **Matrix Addition:**
   - Add corresponding elements of two matrices to create a new matrix.

   ```javascript
   // Example: Matrix Addition
   const matrixA = [[1, 2], [3, 4]];
   const matrixB = [[5, 6], [7, 8]];

   const resultMatrix = [
     [matrixA[0][0] + matrixB[0][0], matrixA[0][1] + matrixB[0][1]],
     [matrixA[1][0] + matrixB[1][0], matrixA[1][1] + matrixB[1][1]]
   ];
   ```

2. **Matrix Multiplication:**
   - Multiply corresponding elements and sum the products to create a new matrix.

   ```javascript
   // Example: Matrix Multiplication
   const matrixC = [[2, 3], [4, 5]];
   const matrixD = [[1, 2], [3, 4]];

   const resultMatrix = [
     [(2 * 1 + 3 * 3), (2 * 2 + 3 * 4)],
     [(4 * 1 + 5 * 3), (4 * 2 + 5 * 4)]
   ];
   ```

3. **Transpose:**
   - Swap the rows and columns of a matrix.

   ```javascript
   // Example: Transpose
   const originalMatrix = [[1, 2, 3], [4, 5, 6]];

   const transposedMatrix = [
     [originalMatrix[0][0], originalMatrix[1][0]],
     [originalMatrix[0][1], originalMatrix[1][1]],
     [originalMatrix[0][2], originalMatrix[1][2]]
   ];
   ```

4. **Determinant:**
   - A scalar value that can be computed for square matrices.

   ```javascript
   // Example: Determinant
   const squareMatrix = [[1, 2], [3, 4]];

   const determinant = squareMatrix[0][0] * squareMatrix[1][1] - squareMatrix[0][1] * squareMatrix[1][0];
   ```

### Libraries for Matrix Operations in JavaScript:

There are libraries in JavaScript that provide functionalities for matrix operations, making it easier to perform complex mathematical computations. Some popular ones include:

- **NumPy.js:** A JavaScript library for numerical computing that includes support for matrices and arrays.
- **Math.js:** A comprehensive mathematics library that includes matrix operations among its features.

Matrices are versatile structures used in various mathematical and computational applications. In JavaScript, manipulating matrices is often done using nested arrays, and for more advanced operations, external libraries may be employed.

---
### Knowledge Check
**Q1.** What is the difference between a stack and a queue?

**A1.** A stack is a fundamental data structure that follows the Last In, First Out (LIFO) principle. This means that the last element added to the stack is the first one to be removed. Think of it as a stack of plates: you add a plate to the top, and the plate you added last is the first one you pick up.

A queue is a fundamental data structure that follows the First In, First Out (FIFO) principle. In a queue, the first element added is the first one to be removed. Think of it like a line of people waiting for a bus: the person who arrived first is the first one to board the bus.

**Q2.** What are the enqueue and dequeue properties?

**A2.** Queue Operations:

1. **Enqueue:**
   - Adds an element to the back of the queue.

   ```javascript
   // Using an array to implement a queue
   let queue = [];

   queue.push(1);
   queue.push(2);
   queue.push(3);

   console.log(queue); // Output: [1, 2, 3]
   ```

2. **Dequeue:**
   - Removes the element from the front of the queue.

   ```javascript
   let frontElement = queue.shift();
   console.log(frontElement); // Output: 1
   console.log(queue); // Output: [2, 3]
   ```

**Q3.** What is a linked list? What is a node?

**A3.** A linked list is a linear data structure in which elements are stored in nodes, and each node points to the next node in the sequence. Unlike arrays, linked lists do not require contiguous memory locations, and they can easily grow or shrink in size. Each node in a linked list consists of two components: data and a reference (or link) to the next node in the sequence. The last node in the list typically points to a null reference, indicating the end of the list.

**Q4.** Which recursive problem-solving method/algorithm design principle does binary search implement?

**A4.** Binary search algorithm is a "divide and conquer" algorithm. A divide and conquer algorithm is built on the principle of dividing the problem into more managable, smaller parts, usually with recursion, and continuing this process until the problem is solved.

Binary search is a highly efficient searching algorithm that finds the position of a target value within a sorted array or list. The key idea behind binary search is to divide the array into two halves at each step and eliminate half of the remaining elements based on the comparison with the target value. This process continues until the target value is found or the search space is reduced to zero.

**Q5.** What abstract data type would you use to defer/store nodes in a breadth-first tree traversal?

**A5.** In breadth-first tree traversal, to store references to nodes we could employ a queue. Breadth-first traversal visits all the nodes at the current depth level before moving on to the nodes at the next level. A queue follows the First In, First Out (FIFO) principle, which aligns well with the breadth-first traversal order.

Here's a simple explanation of how a queue would be used in the context of a breadth-first tree traversal:

1. Enqueue the root node of the tree.
2. While the queue is not empty:
   - Dequeue a node from the front of the queue.
   - Process the dequeued node (e.g., visit it, perform some operation).
   - Enqueue all the children of the dequeued node.

By using a queue, you ensure that nodes are processed in the order in which they were discovered at each level of the tree. This helps you achieve the breadth-first traversal behavior.

**Q6.** What abstract data type would you use to defer/store nodes in a depth-first tree traversal?

**A6.** For storing references nodes during a depth-first tree traversal, we would typically use a stack abstract data type. Depth-first traversal explores as far as possible along one branch before backtracking, and a stack follows the Last In, First Out (LIFO) principle, making it suitable for this traversal order.

Here's a simple explanation of how a stack would be used in the context of a depth-first tree traversal:

1. Push the root node of the tree onto the stack.
2. While the stack is not empty:
   - Pop a node from the top of the stack.
   - Process the popped node (e.g., visit it, perform some operation).
   - Push all the children of the popped node onto the stack.

By using a stack, you ensure that the traversal goes as deep as possible along each branch before backtracking to explore other branches. This is consistent with the depth-first traversal behavior.