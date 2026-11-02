# Section 4: Getting Started With Pydantic In Python

> **Udemy Section 4 of 27**: Getting Started With Pydantic In Python  
> **Lectures Covered**: Lecture 45 to Lecture 46  
> **Instructor**: Krish Naik  
> **Master Index**: [LECTURE_INDEX.md](./LECTURE_INDEX.md) | [00_Course_Overview_and_Roadmap.md](./00_Course_Overview_and_Roadmap.md)

---

> **Lectures Covered**: Lectures 45 – 46  

> **Overview**: Defining deterministic schemas with BaseModel, Field constraints, field_validators, and forcing LLMs to return typed structured outputs.

---

## 📌 Core Concepts & Theoretical Foundations

- **Why Pydantic in AI**: LLMs are probabilistic text generators. Real systems require typed JSON schemas for APIs, databases, and graph state.

- **BaseModel & Field**: Defining types, defaults, descriptions, and numeric/regex constraints.

- **Runtime Data Coercion**: Automatically validates and coerces incoming data types (e.g. string to integer).

- **Tool Calling Schemas**: Pydantic models automatically convert into JSON Schema specs accepted by OpenAI, Anthropic, and Groq function-calling APIs.


---

## 💻 Hands-on Code & Practical Implementation

```python
from pydantic import BaseModel, Field, field_validator

class SearchFilter(BaseModel):
    query: str = Field(description="Search keyword")
    max_results: int = Field(default=5, ge=1, le=20, description="1 to 20 results")
    allowed_domains: list[str] = Field(default_factory=list)

    @field_validator('query')
    @classmethod
    def query_not_empty(cls, v: str) -> str:
        if not v.strip():
            raise ValueError("Query cannot be blank")
        return v.strip()

# Structured output with ChatOpenAI
# structured_llm = llm.with_structured_output(SearchFilter)

```

---

## 💡 Key Takeaways & Interview Preparation

1. **Core Problem Solved**: Focuses directly on mastering Pydantic Data Validation & LLM Schema Enforcement.

2. **Real-world Application**: Used as a foundational building block in production Agentic AI systems.


👉 [Back to Master Lecture Index](./LECTURE_INDEX.md) | [Back to Master Roadmap](./00_Course_Overview_and_Roadmap.md)

---
👉 [Back to Master Lecture Index](./LECTURE_INDEX.md) | [Back to Master Roadmap](./00_Course_Overview_and_Roadmap.md)
