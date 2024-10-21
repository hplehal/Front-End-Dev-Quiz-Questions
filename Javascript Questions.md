# Interview Questions

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
  - Macrotask queue is processed. The event loop dequeues the first callback from the macrotask queue and pushes it onto the call stack for execution. However, after a macrotask queue callback is processed, the event loop does not proceed with the next macrotask yet! The event loop first checks the microtask queue. Checking the microtask queue is necessary as microtasks have higher priority than macrotask queue callbacks. The macrotask queue callback that was just executed could have added more microtasks!
    -If the microtask queue is non-empty, process them as per the previous step.
    - If the microtask queue is empty, the next macrotask queue callback is processed. This repeats until the macrotask queue is empty.
1. This process continues indefinitely, allowing the JavaScript engine to handle both synchronous and asynchronous operations efficiently without blocking the call stack.
