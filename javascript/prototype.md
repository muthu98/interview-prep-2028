# Prototype & Prototype Chain

## What is a Prototype?

A prototype is an object that another object delegates to for properties and methods.

Objects do not copy methods from their prototype; instead, they maintain a reference to it.

---

## Prototype Chain

When JavaScript cannot find a property on an object, it searches:

Object

↓

Prototype

↓

Parent Prototype

↓

Object.prototype

↓

null

---

## Property Lookup

```javascript
const person = {
    name: "Muthu"
};

console.log(person.toString());
```

Output

```
[object Object]
```

Explanation:

`person` does not contain `toString()`.

JavaScript finds it on `Object.prototype`.

---

## __proto__ vs prototype

### prototype

Belongs to constructor functions.

```javascript
Person.prototype
```

---

### __proto__

Belongs to object instances.

```javascript
obj.__proto__
```

Usually

```javascript
obj.__proto__ === Person.prototype
```

---

## Object.create()

Creates a new object linked to another object through the prototype chain.

---

## How new Works

1. Create a new object.
2. Link it to the constructor's prototype.
3. Bind `this`.
4. Execute the constructor.
5. Return the object.

---

## Constructor vs Class

Classes are syntactic sugar over prototype-based inheritance.

Methods declared inside a class are stored on the class prototype.

---

## Interview Questions

- What is a prototype?
- What is prototype chaining?
- How does property lookup work?
- Difference between `prototype` and `__proto__`?
- How does `new` work internally?
- Does class replace prototypes?

Answer:

No. Classes use prototypes internally.