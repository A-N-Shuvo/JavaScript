# JavaScript Learning Roadmap

## Updated Structured Path (Recommended)
- Start: `README.md`
- Roadmap: `01-roadmap-js-0-to-advanced.md`
- Step-by-step: `02-step-by-step-guideline.md`
- Project path: `03-project-based-learning.md`
- Learning flow diagrams: `04-process-flow-diagram.md`
- Concept quick reference: `05-javascript-concepts-reference.md`
- Practice sets: `MCQ-Bank/`

## Note
This file contains a legacy deep-dive reference. For the easiest guided learning journey, use the updated files listed above.

## Phase 1 — Foundations

### 1. Variables & Types
```js
// var (function-scoped, avoid), let (block-scoped), const (block-scoped, immutable binding)
const name = "Alice";
let age = 30;

// Types: string, number, boolean, null, undefined, symbol, bigint, object
typeof "hello"    // "string"
typeof null       // "object" (historical bug)
typeof undefined  // "undefined"
```

### 2. Operators & Coercion
```js
// == coerces types, === does not — always use ===
0 == false   // true
0 === false  // false

// Nullish coalescing: returns right side if left is null/undefined
const val = null ?? "default";  // "default"

// Optional chaining: short-circuits on null/undefined
const city = user?.address?.city;
```

### 3. Control Flow
```js
// if/else, switch, ternary
const label = score >= 60 ? "pass" : "fail";

// for, while, for...of (iterables), for...in (keys — avoid on arrays)
for (const item of [1, 2, 3]) console.log(item);
for (const key in { a: 1 }) console.log(key);
```

### 4. Functions
```js
// Declaration (hoisted), expression (not hoisted), arrow (no own `this`)
function greet(name) { return `Hello ${name}`; }

const greet = function(name) { return `Hello ${name}`; };

const greet = (name) => `Hello ${name}`;

// Default params, rest, spread
function sum(...nums) { return nums.reduce((a, b) => a + b, 0); }
sum(1, 2, 3); // 6

const arr = [1, 2, 3];
Math.max(...arr); // 3
```

---

## Phase 2 — ES6+ Features

### 5. Destructuring
```js
// Array
const [first, second, ...rest] = [1, 2, 3, 4];

// Object
const { name, age, city = "Unknown" } = person;

// Rename
const { name: fullName } = person;

// Function param destructuring
function display({ name, age }) { console.log(name, age); }
```

### 6. Template Literals
```js
const msg = `Hello ${name}, you are ${age} years old.`;

// Tagged templates
function highlight(strings, ...values) {
  return strings.reduce((acc, str, i) => acc + str + (values[i] ?? ""), "");
}
highlight`Hello ${name}!`;
```

### 7. Modules (ESM)
```js
// export
export const PI = 3.14;
export function add(a, b) { return a + b; }
export default class Calculator {}

// import
import Calculator, { PI, add } from "./math.js";
import * as math from "./math.js";

// Dynamic import (lazy loading)
const module = await import("./heavy.js");
```

### 8. Classes
```js
class Animal {
  #name; // private field (ES2022)

  constructor(name) {
    this.#name = name;
  }

  speak() {
    return `${this.#name} makes a sound.`;
  }

  static create(name) { return new Animal(name); }
}

class Dog extends Animal {
  speak() {
    return super.speak() + " Woof!";
  }
}
```

### 9. Symbols & Iterators
```js
// Symbol: unique, often used as object keys
const id = Symbol("id");
const user = { [id]: 123, name: "Alice" };

// Custom iterator
const range = {
  from: 1, to: 5,
  [Symbol.iterator]() {
    let current = this.from;
    return {
      next: () => current <= this.to
        ? { value: current++, done: false }
        : { done: true }
    };
  }
};
for (const n of range) console.log(n); // 1 2 3 4 5
```

---

## Phase 3 — Closures & Scope

### 10. Scope Chain
```js
// Each function creates new scope; inner functions access outer vars via scope chain
const x = 10;
function outer() {
  const y = 20;
  function inner() {
    console.log(x + y); // 30 — accesses both outer scopes
  }
  inner();
}
```

### 11. Closures
Closure = function that remembers variables from its creation scope, even after outer function returns.

```js
function makeCounter() {
  let count = 0;          // this variable is "closed over"
  return {
    increment() { count++; },
    decrement() { count--; },
    value() { return count; }
  };
}

const counter = makeCounter();
counter.increment();
counter.increment();
counter.value(); // 2
// count is inaccessible from outside — true encapsulation
```

```js
// Factory pattern with closure
function multiplier(factor) {
  return (num) => num * factor;  // factor is closed over
}
const double = multiplier(2);
const triple = multiplier(3);
double(5); // 10
triple(5); // 15
```

```js
// Classic closure bug & fix
// Bug: all i refer to same variable
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100); // prints 3 3 3
}

