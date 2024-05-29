# DOM Manipulation and Events

## DOM - Document Object Model
The Document Object Model (DOM) is a programming interface for web documents. It represents the structure of an HTML or XML document as a tree-like data structure, where each element of the document is a node in the tree. The DOM allows JavaScript to access, manipulate, and modify the content and structure of a web page dynamically. In this detailed explanation, we'll cover the various aspects of the DOM in JavaScript.

1. **DOM Tree Structure:**
   At the top of the DOM tree is the document node, which represents the entire HTML document. The document node has several child nodes, such as the `<html>` element, which further has child nodes like the `<head>` and `<body>` elements, and so on. Every HTML element, attribute, and text content in the document is represented as a node in this tree structure.

2. **DOM Node Types:**
   There are different types of nodes in the DOM tree. The main node types are as follows:
   - Element nodes: Represent HTML elements, like `<div>`, `<p>`, `<a>`, etc.
   - Text nodes: Represent the text content within an element.
   - Attribute nodes: Represent attributes of an element, such as `id`, `class`, etc.
   - Comment nodes: Represent HTML comments within the document.
   - Document node: The root of the DOM tree, representing the entire document.

3. **Accessing DOM Elements:**
   JavaScript provides various methods to access elements in the DOM:
   - `document.getElementById()`: Returns an element with the specified ID.
   - `document.getElementsByClassName()`: Returns a collection of elements with the specified class name.
   - `document.getElementsByTagName()`: Returns a collection of elements with the specified tag name.
   - `document.querySelector()`: Returns the first element that matches a given CSS selector.
   - `document.querySelectorAll()`: Returns a "nodelist" of all elements that match a given CSS selector.

4. **Manipulating DOM Elements:**
   Once you have accessed an element, you can manipulate its content, attributes, and structure using properties and methods. Some common operations include:
   - `innerHTML`: Gets or sets the HTML content of an element.
   - `innerText` or `textContent`: Gets or sets the text content of an element.
   - `setAttribute()`: Sets the value of an attribute for an element.
   - `getAttribute()`: Gets the value of an attribute for an element.
   - `appendChild()`: Appends a new child element to an existing element.
   - `removeChild()`: Removes a child element from its parent.

5. **DOM Events:**
   The DOM allows you to handle events like clicks, keypresses, mouse movements, etc. by attaching event listeners to elements. Event listeners are functions that execute when a specific event occurs on an element. For example:
   ```javascript
   const button = document.getElementById('myButton');
   button.addEventListener('click', function(event) {
     // Your code here
   });
   ```

6. **DOM Traversal:**
   Traversal allows you to navigate through the DOM tree. You can move from one element to its parent, siblings, or children. Some methods used for traversal include:
   - `parentNode`: Gets the parent node of an element.
   - `childNodes`: Gets a collection of all child nodes of an element (including text nodes).
   - `firstChild` and `lastChild`: Gets the first and last child nodes of an element.
   - `nextSibling` and `previousSibling`: Gets the next and previous sibling nodes of an element.

7. **DOM Styling:**
   You can manipulate the CSS styles of elements using the `style` property or by adding/removing classes. For example:
   ```javascript
   const element = document.getElementById('myElement');
   element.style.color = 'red';
   element.classList.add('highlight');
   ```

8. **Creating and Modifying DOM Elements:**
   You can create new elements using the `document.createElement()` method and then add them to the document using various methods like `appendChild()` or `insertBefore()`. For example:
   ```javascript
   const newElement = document.createElement('div');
   newElement.textContent = 'This is a new element';
   document.body.appendChild(newElement);
   ```

9. **DOM Performance and Best Practices:**
   As DOM manipulation can be a performance-intensive task, it's essential to use best practices to optimize your code. Minimize direct DOM manipulation and instead, batch changes where possible. Use document fragments for creating multiple elements and inserting them together, rather than inserting them one by one.

### DOM nodes are objects
DOM nodes are objects. In JavaScript, every element, attribute, and text node in the Document Object Model (DOM) is represented as an object. These objects are instances of various DOM interfaces and inherit properties and methods specific to their corresponding node types.

Each node type (element node, text node, attribute node, etc.) is represented by a different DOM interface, which serves as a blueprint for creating instances of those nodes. For example:

