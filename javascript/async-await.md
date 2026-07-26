# Async / Await

## Rule 1
Every async function returns a Promise.

## Rule 2
await waits for a Promise and returns the resolved value.

## Example

```javascript
async function demo() {
    return 5;
}

console.log(demo());      // Promise { 5 }
console.log(await demo()); // 5
```

## Equivalent

```javascript
function demo() {
    return Promise.resolve(5);
}
```

## Remember
await pauses only the current async function.
It does NOT block the JavaScript thread.