// Fix 1: use let (block scope per iteration)
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100); // prints 0 1 2
}

// Fix 2: IIFE to capture each value
for (var i = 0; i < 3; i++) {
  ((j) => setTimeout(() => console.log(j), 100))(i);
}
```

### 12. IIFE & Module Pattern
```js
// Immediately Invoked Function Expression
const result = (() => {
  const private = "secret";
  return { getPrivate: () => private };
})();
result.getPrivate(); // "secret"
```

---

## Phase 4 — Asynchronous JavaScript

### 13. Event Loop & Call Stack
```js
// JS is single-threaded. Event loop processes:
// 1. Call stack (sync code)
// 2. Microtask queue (Promises, queueMicrotask)
// 3. Macrotask queue (setTimeout, setInterval, I/O)

console.log("1");
setTimeout(() => console.log("2"), 0);
Promise.resolve().then(() => console.log("3"));
console.log("4");
// Output: 1, 4, 3, 2  (microtask runs before macrotask)
```

### 14. Callbacks
```js
// Old pattern — "callback hell"
getUser(id, (user) => {
  getPosts(user.id, (posts) => {
    getComments(posts[0].id, (comments) => {
      console.log(comments); // deeply nested
    });
  });
});
```

### 15. Promises
```js
// Promise: pending → fulfilled | rejected
const fetchUser = (id) =>
  new Promise((resolve, reject) => {
    setTimeout(() => {
      if (id > 0) resolve({ id, name: "Alice" });
      else reject(new Error("Invalid ID"));
    }, 1000);
  });

fetchUser(1)
  .then(user => console.log(user))
  .catch(err => console.error(err))
  .finally(() => console.log("done"));

// Promise combinators
Promise.all([p1, p2, p3])        // wait all, fail fast on any rejection
Promise.allSettled([p1, p2])     // wait all, get all results regardless
Promise.race([p1, p2])           // first settled wins
Promise.any([p1, p2])            // first fulfilled wins (ignores rejections)
```

### 16. Async/Await
```js
// Syntactic sugar over Promises — cleaner, synchronous-looking code
async function loadUserData(id) {
  try {
    const user = await fetchUser(id);        // waits for promise
    const posts = await fetchPosts(user.id);
    return { user, posts };
  } catch (err) {
    console.error("Failed:", err.message);
    throw err; // re-throw if needed
  }
}

// Parallel execution (don't await sequentially if independent)
async function loadAll() {
  const [users, posts] = await Promise.all([fetchUsers(), fetchPosts()]);
  return { users, posts };
}

// Top-level await (ESM modules only)
const data = await fetch("/api/data").then(r => r.json());
```

---

## Phase 5 — Advanced Topics

### 17. Prototypes & Prototype Chain
```js
// Every object has __proto__ pointing to its prototype
function Person(name) { this.name = name; }
Person.prototype.greet = function() { return `Hi, I'm ${this.name}`; };

const alice = new Person("Alice");
alice.greet();               // found on prototype
alice.hasOwnProperty("name"); // true — own property
alice.hasOwnProperty("greet"); // false — on prototype

// Object.create for prototype delegation
const animal = { breathe() { return "breathing"; } };
const dog = Object.create(animal);
dog.bark = () => "woof";
dog.breathe(); // delegated to animal
```

### 18. `this` Keyword
```js
// this depends on HOW a function is called, not where defined

// Method call: this = the object
const obj = { name: "Alice", greet() { return this.name; } };

// Regular function call: this = undefined (strict) or window
function show() { console.log(this); }

// Arrow function: this = inherited from enclosing lexical scope
const timer = {
  count: 0,
  start() {
    setInterval(() => {
      this.count++; // `this` is timer, not the interval callback
    }, 1000);
  }
};

// Explicit binding
function greet(greeting) { return `${greeting}, ${this.name}`; }
greet.call({ name: "Alice" }, "Hello");        // call: immediate, args spread
greet.apply({ name: "Bob" }, ["Hi"]);          // apply: immediate, args array
const boundGreet = greet.bind({ name: "Eve" }); // bind: returns new function
```

### 19. Generators & Iterators
```js
function* idGenerator() {
  let id = 1;
  while (true) {
    yield id++;  // pauses here, resumes on next()
  }
}

const gen = idGenerator();
gen.next(); // { value: 1, done: false }
gen.next(); // { value: 2, done: false }