1. Element nodes are represented by the `Element` interface.
2. Text nodes are represented by the `Text` interface.
3. Attribute nodes are represented by the `Attr` interface.

Each of these interfaces provides properties and methods to interact with the respective types of nodes. For example, an `Element` node object has properties like `nodeName`, `nodeType`, `textContent`, `innerHTML`, and methods like `getAttribute()`, `setAttribute()`, `appendChild()`, etc.

When you access an element or any other node in the DOM using JavaScript, you are essentially obtaining a reference to the corresponding DOM node object. You can then use this object to manipulate the element's content, attributes, or structure, as well as attach event listeners or traverse the DOM.

Here's an example of how you can access an element and treat it as an object:

```javascript
// Accessing an element with the ID 'myElement'
const myElement = document.getElementById('myElement');

// myElement is a DOM node object of type Element
// You can now interact with it as an object:
console.log(myElement.nodeName); // Output: "DIV"
console.log(myElement.textContent); // Output: "Hello, World!"

// Adding a new attribute to the element
myElement.setAttribute('data-custom', '123');

// Appending a new child element
const newChild = document.createElement('span');
newChild.textContent = 'New Child Element';
myElement.appendChild(newChild);
```

In summary, DOM nodes in JavaScript are represented as objects, and you can work with them using their respective interfaces to manipulate the web page dynamically.

### DOM Creation Steps
Here's an overview of how the DOM is created by the browser's JavaScript engine:

1. **Parsing HTML**: When a web page is loaded in a browser, the first step is parsing the HTML content. The browser's rendering engine reads and interprets the HTML code to understand the structure of the document. It then generates a hierarchical tree structure called the "Document Object Model."

2. **Node creation**: During the parsing process, the browser's JavaScript engine creates various objects to represent each element in the HTML document. These objects are known as "nodes." There are different types of nodes, such as "element nodes" for HTML tags, "text nodes" for text content, and "attribute nodes" for element attributes.

3. **Building the tree structure**: As the parsing progresses, the nodes are organized into a tree-like structure. Each node in the DOM tree has a parent-child relationship with other nodes, representing the hierarchical structure of the document. The topmost node in the tree is called the "document node" and corresponds to the entire HTML document.

4. **Creating relationships**: The browser's JavaScript engine establishes relationships between nodes to represent the layout of the document. For example, child nodes are connected to their parent nodes, and sibling nodes share the same parent.

5. **Exposing the DOM**: Once the parsing is complete and the DOM tree is built, the browser's JavaScript engine exposes the DOM to the web page's JavaScript code. Developers can access and interact with the DOM using the global `document` object, which represents the root of the DOM tree.

6. **Manipulating the DOM**: With access to the DOM, developers can use JavaScript to modify the content and structure of the web page dynamically. They can add, remove, or modify elements, update text content, change CSS styles, and respond to user interactions.

7. **Rendering updates**: Whenever the DOM is modified, the browser's rendering engine reflows and repaints the affected parts of the web page, updating the visible representation of the changes.

## Events
In JavaScript, events are a fundamental concept that enables interactivity and responsiveness in web applications. Events are actions or occurrences that happen in the browser, such as a mouse click, keyboard input, page loading, or resizing the window. JavaScript provides mechanisms to capture and handle these events, allowing developers to create dynamic and interactive web applications.

### Event Flow
Before diving into the details of events, it's essential to understand the event flow, also known as event propagation. Event flow describes the sequence in which events are processed by nested elements in the HTML document. The event flow can be categorized into three phases:

1. Capture Phase: The event starts from the top-level element (usually the document root) and propagates down the DOM tree until it reaches the target element. During this phase, the event can be intercepted and handled by any ancestor element before reaching the target (with (`capture: true`) ). 

2. Target Phase: The event reaches the target element, which is the element that directly triggered the event.

3. Bubbling Phase: After the event is handled at the target element, it starts propagating back up the DOM tree, allowing ancestor elements to react to the event. The event can be intercepted and handled at multiple levels during this phase.

### Event Handlers
To respond to events in JavaScript, you can attach event handlers, which are functions that execute when a specific event occurs. Event handlers are associated with DOM elements and can be added using various methods, such as `addEventListener` or by assigning functions to specific event properties of an element, like `onclick`, `onkeydown`, `onmouseover`, etc.

