# JavaScript Cheat Sheet

## 1. Basic Syntax

```javascript
console.log("Hello, World!");

let name = "JavaScript";
console.log(name);
```

- `console.log()` — Display output.
- `//` — Single-line comment.
- `/* */` — Multi-line comment.
- `;` — Statement terminator (optional in many cases).

## 2. Variables

```javascript
var oldName = "John";
let age = 20;
const country = "India";
```

| Keyword | Description |
|---|---|
| `var` | Function-scoped, can be redeclared and updated. |
| `let` | Block-scoped, can be updated. |
| `const` | Block-scoped, cannot be reassigned. |

- Prefer `const` by default.
- Use `let` when the value changes.
- Avoid `var` in modern JavaScript.

## 3. Data Types

**Primitive Types**

- `String` — Text.
- `Number` — Integer and decimal numbers.
- `BigInt` — Large integers.
- `Boolean` — `true` or `false`.
- `Undefined` — Variable declared but not assigned.
- `Null` — Intentional absence of a value.
- `Symbol` — Unique identifier.

**Non-Primitive Types**

- `Object`
- `Array`
- `Function`

```javascript
let name = "Alex";
let age = 22;
let price = 99.99;
let isActive = true;
let value = null;
let result;
```

- `typeof value` — Check the data type.
- `typeof null` returns `"object"` (JavaScript quirk).

## 4. Operators

| Operator | Description |
|---|---|
| `+` `-` `*` `/` `%` `**` | Arithmetic |
| `==` `!=` | Loose comparison |
| `===` `!==` | Strict comparison |
| `>` `<` `>=` `<=` | Relational |
| `&&` `\|\|` `!` | Logical |
| `=` `+=` `-=` `*=` | Assignment |
| `++` `--` | Increment / Decrement |
| `??` | Nullish coalescing |
| `?.` | Optional chaining |
| `typeof` | Check data type |
| `instanceof` | Check object type |

**Note:** Prefer `===` and `!==` over loose comparisons.

## 5. Strings

```javascript
let name = "JavaScript";

name.length;
name.toUpperCase();
name.toLowerCase();
name.trim();
name.includes("Java");
name.indexOf("Script");
name.slice(0, 4);
name.replace("Java", "Type");
```

### Template Literals

```javascript
let firstName = "John";
let message = `Hello, ${firstName}`;
```

## 6. Arrays

```javascript
const numbers = [1, 2, 3, 4, 5];
const mixed = [1, "Hello", true];
```

**Common Array Methods**

| Method | Description |
|---|---|
| `push()` | Add element at the end. |
| `pop()` | Remove last element. |
| `shift()` | Remove first element. |
| `unshift()` | Add element at the beginning. |
| `slice()` | Extract part of an array. |
| `splice()` | Add, remove or replace elements. |
| `includes()` | Check if an element exists. |
| `indexOf()` | Find element position. |
| `join()` | Convert array into a string. |
| `concat()` | Combine arrays. |

### Modern Array Methods

| Method | Description |
|---|---|
| `map()` | Transform each element. |
| `filter()` | Filter elements based on a condition. |
| `find()` | Find the first matching element. |
| `findIndex()` | Find the index of a matching element. |
| `reduce()` | Reduce elements to a single value. |
| `forEach()` | Execute a function for each element. |
| `some()` | Check if at least one element matches. |
| `every()` | Check if all elements match. |
| `sort()` | Sort array elements. |

```javascript
const numbers = [1, 2, 3, 4, 5];

numbers.map(n => n * 2);

numbers.filter(n => n > 2);

numbers.find(n => n > 3);

numbers.reduce((sum, n) => sum + n, 0);

numbers.forEach(n => console.log(n));
```

## 7. Objects

Objects store data as key-value pairs.

```javascript
const student = {
    name: "Alex",
    age: 21,
    isActive: true
};
```

**Access Properties**

```javascript
student.name;
student["age"];

// Add property
student.city = "Delhi";

// Update property
student.age = 22;

// Delete property
delete student.isActive;
```

**Useful Object Methods**

```javascript
Object.keys(student);    // Get keys
Object.values(student);  // Get values
Object.entries(student); // Get key-value pairs
```

## 8. Conditional Statements

### If-Else

```javascript
if (age >= 18) {
    console.log("Adult");
} else if (age >= 13) {
    console.log("Teenager");
} else {
    console.log("Child");
}
```

### Ternary Operator

```javascript
let result = age >= 18 ? "Adult" : "Minor";
```

### Switch

```javascript
switch (day) {
    case 1:
        console.log("Monday");
        break;
    default:
        console.log("Invalid day");
}
```

### Truthy & Falsy Values

Falsy values:

- `false`
- `0`
- `-0`
- `0n`
- `""`
- `null`
- `undefined`
- `NaN`

Everything else is truthy.

## 9. Loops

```javascript
// For loop
for (let i = 0; i < 5; i++) {
    console.log(i);
}

// While loop
while (i < 5) {
    i++;
}

// Do-while
do {
    i++;
} while (i < 5);

// For...of (arrays)
for (const num of numbers) {
    console.log(num);
}

// For...in (object keys)
for (const key in student) {
    console.log(key);
}
```

- `break` — Exit the loop.
- `continue` — Skip the current iteration.

## 10. Functions

### Function Declaration

```javascript
function greet(name) {
    return `Hello, ${name}`;
}
```

### Function Expression

```javascript
const greet = function(name) {
    return `Hello, ${name}`;
};
```

### Arrow Function

```javascript
const greet = (name) => `Hello, ${name}`;

const add = (a, b) => a + b;
```

