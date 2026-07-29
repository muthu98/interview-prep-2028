# Closures

## Definition

A closure is a function that remembers variables from its lexical scope even after the outer function has finished executing.

---

## Example

```javascript
function outer() {
    let count = 0;

    return function () {
        count++;
        console.log(count);
    };
}
```

Output

```
1
2
3
```

---

## Independent Closures

```javascript
const c1 = outer();
const c2 = outer();

c1();
c1();

c2();

c1();
```

Output

```
1
2
1
3
```

---

## Key Points

- Lexical Scope
- Private Variables
- State Preservation
- Each invocation creates a new closure

---

## Real World Usage

- React Hooks
- Event Listeners
- Debounce
- Throttle
- Memoization