For example, to add a click event handler to a button with the id "myButton," you can use the `addEventListener` method:

```javascript
const myButton = document.getElementById('myButton');

myButton.addEventListener('click', function(event) {
  // Your event handling code here
});
```

### Event Listeners
Event listeners are functions that "listen" for specific events on DOM elements and trigger the associated event handler when the event occurs. An event listener is set up using the `addEventListener` method, which allows you to specify the event type (e.g., 'click', 'keydown', 'mouseover', etc.) and the function to handle the event.

The `addEventListener` method is used to set up event listeners, and it can be called on any DOM element. Multiple event listeners can be added to the same element, allowing you to have different event handlers for the same event type.

For example, to listen for a click event on the "myButton" element, we use the `addEventListener` method:

```javascript
const myButton = document.getElementById('myButton');

myButton.addEventListener('click', function(event) {
   // Your event handling code here
});
```

### Event Object
When an event occurs, a special object called the "Event Object" is created and passed as an argument to the event handler function. This object contains information about the event, including the type of event, the target element that triggered the event, the event timestamp, any associated data, and more.

### Event Propagation (Stop Propagation)
As mentioned earlier, events propagate through the DOM tree from the top (capture phase) to the target element and then back up (bubbling phase). Sometimes, you may want to stop the event from further propagation to prevent parent elements from handling the same event. You can use the `event.stopPropagation()` method inside an event handler to stop the event from propagating.

### Event Default Behavior (Prevent Default)
Certain events have default behaviors associated with them. For example, clicking on a link (`<a>` element) usually navigates to the URL specified in the `href` attribute. In some cases, you might want to prevent this default behavior from occurring and handle the event differently. You can use the `event.preventDefault()` method inside an event handler to prevent the default behavior from taking place.

### Event Delegation
Event delegation is a popular technique in JavaScript used to optimize event handling and improve performance, especially when dealing with a large number of elements or dynamically created elements. It involves attaching a single event listener to a parent element, rather than attaching individual event listeners to each child element within that parent. This way, you can capture events from multiple elements using a single handler.

The typical process of event delegation involves the following steps:

1. Identify a common parent element: Choose a parent element that contains all the child elements you want to target. This parent element should be an ancestor of the elements you want to handle events for.

2. Attach an event listener to the parent: Add an event listener to the chosen parent element, specifying the type of event you want to handle (e.g., click, mouseover, keypress, etc.).

3. Check the event target: When the event occurs (e.g., a click on a child element), the event will "bubble up" through the DOM tree from the target element (where the event occurred) to its parent and further up until it reaches the document's root element. The event object contains information about the target element and its ancestors. The event listener attached to the parent element will receive the event.

4. Determine the actual target: Inside the event listener, you can use the `event.target` property to find out which child element triggered the event. This way, you can identify the specific element that the event is related to.

5. Handle the event: Perform the desired action based on the target element. Since you have access to the target element inside the event listener, you can execute different actions depending on the target element's attributes or properties.

Event delegation is beneficial for several reasons:

1. Reduced memory usage: By attaching a single event listener to a parent element instead of multiple listeners to individual child elements, you save memory and avoid potential memory leaks.

2. Dynamic elements: If you have elements that are added or removed from the DOM dynamically, event delegation ensures that these new elements are automatically covered by the parent's event listener without the need to add additional listeners.

3. Performance: For large lists or collections of elements, event delegation can significantly improve performance since it reduces the overhead of setting up and managing multiple event listeners.

Here's an example to illustrate event delegation using vanilla JavaScript:

HTML:
```html
<ul id="parentList">
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>
```

JavaScript:
```javascript
const parentList = document.getElementById('parentList');

parentList.addEventListener('click', function(event) {
  // Check if the clicked element is an <li> element
  if (event.target.tagName === 'LI') {
    // Handle the click event for <li> elements
    console.log('Clicked on:', event.target.textContent);
  }
});
```

In this example, we attach the event listener to the `parentList` (the `<ul>` element) and check if the event's target is an `<li>` element. If it is, we log the text content of the clicked `<li>` element to the console. This way, we handle click events for all present and future `<li>` elements without explicitly attaching listeners to each one.


## Script Loading Strategies
If you are using JavaScript to manipulate the DOM, your code won't work if the JavaScript is loaded before the DOM node you are trying to access to.

