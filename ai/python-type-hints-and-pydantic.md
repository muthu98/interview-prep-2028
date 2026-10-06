# Python Type Hints and Pydantic Basics

## Day 21 — Introductory Coverage

```python
def add(a: int, b: int) -> int:
    return a + b

names: list[str] = ["Muthu"]
counts: dict[str, int] = {"tasks": 1}
description: str | None = None
```

Type hints document intended types and help static tools; Python does not enforce them automatically at runtime. `str | None` permits a string or None. In a function parameter, a default such as `= None` is separately needed if callers may omit that argument.

## Pydantic BaseModel

```python
from pydantic import BaseModel

class TaskRequest(BaseModel):
    title: str
    description: str | None = None

task = TaskRequest(title="Study")
```

A BaseModel defines structured data and validates input when a model is constructed. Depending on field types/configuration, parsing can include coercion; do not equate it with strict type checking in every case.

## Connection to Spring DTO Validation

A Spring request DTO with validation annotations and a Pydantic model both describe accepted input. Spring applies constraints through validation integration such as `@Valid`; Pydantic validates during model construction. A plain Python type hint alone is not equivalent to runtime DTO validation.

Exception handling is separate: it determines what happens when validation or application operations fail. Day 21 covered type hints and BaseModel basics; it does not mark Python exception handling or FastAPI implementation complete.

## Revision

Write a typed function, a typed list/dictionary, and a model with a field that may be None and can be omitted. Explain compile/static checking versus runtime validation.

