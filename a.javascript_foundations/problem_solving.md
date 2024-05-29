# Problem Solving

## The Steps in the Problem Solving Process
### Understand the problem
The first step to solving a problem is understanding exactly what the problem is. If you don’t understand the problem, you won’t know when you’ve successfully solved it and may waste a lot of time on a wrong solution.

To gain clarity and understanding of the problem, write it down on paper, reword it in plain English until it makes sense to you, and draw diagrams if that helps. When you can explain the problem to someone else in plain English, you understand it.

### Plan
Now that you know what you’re aiming to solve, don’t jump into coding just yet. It’s time to plan out how you’re going to solve it first. Some of the questions you should answer at this stage of the process:

+ Does your program have a user interface? What will it look like? What functionality will the interface have? Sketch this out on paper.
+ What inputs will your program have? Will the user enter data or will you get input from somewhere else?
+ What’s the desired output?
+ Given your inputs, what are the steps necessary to return the desired output? (Define the steps of the solution in pseudocode.)

The last question is where you will write out an algorithm to solve the problem. You can think of an algorithm as a recipe for solving a particular problem. It defines the steps that need to be taken by the computer to solve a problem.

### Pseudocode
Pseudocode is writing out the logic for your program in natural language instead of code. It helps you slow down and think through the steps your program will have to go through to solve the problem.

Here’s an example of what the pseudocode for a simple program that prints all numbers up to an inputted number might look like:

```
When the user inputs a number
Initialize a counter variable and set its value to zero
While counter is smaller than user inputted number increment the counter by one
Print the value of the counter variable
```

### Divide and conquer (implement)
From your planning, you should have identified some subproblems of the big problem you’re solving. Each of the steps in the algorithm we wrote out in the last section are subproblems. Pick the smallest or simplest one and start there with coding.

It’s important to remember that you might not know all the steps that you might need up front, so your algorithm may be incomplete -— this is fine. Getting started with and solving one of the subproblems you have identified in the planning stage often reveals the next subproblem you can work on. Or, if you already know the next subproblem, it’s often simpler with the first subproblem solved.

Many beginners try to solve the big problem in one go. Don’t do this. If the problem is sufficiently complex, you’ll get yourself tied in knots and make life a lot harder for yourself. Decomposing problems into smaller and easier to solve subproblems is a much better approach. Decomposition is the main way to deal with complexity, making problems easier and more approachable to solve and understand.

In short, break the big problem down and solve each of the smaller problems until you’ve solved the big problem.

#### If you're stuck while implementing
If you reduced the problem into smaller, managable subproblems and but still can't solve the subproblem:

+ **Debug:** 
<br>Go step by step through your solution trying to find where you went wrong. Programmers call this *debugging*.

```
“The art of debugging is figuring out what you really told your program to do rather than what you thought you told it to do.”” — Andrew Singer
```

+ **Reassess:**
<br>Take a step back. Look at the problem from another perspective. Is there anything that can be abstracted to a more general approach?

Another way of reassessing is starting anew. Delete everything and begin again with fresh eyes. I’m serious. You’ll be dumbfounded at how effective this is.

Or reduce the subproblem into something even more simpler. Then keep expanding until you reach the desired solution.

```
“If I could teach every beginning programmer one problem-solving skill, it would be the ‘reduce the problem technique.’

For example, suppose you’re a new programmer and you’re asked to write a program that reads ten numbers and figures out which number is the third highest. For a brand-new programmer, that can be a tough assignment, even though it only requires basic programming syntax.

If you’re stuck, you should reduce the problem to something simpler. Instead of the third-highest number, what about finding the highest overall? Still too tough? What about finding the largest of just three numbers? Or the larger of two?

Reduce the problem to the point where you know how to solve it and write the solution. Then expand the problem slightly and rewrite the solution to match, and keep going until you are back where you started.” — V. Anton Spraul
```

+ **Research:**
<br>Ahh, good ol’ Google. You read that right. No matter what problem you have, someone has probably solved it. Find that person/ solution. In fact, do this even if you solved the problem! (You can learn a lot from other people’s solutions).

Caveat: Don’t look for a solution to the big problem. Only look for solutions to sub-problems. Why? Because unless you struggle (even a little bit), you won’t learn anything. If you don’t learn anything, you wasted your time.

---

### Knowledge Check

**Q1.** What are the stages in the problem solving process?

**A1.** Understand the problem. Plan. Pseudocode. Divide and conquer (Implement).

**Q2.** Why is it important to clearly understand the problem first?

**A2.** Without having a clear understanding of the problem that needs solving, we can't properly implement a solution. Even if we lucked out and found a solution to the problem, we wouldn't be prepared for the inevitable future changes to the problem itself.

**Q3.** What can you do to help get a clearer understanding of the problem?

**A3.** "To gain clarity and understanding of the problem, write it down on paper, reword it in plain English until it makes sense to you, and draw diagrams if that helps. **When you can explain the problem to someone else in plain English, you understand it.**"

**Q4.** What are some of the things you should do in the planning stage of the problem solving process?

**A4.** "Some of the questions you should answer at the planning stage of the process:

+ Does your program have a user interface? What will it look like? What functionality will the interface have? Sketch this out on paper.
+ What inputs will your program have? Will the user enter data or will you get input from somewhere else?
+ What’s the desired output?
+ Given your inputs, what are the steps necessary to return the desired output? (Pseudocode)"

**Q5.** What is an algorithm?

**A5.** An algorithm can be broadly described as a step-by-step guide to solve a problem.

**Q6.** What is pseudocode?

**A6.** Pseudocode is the algorithm but it's in plain language(English) rather than programming language syntax. Pseudocode can be translated to different programming languages.

**Q7.** What are the advantages of breaking a problem down and solving the smaller problems?

**A7.** Slicing a large problem into multiple managable subproblems is an effective way to implement complex and large projects. Because creating a e-commerce web app for example can and will seem daunting at first, but when we break down the problem into smaller parts and solve them one by one, we won't be as much intimidated as diving into the large problem head on. Also solving a smaller problem is ultimately easier and will give you a feeling of accomplishment that will drive you to keep working on the project, instead of being intimidated by it.


