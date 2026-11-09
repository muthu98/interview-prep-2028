# Pydantic Validation Basics

## Day 22

Pydantic is new in this learning track, so the focus was on the basic mental model.

A Pydantic model defines request structure, types, and validation rules.

```python
from pydantic import BaseModel, Field
from typing import Literal

class TaskRequest(BaseModel):
    title: str = Field(min_length=3)
    status: Literal["TODO", "IN_PROGRESS", "COMPLETED"]
```

This can enforce:

- `title` is a string with at least 3 characters
- `status` is one of the allowed literal values

With FastAPI, validation happens before endpoint business logic runs.

Mental model:

```text
Client JSON
  -> FastAPI
  -> Pydantic validation
  -> valid: typed request object
  -> invalid: validation response
```

## Relation to Spring Boot

Pydantic request models play a role similar to Spring request DTOs plus validation annotations.

Exception handling remains a separate concern.
