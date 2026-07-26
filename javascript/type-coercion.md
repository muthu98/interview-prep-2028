# JavaScript Type Coercion

## Equality Operators

```javascript
[] == false      // true
[] === false     // false

null == undefined    // true
null === undefined   // false
```

## Why?

### ==

Performs type coercion before comparison.

### ===

Compares both value and type without conversion.

## String and Number Operations

```javascript
"5" + 2   // "52"
"5" - 2   // 3
"5" * 2   // 10
"5" / 2   // 2.5
```

## Remember

* Prefer `===` over `==`.
* `+` performs string concatenation when one operand is a string.
* `-`, `*`, and `/` convert operands to numbers.
