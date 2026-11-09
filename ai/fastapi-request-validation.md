# FastAPI Request Validation

## Day 23

A FastAPI endpoint can use a Pydantic model directly as its request-body contract.

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class TaskRequest(BaseModel):
    title: str
    status: str

@app.post("/tasks")
def create_task(task: TaskRequest):
    return task
```

Flow:

```text
Client JSON
  -> FastAPI
  -> Pydantic validates body
  -> valid: build TaskRequest and call endpoint
  -> invalid: return validation response before endpoint business logic
```

The important idea is that endpoint code can work with already-validated input.

This was introductory coverage only; deeper FastAPI error handling and production validation patterns remain future work.
