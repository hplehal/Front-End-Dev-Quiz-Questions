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

<!-- ## 2.  What is the event loop in Javascript runtimes? -->