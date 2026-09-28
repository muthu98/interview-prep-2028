# Python Basics for a JavaScript Developer

## Day 20 — Python Basics for a JavaScript Developer

| JavaScript | Python |
|---|---|
| Object used for key-value data | `dict` |
| Array | `list` |
| `push(item)` | `append(item)` for one item |
| `function` and braces | `def`, colon, and an indented body |
| `let` / `const` / `var` declaration | Assignment without those keywords |

Examples practiced:

```python
user = {
    "name": "Muthu",
    "age": 29
}

nums = [1, 2, 3]
nums.append(4)

def add(a, b):
    return a + b
```

Both languages are dynamically typed, but their syntax is not identical. String dictionary keys need quotes, indentation defines the function body, and semicolons are normally omitted.

### Status

- [x] Dictionary and list basics.
- [x] Append an item to a list.
- [x] Basic function syntax.
- [ ] Python type hints — next exercise introduced, not completed.
- [ ] FastAPI-oriented Python — future study.
