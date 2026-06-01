# JavaScript: Basic to Expert

---

## Table of Contents

1. [Introduction to JavaScript](#1-introduction-to-javascript)
2. [Variables & Data Types](#2-variables--data-types)
3. [Operators](#3-operators)
4. [Control Flow & Conditionals](#4-control-flow--conditionals)
5. [Loops](#5-loops)
6. [Functions](#6-functions)
7. [Objects & Arrays](#7-objects--arrays)
8. [ES6+ Modern Features](#8-es6-modern-features)
9. [Asynchronous JavaScript](#9-asynchronous-javascript)
10. [DOM Manipulation](#10-dom-manipulation)
11. [Events](#11-events)
12. [Error Handling](#12-error-handling)
13. [Object-Oriented Programming (OOP)](#13-object-oriented-programming-oop)
14. [Prototypes & Prototypal Inheritance](#14-prototypes--prototypal-inheritance)
15. [Closures & Scope](#15-closures--scope)
16. [The "this" Keyword](#16-the-this-keyword)
17. [Modules (ESM & CommonJS)](#17-modules-esm--commonjs)
18. [Local Storage & Session Storage](#18-local-storage--session-storage)
19. [Fetch API & Working with JSON](#19-fetch-api--working-with-json)
20. [Regular Expressions (RegEx)](#20-regular-expressions-regex)
21. [Functional Programming Concepts](#21-functional-programming-concepts)
22. [Performance Tuning & Memory Management](#22-performance-tuning--memory-management)
23. [Security Best Practices](#23-security-best-practices)
24. [Testing (Jest Basics)](#24-testing-jest-basics)
25. [Expert Patterns & Best Practices](#25-expert-patterns--best-practices)

---

## 1. Introduction to JavaScript

JavaScript (JS) — lightweight, interpreted, or just-in-time compiled programming language with first-class functions. Multi-paradigm: prototype-based, imperative, declarative, and functional programming.

**Key facts:**
- **Environment:** Runs in browsers (V8, SpiderMonkey) and server-side (Node.js, Bun).
- **Threading:** Single-threaded, non-blocking event loop execution model.
- **Paradigms:** Dynamic typing, prototype-based object orientation.

---

## 2. Variables & Data Types

### Variable Declaration (var, let, const)
```javascript
var oldWay = "Avoid using var"; // Function-scoped, hoisted, re-declarable
let modernVar = "Use let";     // Block-scoped, mutable
const permanent = "Use const";  // Block-scoped, immutable reference

```

### Primitive Data Types

```javascript
let name = "Anik";            // String
let age = 25;                 // Number (both integer and float)
let isCoding = true;          // Boolean
let unknown;                  // Undefined (declared but unassigned)
let empty = null;             // Null (intentional absence of value)
let bigNumber = 90071992n;    // BigInt (arbitrary precision integers)
let uniqueKey = Symbol("id"); // Symbol (immutable primitive, strictly unique)

```

### Structural Data Types

```javascript
let user = { name: "Anik", age: 25 }; // Object literal
let collection = [1, 2, 3];           // Array (specialized object)

```

---

## 3. Operators

### Arithmetic Operators

```javascript
let sum = 10 + 5;       // 15 (Addition)
let diff = 10 - 5;      // 5 (Subtraction)
let product = 10 * 5;   // 50 (Multiplication)
let quotient = 10 / 5;  // 2 (Division)
let remainder = 10 % 3; // 1 (Modulus)

```

### Assignment Operators

```javascript
let x = 10;
x += 5; // Equivalent to x = x + 5

```

### Comparison Operators

```javascript
console.log(5 == "5");  // true (Abstract equality, coerces types)
console.log(5 === "5"); // false (Strict equality, checks value + type - Preferred)
console.log(10 > 5);    // true

```

### Logical Operators

```javascript
let result = (10 > 5) && (5 > 3); // Logical AND
let result2 = (10 > 5) || (5 < 3); // Logical OR
let result3 = !(10 > 5);           // Logical NOT

```

---

## 4. Control Flow & Conditionals

```javascript
let score = 85;

// If-Else Block
if (score >= 80) {
    console.log("Grade: A");
} else if (score >= 50) {
    console.log("Grade: Pass");
} else {
    console.log("Grade: Fail");
}

// Ternary Operator (Short-hand if-else)
let status = score >= 50 ? "Passed" : "Failed";

// Switch Statement
let day = "Monday";
switch (day) {
    case "Sunday":
        console.log("Weekend");
        break;
    case "Monday":
        console.log("Weekday");
        break;
    default:
        console.log("Invalid day");
}

```

---

## 5. Loops

```javascript
// For Loop (Iterating over a set range)
for (let i = 0; i < 5; i++) {
    console.log("Iteration: " + i);
}

// While Loop (Executes while condition evaluates to true)
let count = 0;
while (count < 5) {
    console.log("Count: " + count);
    count++;
}

// Do-While Loop (Executes at least once guaranteed)
let num = 1;
do {
    console.log("Runs once: " + num);
    num++;
} while (num <= 0);

// For...of Loop (Iterating over iterable values like Arrays)
let fruits = ["Apple", "Banana", "Orange"];
for (let fruit of fruits) {
    console.log(fruit);
}

// For...in Loop (Iterating over enumerable properties of an Object)
let person = { name: "Anik", age: 25 };
for (let key in person) {
    console.log(`${key}: ${person[key]}`);
}

```

---

## 6. Functions

```javascript
// Function Declaration
function greet(name) {
    return "Hello " + name;
}

// Function Expression
const add = function(a, b) {
    return a + b;
};

// Arrow Function (ES6)
const multiply = (a, b) => a * b;

// Default Parameters
const welcome = (user = "Guest") => "Welcome " + user;

```

---

## 7. Objects & Arrays

### Array Methods

```javascript
let numbers = [10, 20, 30, 40];

numbers.push(50);    // Mutates array: adds element to end
numbers.pop();       // Mutates array: removes element from end
numbers.unshift(5);  // Mutates array: adds element to start
numbers.shift();     // Mutates array: removes element from start

// Functional Array Transformations
let doubled = numbers.map(num => num * 2);           // Returns new transformed array
let filtered = numbers.filter(num => num > 20);      // Returns new filtered array
let sumOfAll = numbers.reduce((acc, num) => acc + num, 0); // Accumulates array into single value

```

### Object Manipulation

```javascript
const car = {
    brand: "Toyota",
    model: "Corolla",
    start: function() {
        return this.brand + " engine started.";
    }
};

console.log(car.brand);   // Dot notation
console.log(car["model"]); // Bracket notation
console.log(car.start()); // Executing method

```

---

## 8. ES6+ Modern Features

```javascript
// Template Literals
let user = "Anik";
let message = `Welcome back, ${user}!`; 

// Destructuring Assignment
const settings = { theme: "dark", volume: 80 };
const { theme, volume } = settings;

const colorList = ["red", "green", "blue"];
const [firstColor, secondColor] = colorList;

// Spread Operator (...)
let basicColors = ["red", "green"];
let allColors = [...basicColors, "blue", "yellow"]; // Unpacks arrays/objects

const baseObj = { a: 1, b: 2 };
const newObj = { ...baseObj, c: 3 };

// Rest Parameter (Gathers arguments into an array)
function sumNumbers(...nums) {
    return nums.reduce((sum, n) => sum + n, 0);
}

```

---

## 9. Asynchronous JavaScript

```javascript
// 1. Callbacks (Legacy pattern)
function fetchData(callback) {
    setTimeout(() => {
        callback("Data resolved via callback");
    }, 2000);
}

// 2. Promises (ES6 Native standard)
const getResult = () => {
    return new Promise((resolve, reject) => {
        let success = true;
        if (success) resolve("Promise Resolved");
        else reject("Promise Rejected");
    });
};

getResult()
    .then(res => console.log(res))
    .catch(err => console.error(err));

// 3. Async/Await (Syntactic sugar over Promises)
async function executeTask() {
    try {
        let response = await getResult(); // Halts execution line until promise settles
        console.log(response);
    } catch (error) {
        console.error("Caught error:", error);
    }
}

```

---

## 10. DOM Manipulation

Interfacing with the Document Object Model (DOM) to alter structural layouts dynamically.

```javascript
// Selection Methods
const title = document.getElementById("main-title");
const buttons = document.querySelectorAll(".btn"); // NodeList

// Content Alterations
title.textContent = "Altered Text Content";
title.innerHTML = "<strong>New Structural Content</strong>";

// Dynamic CSS Styling
title.style.color = "blue";
title.style.backgroundColor = "yellow";

// Node Generation and Injection
const newParagraph = document.createElement("p");
newParagraph.textContent = "Dynamically injected text node.";
document.body.appendChild(newParagraph);

```

---

## 11. Events

```javascript
const alertBtn = document.getElementById("my-btn");

// Attaching Event Listeners
alertBtn.addEventListener("click", function(event) {
    alert("Triggered Event!");
    console.log(event.target); // Node referencing the source of the event
});

```

**Vital browser events:**

* `'mouseover'` - Mouse pointer enters element boundaries
* `'keydown'`   - Key structural compression action
* `'submit'`    - Form element submission interception

---

## 12. Error Handling

```javascript
try {
    let x = 10;
    let y = x / nonExistentVariable; // Throws a ReferenceError
} catch (error) {
    console.error("Error signature intercepted: " + error.message);
} finally {
    console.log("Cleanup actions execute here unconditionally.");
}

// Instantiating Custom Error Interfaces
function checkAge(age) {
    if (age < 18) {
        throw new Error("Validation failure: Age domain must be >= 18.");
    }
    return "Authorized";
}

```

---

## 13. Object-Oriented Programming (OOP)

```javascript
// Base Class Blueprint
class Employee {
    constructor(name, salary) {
        this.name = name;
        this.salary = salary;
    }

    showDetails() {
        return `${this.name} earns ${this.salary} USD.`;
    }
}

// Classical Subclass Inheritance
class Manager extends Employee {
    constructor(name, salary, department) {
        super(name, salary); // Invokes the parent class constructor engine
        this.department = department;
    }

    showManagerDetails() {
        return `${this.name} oversees the ${this.department} division.`;
    }
}

const mgr = new Manager("Anik", 5000, "Engineering");
console.log(mgr.showDetails());

```

---

## 14. Prototypes & Prototypal Inheritance

JavaScript abstracts inheritance constructs using internal prototype link structures natively.

```javascript
function Device(name) {
    this.name = name;
}

// Adding shared capabilities directly to structural prototype tree to conserve execution memory
Device.prototype.turnOn = function() {
    return this.name + " execution link activated.";
};

const laptop = new Device("Laptop");
console.log(laptop.turnOn());

```

---

## 15. Closures & Scope

### Scope Class Range Profile

| Scope | Description |
| --- | --- |
| **Global Scope** | Everywhere inside execution context |
| **Function Scope** | Confined inside declaring boundary function |
| **Block Scope** | Limited strictly inside brackets `{}` (let/const only) |

### Closure Mechanics

A closure forms when an inner nested function references states captured outside its immediate lexical scope context, sustaining scope persistence.

```javascript
function createCounter() {
    let count = 0; // Private encapsulated state variable
    return function() {
        count++;
        return count;
    };
}

const counter = createCounter();
console.log(counter()); // 1
console.log(counter()); // 2 (Retains context memory)

```

---

## 16. The "this" Keyword

The runtime execution target binding of `this` varies systematically depending upon call context vectors.

```javascript
const userProfile = {
    username: "Anik",
    greet: function() {
        return "Identity reference: " + this.username; // `this` binds to userProfile
    }
};

// Controlling runtime execution context explicitly using call(), apply(), and bind()
function introduce(language, tool) {
    return `${this.username} works with ${language} utilizing ${tool}.`;
}

const explicitContext = { username: "Tamim" };

console.log(introduce.call(explicitContext, "JavaScript", "VSCode")); 
console.log(introduce.apply(explicitContext, ["JS", "Git"]));        
const permanentBound = introduce.bind(explicitContext, "Node.js", "Docker"); // Returns bound function
console.log(permanentBound());

```

---

## 17. Modules (ESM & CommonJS)

### ES Modules (ESM) — Browser / Modern Runtime Standard

```javascript
// file: math.js
export const addNumbers = (a, b) => a + b;
export default function multiply(a, b) { return a * b; }

// file: app.js
import multiply, { addNumbers } from './math.js';

```

### CommonJS Modules (CJS) — Traditional Node.js Standard

```javascript
// file: tools.js
module.exports = { log: msg => console.log(msg) };

// file: index.js
const tools = require('./tools');

```

---

## 18. Local Storage & Session Storage

```javascript
// Local Storage Engines (Persistent across browser runtime restarts)
localStorage.setItem("username", "Anik123");
let userSaved = localStorage.getItem("username");
localStorage.removeItem("username"); 
localStorage.clear(); 

// Storing Complex Data Framework Arrays/Objects (Serialize using strings)
const dataObj = { id: 1, role: "admin" };
localStorage.setItem("userRole", JSON.stringify(dataObj));
const retrieved = JSON.parse(localStorage.getItem("userRole")); // Parse transformation back to object

```

---

## 19. Fetch API & Working with JSON

```javascript
// Standard Asynchronous Read (GET)
fetch("[https://api.example.com/users](https://api.example.com/users)")
    .then(response => {
        if (!response.ok) throw new Error("HTTP Network error instance");
        return response.json();
    })
    .then(data => console.log(data))
    .catch(error => console.error("Error caught:", error));

// Complex Structural Mutate Request (POST via Async/Await)
async function sendData() {
    try {
        const response = await fetch("[https://api.example.com/users](https://api.example.com/users)", {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify({ name: "New User", role: "Member" })
        });
        const result = await response.json();
        console.log(result);
    } catch (err) {
        console.error(err);
    }
}

```

---

## 20. Regular Expressions (RegEx)

```javascript
let pattern = /javascript/i; // Flag 'i' designates Case-Insensitive evaluation matching
let text = "I love JavaScript!";
console.log(pattern.test(text)); // true

// Baseline Structural Validation Rules Example (Email Evaluation Matching Syntax)
let emailPattern = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6}$/;
console.log(emailPattern.test("test@example.com")); // true

```

---

## 21. Functional Programming Concepts

```javascript
// 1. Pure Functions (Consistent output derivation given matching arguments, zero side effects)
const pureAdd = (a, b) => a + b;

// 2. High-Order Functions (Functions receiving references or yielding functional targets)
const runTwice = (func, val) => func(func(val));
const addFive = x => x + 5;
console.log(runTwice(addFive, 10)); // Output: 20

// 3. Immutability Framework Concepts
const originalArray = [1, 2, 3];
const protectedArray = [...originalArray, 4]; // Avoids destructive mutation vectors

```

---

## 22. Performance Tuning & Memory Management

### Event Throttle/Debounce Strategies

```javascript
function debounce(func, delay) {
    let timer;
    return function(...args) {
        clearTimeout(timer);
        timer = setTimeout(() => func.apply(this, args), delay);
    };
}
const processSearch = debounce(() => console.log("Optimized network call executed"), 500);

```

### Memory Allocation Management Practices

* Evade accidental implicit declaration attachments to the global base object window scopes.
* Clear structural listeners (`removeEventListener`) inside interface cleanup workflows to drop dead internal reference tree branches.

---

## 23. Security Best Practices

```javascript
// Enforcing Strict Evaluation Execution Directives
"use strict";
// unauthorizedGlobal = 100; // Reference Error occurs natively

// Mitigating XSS (Cross-Site Scripting) Vectors
// AVOID: element.innerHTML = userControlledInput;
// PREFER: element.textContent = userControlledInput;

```

---

## 24. Testing (Jest Basics)

```javascript
// file: math.js
const sum = (a, b) => a + b;
module.exports = sum;

// file: math.test.js
const sum = require('./math');

test('Validates mathematical transformation execution mapping structure', () => {
    expect(sum(1, 2)).toBe(3);
});

```

---

## 25. Expert Patterns & Best Practices

### High Performance Memoization Caching Pattern

```javascript
function memoizeStructure(fn) {
    const cache = {};
    return function(...args) {
        const key = JSON.stringify(args);
        if (cache[key]) {
            return cache[key]; // Returns bypass resolution match instantly from memory state
        }
        const result = fn.apply(this, args);
        cache[key] = result;
        return result;
    };
}

```

### Defensive Optional Chaining (?.) & Nullish Coalescing (??) Operators

```javascript
const apiData = { user: { profile: { bio: "Developer Reference Details" } } };

// Optional chaining prevents execution thread termination breakdowns
console.log(apiData?.user?.profile?.bio); 
console.log(apiData?.user?.address?.city); // Evaluates cleanly to undefined without breaking

// Nullish Coalescing preserves deliberate falsy structural data values like numbers (0) or empty strings ("")
let userScore = 0;
let defaultCheckedScore = userScore ?? 100; // Resolves to 0 cleanly (Unlike standard logical OR shortfalls)

```

---

## Quick Reference Cheat Sheet

```javascript
// Declarations Matrix
let mutable = "let"; const fixedValue = "const";

// Compact Transformations Array Mappings
arr.map(x => x * 2); arr.filter(x => x > 5); arr.reduce((acc, current) => acc + current, 0);

// Modern Structural Branch Parsing Interception
async function runtimeContext() { let output = await fetch(endpoint); }

// Event Handling Interface
document.querySelector(".action-target").addEventListener("click", event => {
    console.log(event.type);
});

```

---

*JavaScript Target Baseline Specifications: Modern ECMAScript Standard Formats | Last Updated: 2026-05*