// Finite generator
function* range(start, end) {
  for (let i = start; i <= end; i++) yield i;
}
[...range(1, 5)]; // [1, 2, 3, 4, 5]
```

### 20. Proxy & Reflect
```js
// Proxy: intercept object operations
const handler = {
  get(target, key) {
    return key in target ? target[key] : `Property ${key} not found`;
  },
  set(target, key, value) {
    if (typeof value !== "number") throw new TypeError("Numbers only");
    target[key] = value;
    return true;
  }
};

const proxy = new Proxy({}, handler);
proxy.age = 25;
proxy.age;    // 25
proxy.name;   // "Property name not found"

// Reflect: complement to Proxy, mirrors object operations
Reflect.ownKeys(obj);
Reflect.has(obj, "key");
```

### 21. WeakMap, WeakSet, WeakRef
```js
// WeakMap: keys are weakly held (garbage collectible), no iteration
const cache = new WeakMap();
function processUser(user) {
  if (cache.has(user)) return cache.get(user);
  const result = expensiveOp(user);
  cache.set(user, result);
  return result;
}

// WeakRef: hold reference without preventing GC
const weakRef = new WeakRef(someObject);
const obj = weakRef.deref(); // may be undefined if GCed
```

---

## Phase 6 — Modern JavaScript (ES2020–2025)

### 22. ES2020
```js
// Optional chaining
const street = user?.address?.street;
const first = arr?.[0];
const result = obj?.method?.();

// Nullish coalescing
const port = config.port ?? 3000;

// BigInt
const big = 9007199254740991n + 1n;

// Promise.allSettled
const results = await Promise.allSettled([p1, p2, p3]);
results.forEach(r => console.log(r.status, r.value ?? r.reason));

// globalThis (works in browser, Node, workers)
globalThis.setTimeout(() => {}, 0);
```

### 23. ES2021
```js
// Logical assignment operators
x ||= "default";   // x = x || "default"
x &&= transform(x); // x = x && transform(x)
x ??= "fallback";  // x = x ?? "fallback"

// String.replaceAll
"hello world".replaceAll("o", "0"); // "hell0 w0rld"

// Promise.any
const first = await Promise.any([slowApi(), fastApi()]); // fastest fulfillment
```

### 24. ES2022
```js
// Class fields & private
class User {
  name = "default";     // public field
  #password;            // private field

  constructor(name, pass) {
    this.name = name;
    this.#password = pass;
  }

  #validate() { /* private method */ }

