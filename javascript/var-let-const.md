# var vs let vs const

- **Category:** JavaScript Fundamentals
- **Importance:** ⭐⭐⭐⭐⭐

---

# Overview

JavaScript provides three ways to declare variables:

- `var`
- `let`
- `const`

Choosing the correct one is important for writing predictable and maintainable code.

---

# Comparison

| Feature | var | let | const |
|---------|-----|-----|-------|
| Scope | Function | Block | Block |
| Reassign | ✅ Yes | ✅ Yes | ❌ No |
| Redeclare | ✅ Yes | ❌ No | ❌ No |
| Hoisted | ✅ Yes | ✅ Yes | ✅ Yes |
| Temporal Dead Zone | ❌ No | ✅ Yes | ✅ Yes |

---

# Scope

## var

```javascript
if (true) {
    var message = "Hello";
}

console.log(message);
```

Output

```text
Hello
```

Reason:

`var` is function-scoped.

---

## let

```javascript
if (true) {
    let message = "Hello";
}

console.log(message);
```

Output

```text
ReferenceError
```

Reason:

`let` is block-scoped.

---

## const

```javascript
if (true) {
    const message = "Hello";
}

console.log(message);
```

Output

```text
ReferenceError
```

Reason:

`const` is also block-scoped.

---

# Example 1

```javascript
for (var i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 0);
}
```

Output

```text
3
3
3
```

### Why?

- `var` is function-scoped.
- Only one variable `i` exists.
- The loop finishes first.
- When callbacks execute, `i` is already `3`.

---

# Example 2

```javascript
for (let i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 0);
}
```

Output

```text
0
1
2
```

### Why?

`let` creates a new block-scoped variable for every iteration.

Each callback remembers its own value.

---

# const with Arrays

```javascript
const arr = [1, 2, 3];

arr.push(4);

console.log(arr);
```

Output

```text
[1, 2, 3, 4]
```

Reason:

The array itself is modified.

The variable is not reassigned.

---

# Reassigning const

```javascript
const arr = [1, 2, 3];

arr = [5];
```

Output

```text
TypeError: Assignment to constant variable.
```

Reason:

`const` variables cannot be reassigned.

---

# const with Objects

```javascript
const person = {
    name: "Muthu"
};

person.name = "Kumar";

console.log(person);
```

Output

```javascript
{
    name: "Kumar"
}
```

Reason:

Object properties can be modified.

The reference cannot be changed.

---

# Hoisting

```javascript
console.log(a);

var a = 10;
```

Output

```text
undefined
```

---

```javascript
console.log(a);

let a = 10;
```

Output

```text
ReferenceError
```

---

```javascript
console.log(a);

const a = 10;
```

Output

```text
ReferenceError
```

---

# Key Learnings

## var

- Function-scoped
- Can redeclare
- Can reassign
- Avoid in modern JavaScript

---

## let

- Block-scoped
- Can reassign
- Cannot redeclare in the same scope

---

## const

- Block-scoped
- Cannot reassign
- Objects and arrays can still be modified

---

# Common Interview Questions

### Why does `var` print `3 3 3`?

Because all callbacks share the same variable.

---

### Why does `let` print `0 1 2`?

Each loop iteration gets a new block-scoped variable.

---

### Can a `const` object be modified?

✅ Yes.

Its properties can change.

---

### Can a `const` variable be reassigned?

❌ No.

---

### Difference between `const` and immutable?

`const` makes the variable reference immutable.

It does **not** make the object or array immutable.

---

# Best Practices

✅ Prefer `const` by default.

✅ Use `let` only when reassignment is needed.

❌ Avoid `var` in modern JavaScript.

---

# Revision Notes

- `var` → Function Scope
- `let` → Block Scope
- `const` → Block Scope + No Reassignment
- `const` objects and arrays are mutable.
- `let` creates a new binding for each loop iteration.