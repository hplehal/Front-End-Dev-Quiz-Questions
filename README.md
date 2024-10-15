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
