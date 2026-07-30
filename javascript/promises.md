# JavaScript Promises

## What is a Promise?

A Promise is an object that represents the eventual completion or failure of an asynchronous operation.

---

## Promise States

- Pending
- Fulfilled
- Rejected

---

## resolve()

Marks the Promise as fulfilled and passes the value to `.then()`.

---

## reject()

Marks the Promise as rejected and passes the error to `.catch()`.

---

## .then()

Executes when the Promise is fulfilled.

---

## .catch()

Handles rejected Promises and errors.

---

## .finally()

Executes regardless of whether the Promise is fulfilled or rejected.

---

## Promise Chaining

Allows multiple asynchronous operations to execute sequentially using multiple `.then()` calls.

---

## Important Points

- Promise settles only once.
- Pending → Fulfilled
- Pending → Rejected
- Cannot change state after settlement.