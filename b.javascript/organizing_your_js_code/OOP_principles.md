# OOP Principles (SOLID)
## Principle #1: Single Responsibility
The single responsibility principle says that a class or module should have only a single purpose. For example, if you have a wallet class, that class should only implement wallet functionality. It’s fine to call other functionality, but it shouldn’t be written there.

Let’s look at a bad example. In the code below, the Car class has a single method; start. When this method is called the car may or may not start, depending on some logic which isn’t included here as it’s not important. The class will then log some information depending on the outcome. But notice how the logging functionality is implemented as a method of this class:

```js
class Car {
    constructor(make, model) {
        this.make = make;
        this.model = model;
    }

    start() {
        if (...) { // Logic to determine whether or not the car should start
            this.errorLog(`The car ${this.make} ${this.model} started.`);
            return true;
        }
        this.errorLog(`The car ${this.make} ${this.model} failed to start.`);
        return false;
    }

    errorLog(message) {
        console.log(message);
    }
}
```

This violates the single responsibility principle, because the logic for logging the information should not be a responsibility of the Car class.

There are a number of readability and code management issues that are caused by this, but the easiest issue to describe is actually refactoring.

Let’s say your logger logs to a file, and this works great for several months. Suddenly, an update occurs on the underlying system that the car class is running on, and you need to change the way you write to files. Suddenly you now need to update every file writing instance of every class you’ve ever implemented a logger inside of. The task would be huge! But what if you’d followed the single responsibility principle?

```js
class ErrorLog {
    static log(message) {
        console.log(message);
    }
}

class Car {
    constructor(make, model) {
        this.make = make;
        this.model = model;
    }

    start() {
        if (...) { // Logic to determine whether or not the car should start
            ErrorLog.log(`The car ${this.make} ${this.model} started.`);
            return true;
        }
        ErrorLog.log(`The car ${this.make} ${this.model} failed to start.`);
        return false;
    }
}
```

As you can see here, we wouldn’t have this problem. The logger is stored in a separate class, which means its functionality is separate to the Car class. The Car class can be changed, moved around or even deleted without affecting the logger class. Likewise, if a change is required to the logger class, it only needs to be carried out in a single place.

# Principle #2: Open-Closed
The open-closed principle says that code should be open for extension, but closed for modification. What this means is that if we want to add additional functionality, we should be able to do so simply by extending the original functionality, without the need to modify it.

To explain this, let’s look at an example. Below we have a Vehicle class. When a Vehicle instance is created, we pass in the fuel capacity and fuel efficiency. To get our range, we simply multiply our capacity by our efficiency.

```js
class Vehicle {
    constructor(fuelCapacity, fuelEfficiency) {
        this.fuelCapacity = fuelCapacity;
        this.fuelEfficiency = fuelEfficiency;
    }

    getRange() {
        return this.fuelCapacity * this.fuelEfficiency;
    }
}

const standardVehicle = new Vehicle(10, 15);

console.log(standardVehicle.getRange()); // Outputs '150'
```

But let’s say we add a new type of vehicle; a hybrid vehicle. This vehicle doesn’t just have standard fuel-based range, it also has an electric range which it can use as well. To find out the range now, we need to modify our getRange() method to check if the vehicle is hybrid, and add its electric range if so:

```js
class Vehicle {
    constructor(fuelCapacity, fuelEfficiency) {
        this.fuelCapacity = fuelCapacity;
        this.fuelEfficiency = fuelEfficiency;
    }

    getRange() {
        let range = this.fuelCapacity * this.fuelEfficiency;

        if (this instanceof HybridVehicle) {
            range += this.electricRange;
        }
        return range;
    }
}

class HybridVehicle extends Vehicle {
    constructor(fuelCapacity, fuelEfficiency, electricRange) {
        super(fuelCapacity, fuelEfficiency);
        this.electricRange = electricRange;
    }
}

const standardVehicle = new Vehicle(10, 15);
const hybridVehicle = new HybridVehicle(10, 15, 50);

console.log(standardVehicle.getRange()); // Outputs '150'
console.log(hybridVehicle.getRange()); // Outputs '200'
```

This violates the open-closed principle, because whilst adding our new HybridVehicle class we have had to go back and modify the code of our Vehicle class in order to make it work. Going forward, every time we add a new type of vehicle that might have different parameters for its range, we’ll have to continually modify that existing getRange function.

Instead what we could do, is to override the getRange method in the HybridVehicle class, giving the correct output for both Vehicle types, without ever modifying the original code:

