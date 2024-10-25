# Front-End-Dev-Quiz-Questions
This is a repo for personal reference of different quiz questions about front end development topics. It is a deep dive into javascript, react, HTML &amp; CSS


## Javascript Questions 

### 1. What is the difference between Javascript variables ‘let’ , ‘const’ and  ‘var’?

```jsx
console.log(string); //This will give you an 'undefined' (Hoisting)
console.log(count); //Reference Error
console.log(obj); //Reference Error

let count = 1;
const obj = {};
var string = 'hello';
```

‘var’ are scoped inside the function in which they are created or  if created outside of any function, to the global object. ‘let’ and ‘const’ are block scoped, they are only accessible within the nearest set of curly braces

In modern Javascript it is recommended to use ‘const’ for values that dont need to be reassigned. It promotes immutability and prevents accidental changes

Use ‘let’ when reassigning a variable inside a scope.

Avoid using ‘var’ for its possible scoping issue and hoisting problems

### 2.  Explain event delegation in JavaScript? 
Event delegation is a design pattern in JavaScript used to efficiently manage and handle events on multiple child elements by attaching a single event listener to a common ancestor element. This pattern is particularly valuable in scenarios where you have a large number of similar elements, such as list items, and want to optimize event handling.

```jsx
// HTML:
// <ul id="list-items">
//   <li>Item 1</li>
//   <li>Item 2</li>
//   <li>Item 3</li>
// </ul>


const itemList = document.getElementById('list-item');

itemList.addEventListener('click', (event) => {
  if (event.target.tagName === 'li') {
    console.log(`Clicked on ${event.target.textContent}`);
  }
});
```
In this example, a single click event listener is attached to the ul element. When a click event occurs on an li element, the event bubbles up to the ul element, where the event listener checks the target's tag name to identify whether a list item was clicked. It's crucial to check the identity of the event.target as there can be other kinds of elements in the DOM tree.

### 3.  Explain event loop in Javascript?

The event loop is the heart of JavaScript's asynchronous operation. It is a mechanism in browsers that handles the execution of code, allowing for asynchronous operations and ensuring that the single-threaded nature of JavaScript engines does not block the execution of the program.

#### Event loop order :
1. The JavaScript engine starts executing scripts, placing synchronous operations on the call stack.
1. When an asynchronous operation is encountered (e.g., setTimeout(), HTTP request), it is offloaded to the respective Web API or Node.js API to handle the operation in the background.
1. Once the asynchronous operation completes, its callback function is placed in the respective queues – task queues (also known as macrotask queues / callback queues) or microtask queues. We will refer to "task queue" as "macrotask queue" from here on to better differentiate from the microtask queue.
1. The event loop continuously monitors the call stack and executes items on the call stack. If/when the call stack is empty:
  - Microtask queue is processed. The event loop takes the first callback from the microtask queue and pushes it to the call stack for execution. This repeats until the microtask queue is empty.
  - Macrotask queue is processed. The event loop dequeues the first callback from the macrotask queue and pushes it onto the call stack for execution. However, after a macrotask queue callback is processed, the event loop does not proceed with       the next macrotask yet! The event loop first checks the microtask queue. Checking the microtask queue is necessary as microtasks have higher priority than macrotask queue callbacks. The macrotask queue callback that was just executed could        have added more microtasks!
    - If the microtask queue is non-empty, process them as per the previous step.
    - If the microtask queue is empty, the next macrotask queue callback is processed. This repeats until the macrotask queue is empty.
5. This process continues indefinitely, allowing the JavaScript engine to handle both synchronous and asynchronous operations efficiently without blocking the call stack.

### 4. Describe event bubbling in JavaScript and browsers:
Event bubbling is a DOM event propagation mechanism where an event (e.g. a click), starts at the target element and bubbles up to the root of the document. This allows ancestor elements to also respond to the event.

Event bubbling is essential for event delegation, where a single event handler manages events for multiple child elements, enhancing performance and code simplicity. While convenient, failing to manage event propagation properly can lead to unintended behavior, such as multiple handlers firing for a single event.

During the bubbling phase, the event starts at the target element and bubbles up through its ancestors in the DOM hierarchy. This means that the event handlers attached to the target element and its ancestors can all potentially receive and respond to the event.
```jsx

// HTML:
// <div id="parent">
//   <button id="child">Click me!</button>
// </div>

const parent = document.getElementById('parent');
const child = document.getElementById('child');

parent.addEventListener('click', () => {
  console.log('Parent element clicked');
});

child.addEventListener('click', () => {
  console.log('Child element clicked');
});
```
When you click the "Click me!" button, both the child and parent event handlers will be triggered due to the event bubbling.

Event bubbling can be stopped during the bubbling phase using the `stopPropagation()` method. If an event handler calls `stopPropagation()`, it prevents the event from further bubbling up the DOM tree, ensuring that only the handlers of the elements up to that point in the hierarchy are executed.
```jsx

child.addEventListener('click', (event) => {
  console.log('Child element clicked');
  event.stopPropagation();
});

```

#### Benefits
- Cleaner code: Reduced number of event listeners improves code readability and maintainability.
- Efficient event handling: Minimizes performance overhead by attaching fewer listeners.
- Flexibility: Allows handling events happening on child elements without directly attaching listeners to them.
#### Pitfalls
- Accidental event handling: Be mindful that parent elements might unintentionally capture events meant for children. Use event.target to identify the specific element that triggered the event.
- Event order: Events bubble up in a specific order. If multiple parents have event listeners, their order of execution depends on the DOM hierarchy.
- Over-delegation: While delegating events to a common ancestor is efficient, attaching a listener too high in the DOM tree might capture unintended events.

### 5. Describe the difference between a cookie, `sessionStorage` and `localStorage` in browsers

`Cookies`: Suitable for server-client communication, small storage capacity, can be persistent or session-based, domain-specific. Sent to the server on every request.
`localStorage`: Suitable for long-term storage, data persists even after the browser is closed, accessible across all tabs and windows of the same origin, highest storage capacity among the three.
`sessionStorage`: Suitable for temporary data within a single page session, data is cleared when the tab or window is closed, has a higher storage capacity compared to cookies.