  static #count = 0;   // private static
  static getCount() { return User.#count; }
}

// at() method — negative indexing
[1, 2, 3].at(-1);    // 3
"hello".at(-1);       // "o"

// Object.hasOwn (replaces hasOwnProperty)
Object.hasOwn(obj, "key"); // true/false

// Top-level await in ESM
const data = await fetch("/api").then(r => r.json());

// Error cause
throw new Error("Failed to fetch", { cause: originalError });
```

### 25. ES2023
```js
// Array methods: findLast, findLastIndex
[1, 2, 3, 4].findLast(n => n % 2 === 0); // 4

// toSorted, toReversed, toSpliced, with — non-mutating array ops
const sorted = [3, 1, 2].toSorted();      // new array, original unchanged
const reversed = [1, 2, 3].toReversed();
const updated = [1, 2, 3].with(1, 99);   // [1, 99, 3]

// Hashbang grammar: #!/usr/bin/env node at top of files
```

### 26. ES2024
```js
// Promise.withResolvers: expose resolve/reject outside constructor
const { promise, resolve, reject } = Promise.withResolvers();
setTimeout(() => resolve("done"), 1000);
await promise;

// Object.groupBy / Map.groupBy
const grouped = Object.groupBy(items, item => item.category);
// { "food": [...], "tech": [...] }

// ArrayBuffer.resize, SharedArrayBuffer improvements
// RegExp /v flag (set notation in character classes)
const re = /[\p{Script=Greek}&&\p{Letter}]/v;
```

### 27. ES2025 (Latest)
```js
// Iterator helpers — lazy chaining on iterators
function* naturals() { let n = 0; while (true) yield n++; }

const result = naturals()
  .filter(n => n % 2 === 0)
  .map(n => n * n)
  .take(5)
  .toArray(); // [0, 4, 16, 36, 64]

// Set operations
const a = new Set([1, 2, 3]);
const b = new Set([2, 3, 4]);
a.union(b);        // Set {1, 2, 3, 4}
a.intersection(b); // Set {2, 3}
a.difference(b);   // Set {1}
a.isSubsetOf(b);   // false

// Float16Array
const f16 = new Float16Array([1.5, 2.5]);

// Duplicate named capture groups in regex
const re = /(?<year>\d{4})-\d{2}|(?<year>\d{4})\.\d{2}/v;

// RegExp.escape (proposal)
const safe = RegExp.escape("hello.world"); // "hello\\.world"
```

---

## Phase 7 — Functional Programming Patterns

### 28. Array Methods
```js
const nums = [1, 2, 3, 4, 5];

nums.map(n => n * 2);           // [2, 4, 6, 8, 10] — transform
nums.filter(n => n % 2 === 0);  // [2, 4] — subset
nums.reduce((acc, n) => acc + n, 0); // 15 — accumulate
nums.find(n => n > 3);          // 4 — first match
nums.every(n => n > 0);         // true — all satisfy
nums.some(n => n > 4);          // true — any satisfies
nums.flat(2);                   // flatten nested arrays to depth 2
nums.flatMap(n => [n, n * 2]);  // map then flatten 1 level
```

### 29. Currying & Composition
```js
// Currying: transform f(a,b,c) into f(a)(b)(c)
const curry = (fn) => {
  const arity = fn.length;
  return function curried(...args) {
    if (args.length >= arity) return fn(...args);
    return (...more) => curried(...args, ...more);
  };
};

const add = curry((a, b, c) => a + b + c);
add(1)(2)(3); // 6
add(1, 2)(3); // 6

// Composition: pipe data through functions
const pipe = (...fns) => (x) => fns.reduce((v, f) => f(v), x);

const process = pipe(
  x => x * 2,
  x => x + 1,
  x => x.toString()
);
process(5); // "11"
```

### 30. Immutability
```js
// Spread for immutable updates
const state = { user: { name: "Alice", age: 30 }, count: 0 };

// Update nested immutably
const newState = {
  ...state,
  user: { ...state.user, age: 31 },
  count: state.count + 1
};

// Object.freeze (shallow)
const config = Object.freeze({ host: "localhost", port: 3000 });
config.port = 8080; // silently fails (throws in strict mode)
```

---

## Phase 8 — Error Handling & Patterns

### 31. Error Handling
```js
// Custom errors
class ValidationError extends Error {
  constructor(message, field) {
    super(message);
    this.name = "ValidationError";
    this.field = field;
  }
}

try {
  throw new ValidationError("Required", "email");
} catch (err) {
  if (err instanceof ValidationError) {
    console.log(err.field, err.message);
  } else {
    throw err; // re-throw unknown errors
  }
}

// Async error handling
async function safe(promise) {
  try {
    return [await promise, null];
  } catch (err) {
    return [null, err];
  }
}

const [data, err] = await safe(fetchUser(id));
if (err) { /* handle */ }
```

### 32. Design Patterns
```js
// Observer pattern
class EventEmitter {
  #listeners = new Map();

  on(event, fn) {
    if (!this.#listeners.has(event)) this.#listeners.set(event, []);
    this.#listeners.get(event).push(fn);
    return () => this.off(event, fn); // returns unsubscribe fn
  }

  emit(event, ...args) {
    this.#listeners.get(event)?.forEach(fn => fn(...args));
  }

  off(event, fn) {
    const fns = this.#listeners.get(event) ?? [];
    this.#listeners.set(event, fns.filter(f => f !== fn));
  }
}

// Singleton
class Config {
  static #instance;
  static getInstance() {
    Config.#instance ??= new Config();
    return Config.#instance;
  }
}
```

---

## Learning Order

| Week | Topics |
|------|--------|
| 1–2  | Phase 1: variables, types, functions, control flow |
| 3    | Phase 2: ES6+ (destructuring, modules, classes) |
| 4    | Phase 3: closures, scope, IIFE |
| 5–6  | Phase 4: event loop, callbacks, promises, async/await |
| 7    | Phase 5: prototypes, `this`, generators, proxy |
| 8    | Phase 6: ES2020–2025 features |
| 9–10 | Phase 7–8: FP patterns, error handling, design patterns |

## Resources

- **MDN Web Docs** — authoritative reference for all JS features
- **javascript.info** — best free deep-dive tutorial
- **You Don't Know JS (book series)** — deep understanding of closures, `this`, async
- **TC39 proposals** — github.com/tc39/proposals for what's coming next
- **Node.js docs** — for server-side JS environment specifics

## Practice Projects

1. **Todo app** — closures, DOM, events
2. **Fetch + async** — Promise chains, async/await, error handling
3. **Custom event system** — Observer pattern, WeakMap
4. **Lazy iterator pipeline** — generators, ES2025 iterator helpers
5. **Mini state manager** — proxy, immutability, pub/sub