```js
class Vehicle {
    constructor(fuelCapacity, fuelEfficiency) {
        this.fuelCapacity = fuelCapacity;
        this.fuelEfficiency = fuelEfficiency;
    }

    getRange() {
        return this.fuelCapacity * this.fuelEfficiency;
    }
}

class HybridVehicle extends Vehicle {
    constructor(fuelCapacity, fuelEfficiency, electricRange) {
        super(fuelCapacity, fuelEfficiency);
        this.electricRange = electricRange;
    }

    getRange() {
        return (this.fuelCapacity * this.fuelEfficiency) + this.electricRange;
    }
}

const standardVehicle = new Vehicle(10, 15);
const hybridVehicle = new HybridVehicle(10, 15, 50);

console.log(standardVehicle.getRange()); // Outputs '150'
console.log(hybridVehicle.getRange()); // Outputs '200'
```

## Principle #3: Liskov Substitution
The Liskov substitution principle states that any class should be substitutable for its parent class without unexpected consequences. In others words, if the classes Cat and Dog extend the class Animal, then we would expect all of the functionality held within the Animal class to behave normally for a Cat and Dog object.

A classic example of a Liskov substitution violation is the “square & rectangle problem”. In this problem, it is posed that a Square class can inherit from a Rectangle class. On the face of it, this makes sense; both shapes have two sides, and both calculate their area by multiplying their sides by each other.

But the problem arises when we try to utilise some Rectangle functionality on a Square object. Let’s look at an example:

```js
class Rectangle {
    constructor(height, width) {
        this.height = height;
        this.width = width;
    }

    setHeight(newHeight) {
        this.height = newHeight;
    }
}

class Square extends Rectangle {}

const rectangle = new Rectangle(4, 5);
const square = new Square(4, 4);

console.log(`Height: ${rectangle.height}, Width: ${rectangle.width}`); // Outputs 'Height: 4, Width: 5' (correct)
console.log(`Height: ${square.height}, Width: ${square.width}`); // Outputs 'Height: 4, Width: 4' (correct)

square.setHeight(5);
console.log(`Height: ${square.height}, Width: ${square.width}`); // Outputs 'Height: 5, Width: 4' (This should not be possible)
```

In this example we initialise a Rectangle and Square, and output their dimensions. We then call the Rectangle.setHeight() on the Square object, and output its dimensions again. What we find is that the square now has a different height than its length, which of course makes for an invalid square.

This can be solved, using polymorphism, an if statement in the Rectangle class, or a variety of other methods. But the real cause of the issue is that Square is not a good child class of Rectangle, and that in reality, perhaps both shapes should inherit from a Shape class instead.

## Principle #4: Interface Segregation
The interface segregation principle states that an entity should never be forced to implement an interface that contains elements which it will never use. For example, a Penguin should never be forced to implement a Bird interface if that Bird interface includes functionality relating to flying, as penguins (spoiler alert) cannot fly.

Now, this functionality is a little more difficult to demonstrate using JavaScript, due to its lack of interfaces. However, we can demonstrate it by using composition.

One of the advantages of composition over inheritance is the ability to more finely control and segregate interfaces. Inheritance implies a stronger coupling between the subclass and the superclass, and it often leads to inheriting not only the desired behavior but also unwanted or unnecessary behavior.

With composition, you can selectively choose and combine components (or objects) that provide the specific functionality you need. 

Here’s an example that addresses the interface segregation principle:

```js
class Penguin {}

class Bird {}

const flyer = {
    fly() {
        console.log(`Flap flap, I'm flying!`);
    },
};

Object.assign(Bird.prototype, flyer);

const bird = new Bird();
bird.fly(); // Outputs 'Flap flap, I'm flying!'