### Internal JavaScript Solution - "DOMContentLoaded" Event

```js
document.addEventListener("DOMContentLoaded", () => {
  // …
});
```
This is an event listener, which listens for the browser's DOMContentLoaded event, which signifies that the HTML body is completely loaded and parsed. The JavaScript inside this block will not run until after that event is fired, therefore the error is avoided.

### External JavaScript Solution - "async" and "defer" Attributes
Scripts loaded using the async attribute will download the script without blocking the page while the script is being fetched. However, once the download is complete, the script will execute, which blocks the page from rendering. You get no guarantee that scripts will run in any specific order. It is best to use async when the scripts in the page run independently from each other and depend on no other script on the page.

Scripts loaded with the defer attribute will load in the order they appear on the page. They won't run until the page content has all loaded, which is useful if your scripts depend on the DOM being in place (e.g. they modify one or more elements on the page).

Here is a visual representation of the different script loading methods and what that means for your page:

!["Script Loading Methods"](../../img/javascript/script-loading-methods.jpg "Script Loading Methods")

To summarize:

+ async and defer both instruct the browser to download the script(s) in a separate thread, while the rest of the page (the DOM, etc.) is downloading, so the page loading is not blocked during the fetch process.

+ scripts with an async attribute will execute as soon as the download is complete. This blocks the page and does not guarantee any specific execution order.

+ scripts with a defer attribute will load in the order they are in and will only execute once everything has finished loading.

+ If your scripts should be run immediately and they don't have any dependencies, then use async.

+ If your scripts need to wait for parsing and depend on other scripts and/or the DOM being in place, load them using defer and put their corresponding \<script> elements in the order you want the browser to execute them.

### The Old Fashioned Solution
An old-fashioned solution used to be to put your script element right at the bottom of the body (e.g. just before the \</body> tag), so that it would load after all the HTML has been parsed. The problem with this solution is that loading/parsing of the script is completely blocked until the HTML DOM has been loaded. On larger sites with lots of JavaScript, this can cause a major performance issue, slowing down your site.

---

### Knowledge Check

**Q1.** What is the DOM?

**A1.** Document Object Model(DOM) is an interface created by the browser's JavaScript engine after parsing the requested HTML page. It's primarily used to manipulate the HTML elements (more accurately, DOM nodes) in order to add interactivity to the web page.

**Q2.** How do you target the nodes you want to work with?

**A2.** To target the DOM node we want to work with, we can access the node with `document.querySelector()`, using CSS selectors between the parantheses, then store the returned value in a variable. This way we can manipulate the node using various properties and methods avaliable to that node type. `document.querySelector()` returns first node with the given CSS selector, while `document.querySelectorAll()` returns all the nodes (a "nodelist") corresponding the given CSS selector.

**Q3.** How do you create an element in the DOM?

**A3.** 
We can create new elements using the `document.createElement()` method and then add them to the document using various methods like `appendChild()` or `insertBefore()`. For example:

   ```javascript
   const newElement = document.createElement('div');
   newElement.textContent = 'This is a new element';
   document.body.appendChild(newElement);
   ```

**Q4.** How do you add an element to the DOM?

**A4.** As demonstrated in the above example, we can add an element to the DOM tree with `appendChild()` method.

```javascript
   const newElement = document.createElement('div');
   newElement.textContent = 'This is a new element';
   document.body.appendChild(newElement);
   ```

**Q5.** How do you remove an element from the DOM?

**A5.** The `removeChild()` method is a JavaScript method used to remove a child node from its parent. Here's an example of how to use `removeChild()`:

```html
<div id="parent">
  <p>This is a paragraph.</p>
  <p>This is another paragraph.</p>
</div>
```

```javascript
// Get a reference to the parent element
const parentElement = document.getElementById('parent');

// Get a reference to the child node you want to remove (in this case, the first <p> element)
const childToRemove = parentElement.querySelector('p');

// Check if the child node exists before attempting to remove it
if (childToRemove) {
  // Use the removeChild() method to remove the child node from its parent
  parentElement.removeChild(childToRemove);
}
```

After running this JavaScript code, the first `<p>` element will be removed from the "parent" div, and the resulting HTML structure will look like this:

```html
<div id="parent">
  <p>This is another paragraph.</p>
</div>
```