### Default Parameters

```javascript
function greet(name = "Guest") {
    return `Hello, ${name}`;
}
```

## 11. Scope & Hoisting

**Scope**

- Global Scope — Accessible throughout the program.
- Function Scope — Accessible inside a function.
- Block Scope — Accessible inside a block `{}` using `let` and `const`.

**Hoisting**

- Function declarations are hoisted.
- `var` is hoisted and initialized with `undefined`.
- `let` and `const` cannot be accessed before declaration (Temporal Dead Zone).

## 12. Closures & Higher-Order Functions

**Closure:** A function remembers variables from its outer scope.

```javascript
function counter() {
    let count = 0;

    return function() {
        return ++count;
    };
}

const increment = counter();
increment();
```

**Higher-Order Function:** A function that accepts another function or returns a function.

```javascript
function calculate(a, b, operation) {
    return operation(a, b);
}

calculate(10, 5, (a, b) => a + b);
```

## 13. ES6+ Features

### Destructuring

```javascript
// Array destructuring
const [a, b] = [10, 20];

// Object destructuring
const { name, age } = student;
```

### Spread Operator

```javascript
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5];

// Object copy
const newStudent = { ...student, age: 22 };
```

### Rest Parameters

```javascript
function sum(...numbers) {
    return numbers.reduce((total, n) => total + n, 0);
}
```

### Optional Chaining

```javascript
console.log(student.address?.city);
```

### Nullish Coalescing

```javascript
const username = null;
const name = username ?? "Guest";
```

### Modules

```javascript
// Export
export const name = "JavaScript";

// Import
import { name } from "./app.js";

// Default export
export default function greet() {
    console.log("Hello");
}
```

## 14. Object-Oriented Programming

### Constructor Function

```javascript
function Student(name, age) {
    this.name = name;
    this.age = age;
}
```

### Classes & Objects

```javascript
class Student {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    introduce() {
        return `Hello, I am ${this.name}`;
    }
}

const student = new Student("Alex", 21);
```

### Inheritance

```javascript
class Person {
    constructor(name) {
        this.name = name;
    }
}

class Student extends Person {
    constructor(name, course) {
        super(name);
        this.course = course;
    }
}
```

- `this` — Refers to the current object.
- `super` — Calls the parent class constructor or methods.
- `extends` — Inherits from another class.
- `constructor()` — Initializes an object.
- `new` — Creates an object.

## 15. Asynchronous JavaScript

### Callbacks

A function passed as an argument to another function.

```javascript
function greet(callback) {
    console.log("Hello");
    callback();
}

greet(() => console.log("Welcome"));
```

### setTimeout & setInterval

```javascript
setTimeout(() => {
    console.log("Executed once");
}, 2000);

setInterval(() => {
    console.log("Repeating");
}, 1000);
```

### Promises

Represents the eventual completion or failure of an asynchronous operation.

**Promise States:**
- Pending
- Fulfilled
- Rejected

```javascript
const promise = new Promise((resolve, reject) => {
    resolve("Success");
});

promise
    .then(result => console.log(result))
    .catch(error => console.log(error))
    .finally(() => console.log("Completed"));
```

### Async / Await

A cleaner way to work with promises.

```javascript
async function getData() {
    try {
        const response = await fetch("https://example.com");
        const data = await response.json();

        return data;
    } catch (error) {
        console.log(error);
    }
}
```

## 16. Error Handling

```javascript
try {
    JSON.parse("invalid JSON");
} catch (error) {
    console.log(error.message);
} finally {
    console.log("Completed");
}
```

```javascript
throw new Error("Something went wrong");
```

- `try` — Contains code that may throw an error.
- `catch` — Handles errors.
- `finally` — Executes after try/catch.
- `throw` — Creates or throws an error.

## 17. JSON

JSON (JavaScript Object Notation) is commonly used for exchanging data between applications.

```javascript
const user = {
    name: "Alex",
    age: 22
};

// Object to JSON string
const json = JSON.stringify(user);

// JSON string to object
const obj = JSON.parse(json);
```

## 18. DOM Manipulation

The DOM allows JavaScript to interact with HTML elements in a browser.

```javascript
// Select elements
document.getElementById("title");
document.querySelector(".container");
document.querySelectorAll("p");

// Change content
document.getElementById("title").textContent = "Hello";

// Change styles
element.style.color = "red";

// Event listener
button.addEventListener("click", () => {
    console.log("Button clicked");
});

// Create an element
const div = document.createElement("div");

// Add element
document.body.appendChild(div);
```

## 19. Useful JavaScript Methods

| Method | Description |
|---|---|
| `JSON.stringify()` | Convert object to JSON string. |
| `JSON.parse()` | Convert JSON string to object. |
| `parseInt()` | Convert string to integer. |
| `parseFloat()` | Convert string to decimal number. |
| `Number()` | Convert value to number. |
| `String()` | Convert value to string. |
| `isNaN()` | Check whether a value is NaN. |
| `Math.round()` | Round a number. |
| `Math.floor()` | Round down. |
| `Math.ceil()` | Round up. |
| `Math.random()` | Generate a random number. |

## 20. Quick Revision

- Prefer `const` and `let` over `var`.
- Use `===` instead of `==`.
- Use `map()` to transform arrays.
- Use `filter()` to select elements.
- Use `reduce()` to calculate a single result.
- Use arrow functions for concise callbacks.
- Understand closures and higher-order functions.
- Learn destructuring, spread and rest operators.
- Understand promises and `async/await`.
- Use `try...catch` for error handling.
- Understand objects, classes and prototypes.
