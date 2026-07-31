# JavaScript Hoisting

## What is Hoisting?

Hoisting is JavaScript's behavior of processing declarations before code execution.

---

## var

- Hoisted
- Initialized with `undefined`
- Accessible before initialization

Example

```javascript
console.log(a);

var a = 10;
```

Output

```
undefined
```

---

## let

- Hoisted
- Not initialized
- Exists inside the Temporal Dead Zone (TDZ)

Example

```javascript
console.log(a);

let a = 10;
```

Output

```
ReferenceError
```

---

## const

- Hoisted
- Not initialized
- Exists inside the Temporal Dead Zone (TDZ)

Example

```javascript
console.log(a);

const a = 10;
```

Output

```
ReferenceError
```

---

## Temporal Dead Zone (TDZ)

The period between entering a scope and initializing a `let` or `const` variable.

Accessing the variable during this period throws a `ReferenceError`.

---

## Function Declaration

```javascript
sayHello();

function sayHello() {
    console.log("Hello");
}
```

Output

```
Hello
```

Fully hoisted.

---

## Function Expression

```javascript
sayHello();

var sayHello = function () {
    console.log("Hello");
};
```

Output

```
TypeError: sayHello is not a function
```

---

## Learning

- `var`, `let`, and `const` are all hoisted.
- `let` and `const` remain in the TDZ until initialization.
- Function declarations are fully hoisted.
- Function expressions behave according to the variable used (`var`, `let`, or `const`).