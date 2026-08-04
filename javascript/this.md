# JavaScript - this

## What is this?

`this` refers to the object that is executing the current function.

Its value depends on **how the function is called**.

---

## Global Scope

Browser:

```javascript
console.log(this);
```

Output:

```
window
```

---

## Regular Function

```javascript
function test() {
    console.log(this);
}
```

Non Strict

```
window
```

Strict Mode

```
undefined
```

---

## Object Method

```javascript
const obj = {
    name: "Muthu",
    greet() {
        console.log(this.name);
    }
};
```

Output

```
Muthu
```

---

## Arrow Function

Arrow functions do not have their own `this`.

They inherit `this` from the surrounding scope.

---

# call()

Immediately invokes the function.

```javascript
greet.call(obj, "Chennai");
```

---

# apply()

Immediately invokes the function.

Arguments are passed as an array.

```javascript
greet.apply(obj, ["Chennai"]);
```

---

# bind()

Returns a new function.

```javascript
const fn = greet.bind(obj);

fn();
```

---

# Interview Tips

- `call()` → invoke immediately
- `apply()` → invoke immediately using array arguments
- `bind()` → returns a new function