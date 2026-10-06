# Controlled vs Uncontrolled Components

## Day 21 — Scope

Completed controlled vs uncontrolled components only. Deeper form-performance topics were not completed.

- **Controlled:** React state supplies the input's current `value` (or `checked`), and an `onChange` handler updates that state.
- **Uncontrolled:** the DOM holds the current input value. Use `defaultValue` for an initial value and a ref or form submission to read the current value.

```jsx
// Controlled input, inside a component:
const [name, setName] = useState("");
<input value={name} onChange={event => setName(event.target.value)} />

// Uncontrolled input, inside a component:
const nameRef = useRef(null);
<input defaultValue="" ref={nameRef} />
// Read nameRef.current.value when needed.
```

Controlled inputs are useful when the UI must react to the current value; uncontrolled inputs are useful when values only need to be read on submission. Keep an input consistently controlled or uncontrolled during its lifetime.

## Revision

Explain who owns the current value and the difference between value and defaultValue. Form-performance optimization remains future work.