**Q6.** How can you alter an element in the DOM?

**A6.** When you have a reference to an element, you can use that reference to alter the element’s own properties. This allows you to do many useful alterations, like adding/removing and altering attributes, changing classes, adding inline style information and more. For example:

```javascript
const div = document.createElement('div');                     
// creates a new div referenced in the variable 'div'
```

**Adding inline style**

```javascript
div.style.color = 'blue';                                      
// adds the indicated style rule

div.style.cssText = 'color: blue; background: white;';          
// adds several style rules

div.setAttribute('style', 'color: blue; background: white;');    
// adds several style rules
```

Note that if you’re accessing a kebab-cased CSS rule from JS, you’ll either need to use camelCase or you’ll need to use bracket notation instead of dash notation.

```javascript
div.style.background-color // doesn't work - attempts to subtract color from div.style.background
div.style.backgroundColor // accesses the div's background-color style
div.style['background-color'] // also works
div.style.cssText = "background-color: white;" // sets the div's background-color by assigning a CSS string
```

**Editing attributes**

```javascript
div.setAttribute('id', 'theDiv');                              
// if id exists, update it to 'theDiv', else create an id
// with value "theDiv"

div.getAttribute('id');                                        
// returns value of specified attribute, in this case
// "theDiv"

div.removeAttribute('id');                                     
// removes specified attribute
```

**Working with classes**

```javascript
div.classList.add('new');                                      
// adds class "new" to your new div

div.classList.remove('new');                                   
// removes "new" class from div

div.classList.toggle('active');                                
// if div doesn't have class "active" then add it, or if
// it does, then remove it
```

**Adding text content**

```javascript
div.textContent = 'Hello World!'                               
// creates a text node containing "Hello World!" and
// inserts it in div
```

**Adding HTML content**

```javascript
div.innerHTML = '<span>Hello World!</span>';                   
// renders the HTML inside div
```

Note that textContent is preferable for adding text, and innerHTML should be used sparingly as it can create security risks if misused. 

**Q7.** When adding text to a DOM element, should you use textContent or innerHTML? Why?

**A7.** `innerHTML` can be misused to inject malicious script into our code, using `textContent` to add text to a DOM element eliminates this possibility.

**Q8.** Where should you include your JavaScript tag in your HTML file when working with DOM nodes?

**A8.** In order to successfully target a DOM element and not get an error, the DOM node we are trying to access should be already created by the JavaScript engine. There are several script loading strategies avaliable to achieve this. A modern recommended way to include our JavaScript code into our HTML page is to use the boolean `defer` attribute along with our script tag (`<script defer>`).

Scripts loaded with the defer attribute will load in the order they appear on the page. They won't run until the page content has all loaded, which is useful if your scripts depend on the DOM being in place (e.g. they modify one or more elements on the page).

**Q9.** How do “events” and “listeners” work?

**A9.** In JavaScript, events are a fundamental concept that enables interactivity and responsiveness in web applications. Events are actions or occurrences that happen in the browser, such as a mouse click, keyboard input, page loading, or resizing the window. JavaScript provides mechanisms to capture and handle these events, allowing developers to create dynamic and interactive web applications.

Event listeners are functions that "listen" for specific events on DOM elements and trigger the associated event handler when the event occurs. An event listener is set up using the `addEventListener` method, which allows you to specify the event type (e.g., 'click', 'keydown', 'mouseover', etc.) and the function to handle the event.

The `addEventListener` method is used to set up event listeners, and it can be called on any DOM element. Multiple event listeners can be added to the same element, allowing you to have different event handlers for the same event type.

For example, to listen for a click event on the "myButton" element, we use the `addEventListener` method:

```javascript
const myButton = document.getElementById('myButton');

myButton.addEventListener('click', function(event) {
   // Your event handling code here
});
```

**Q10.** What are three ways to use events in your code?

**A10.** In JavaScript, there are several ways to handle events, but the three primary methods are:

**Specify function attributes directly on HTML elements**

```javascript
<button onclick="alert('Hello World')">Click Me</button>
```

This solution is less than ideal because we’re cluttering our HTML with JavaScript. Also, we can only set one “onclick” property per DOM element, so we’re unable to run multiple separate functions in response to a click event using this method.