const penguin = new Penguin();
penguin.fly(); // 'Error: penguin.fly is not a function'
```

What this example does is to add the flying functionality (or interface) only to the class(es) that require it. This means that penguins won’t be given the ability to fly, whereas birds will.

## Principle #5: Dependency Inversion
The dependency inversion principle states that high level code should never depend on low level interfaces, and should instead use abstractions. It’s all about decoupling code.

Let’s say we have a piece of software that runs an online store, and within that software one of the classes (PurchaseHandler) handles the final purchase. This class is capable of charging the user’s credit card, and does so by using a PayPal API:

```js
class PurchaseHandler {
    processPayment(paymentDetails, amount) {
        // Complicated, PayPal specific logic goes here
        const paymentSuccess = PayPal.requestPayment(paymentDetails, amount);

        if (paymentSuccess) {
            // Do something
            return true;
        }

        // Do something
        return false;
    }
}
```

The problem here is that if we change from PayPal to Square (another payment processor) in 6 months time, this code breaks. We need to go back and swap out our PayPal API calls for Square API calls. But in addition, what if the Square API wants different types of data? Or perhaps it wants us to “stage” a payment first, and then to process it once staging has completed?

That’s bad, and so we need to abstract the functionality out instead.

Rather than directly call the PayPal API from our payment page, we’ll instead create another class called PaymentHandler. The interface for PurchaseHandler class will remain the same no matter what underlying payment system we use, even if the two systems are completely different. We’ll still need to make changes to the PaymentHandler interface if we change payment processor, but our higher level interface remains unchanged.

```js
class PurchaseHandler {
    processPayment(paymentDetails, amount) {
        const paymentSuccess = PaymentHandler.requestPayment(
            paymentDetails,
            amount
        );

        if (paymentSuccess) {
            // Do something
            return true;
        }

        // Do something
        return false;
    }
}

class PaymentHandler {
    requestPayment(paymentDetails, amount) {
        // Complicated, PayPal specific logic goes here
        return PayPal.requestPayment(paymentDetails, amount);
    }
}
```

Now you may be looking at this and thinking “but wait, that’s way more code”, and you’d be right. Like many of the SOLID principles (and indeed OO principles in general), the objective is less about writing less code or writing it quicker, and more about writing better code. The above change will save you days or maybe even weeks further down the line, in exchange for spending a few hours on it now.

---
### Knowledge Check

**Q1.** Explain the “Single Responsibility Principle”.

**A1.** The single responsibility principle says that a class or module should have only a single purpose, or in other words, should have only a single reason to change. For example, if you have a wallet class, that class should only implement wallet functionality. It’s fine to call other functionality, but it shouldn’t be written there.

**Q2.** Briefly explain the additional SOLID principles.

**A2.** <br>
**Principle #2: Open-Closed:** The open-closed principle says that code should be open for extension, but closed for modification. What this means is that if we want to add additional functionality, we should be able to do so simply by extending the original functionality, without the need to modify it.

**Principle #3: Liskov Substitution:** The Liskov substitution principle states that any class should be substitutable for its parent class without unexpected consequences. In others words, if the classes Cat and Dog extend the class Animal, then we would expect all of the functionality held within the Animal class to behave normally for a Cat and Dog object.

**Principle #4: Interface Segregation:** The interface segregation principle states that an entity should never be forced to implement an interface that contains elements which it will never use. For example, a Penguin should never be forced to implement a Bird interface if that Bird interface includes functionality relating to flying, as penguins cannot fly.

**Principle #5: Dependency Inversion:** The dependency inversion principle states that high level code should never depend on low level interfaces, and should instead use abstractions.

**Q3.** Explain what “tightly coupled” objects are and why we want to avoid them.

**A3.** In software development, "tightly coupled" refers to a situation where two or more components or objects depend on each other in a way that one component or object cannot function independently of the others. In other words, the components are highly interconnected and interdependent. Tightly coupled systems make it difficult to modify or replace one component without affecting the others.

Here are a few reasons why tightly coupled objects are generally undesirable:

1. **Reduced Modularity:** Tightly coupled systems lack modularity, making it challenging to isolate and change individual components without affecting the entire system. This reduces the flexibility and maintainability of the code.

2. **Difficulty in Testing:** When objects are tightly coupled, it becomes more difficult to test them in isolation. Changes to one component may have unintended consequences on other components, making it harder to isolate and identify the source of issues.

3. **Limited Reusability:** Tightly coupled systems are less reusable because individual components cannot be easily extracted and used in other contexts. Reusing or repurposing a tightly coupled component often requires carrying along its dependencies.

4. **Increased Complexity:** Tight coupling often leads to increased complexity. Understanding and maintaining a complex system can be challenging, especially when changes in one part of the system have ripple effects throughout the entire codebase.

5. **Dependency Management:** Tightly coupled systems often have complex dependency chains. This makes it harder to manage dependencies and increases the risk of introducing unintended side effects when updating or replacing components.

6. **Scalability Issues:** Tightly coupled systems may face scalability challenges. As the system grows, adding new features or modifying existing ones can become increasingly difficult without causing disruptions elsewhere in the system.

To address these issues, software developers strive to design systems with "loose coupling," where components are independent and interact through well-defined interfaces. Loose coupling promotes modularity, testability, reusability, and easier maintenance. Design principles such as the Dependency Inversion Principle (DIP) and Dependency Injection (DI) are commonly used to achieve loose coupling in object-oriented design.