**Set properties of form `on[eventType] (onclick, onmousedown, etc.)` on the DOM nodes in your JavaScript**

```html
<!-- the HTML file -->
<button id="btn">Click Me</button>
```

```javascript
// the JavaScript file
const btn = document.querySelector('#btn');
btn.onclick = () => alert("Hello World");
```

This is a little better. We’ve moved the JS out of the HTML and into a JS file, but we still have the problem that a DOM element can only have 1 “onclick” property.

**Attach event listeners to the DOM nodes with JavaScript (Recommended)**

```html
<!-- the HTML file -->
<button id="btn">Click Me Too</button>
```

```javascript
// the JavaScript file
const btn = document.querySelector('#btn');
btn.addEventListener('click', () => {
  alert("Hello World");
});
```

Now, we maintain separation of concerns, and we also allow multiple event listeners if the need arises. This method is much more flexible and powerful.

Note that all 3 of these methods can be used with named functions like so:

```html
<!-- the HTML file -->
<!-- METHOD 1 -->
<button onclick="alertFunction()">CLICK ME.</button>
```

```javascript
// the JavaScript file
function alertFunction() {
  alert("YAY! YOU DID IT!");
}

// METHOD 2
btn.onclick = alertFunction;

// METHOD 3
btn.addEventListener('click', alertFunction);
```

**Q11.** Why are event listeners the preferred way to handle events?

**A11.** As explained above, by using event listeners, we separete our HTML code and JavaScript code, also we can listen for multiple events if the need arises. The other methods; specifying function attributes directly on HTML elements, requires mixing our HTML with JavaScript and we can't listen for multiple events, while with setting properties of form `on[eventType] (onclick, onmousedown, etc.)` on the DOM nodes in our JavaScript, we seperate HTML and JavaScript, but still can't listen for multiple events. 

**Q12.** What are the benefits of using named functions in your listeners?

**A12.** If the function is something we will use in multiple places in our code, it makes more sense to use function declaration and call the function with it's name, instead of anonymously declaring the same function in multiple places. This way we can keep our code cleaner and concise.

**Q13.** How do you attach listeners to groups of nodes?

**A13.** We can get a "nodelist" of all of the items matching a specific CSS selector with `querySelectorAll('selector')`. In order to add a listener to each of them we simply need to iterate through the whole list like so:

```html
<div id="container">
    <button id="1">Click Me</button>
    <button id="2">Click Me</button>
    <button id="3">Click Me</button>
</div>
```

```javascript
// buttons is a node list. It looks and acts much like an array.
const buttons = document.querySelectorAll('button');

// we use the .forEach method to iterate through each button
buttons.forEach((button) => {

  // and for each one we add a 'click' listener
  button.addEventListener('click', () => {
    alert(button.id);
  });
}); // A caveat: forEach() method takes a function as an argument, thus above anonymous function is a callback function.
```

**Q14.** What is the difference between the return values of querySelector and querySelectorAll?

**A14.** 
- `document.querySelector()`: Returns the first element that matches a given CSS selector.
- `document.querySelectorAll()`: Returns a "nodelist" of all elements that match a given CSS selector.

**Q15.** What does a “nodelist” contain?

**A15.** A nodelist contains an array-like list of references to DOM nodes returned by `document.querySelectorAll()`.

**Q16.** Explain the difference between “capture” and “bubbling”.

**A16.** Event flow (also known as event propagation) describes the sequence in which events are processed by nested elements in the HTML document. The event flow can be categorized into three phases:

1. Capture Phase: The event starts from the top-level element (usually the document root) and propagates down the DOM tree until it reaches the target element. During this phase, the event can be intercepted and handled by any ancestor element before reaching the target (with (`capture: true`) ). 

2. Target Phase: The event reaches the target element, which is the element that directly triggered the event.

3. Bubbling Phase: After the event is handled at the target element, it starts propagating back up the DOM tree, allowing ancestor elements to react to the event. The event can be intercepted and handled at multiple levels during this phase.

**Event Propagation (Stop Propagation)**: As mentioned earlier, events propagate through the DOM tree from the top (capture phase) to the target element and then back up (bubbling phase). Sometimes, you may want to stop the event from further propagation to prevent parent elements from handling the same event. You can use the `event.stopPropagation()` method inside an event handler to stop the event from propagating.