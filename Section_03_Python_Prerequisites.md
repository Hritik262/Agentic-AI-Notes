# Section 3: Python Prerequisites

> **Udemy Section 3 of 27**: Python Prerequisites  
> **Lectures Covered**: Lecture 5 to Lecture 44  
> **Instructor**: Krish Naik  
> **Master Index**: [README.md](./README.md) | [00_Course_Overview_and_Roadmap.md](./00_Course_Overview_and_Roadmap.md)

---

> **Lectures Covered**: Lectures 5 – 16  

> **Overview**: Core syntax, semantics, data types, operators, loops, lists, sets, dictionaries, and tuples necessary for manipulating LLM inputs and state objects.

---

## 📌 Core Concepts & Theoretical Foundations

- **Syntax vs Semantics**: Syntax is the grammatical arrangement of words/symbols; semantics is the runtime meaning and execution behavior.

- **Dynamic Typing & Variables**: Variables don't need explicit type declarations, but type hints (`str`, `int`, `list[str]`) are strongly recommended in agent workflows.

- **List Comprehensions**: Highly efficient syntax for transforming LLM outputs and message lists: `[msg.content for msg in messages]`.

- **Dictionaries & State**: Key-value pairs form the fundamental data structure for agent state, tool arguments, and JSON payloads.

- **Sets & Tuples**: Sets ensure uniqueness (e.g. unique tool names or URLs visited); tuples provide immutable records.


---

## 💻 Hands-on Code & Practical Implementation

```python
# Core Collections Example
documents = ["doc1: LangChain intro", "doc2: LangGraph nodes", "doc3: LangChain agents"]

# List comprehension: Extract document titles
titles = [doc.split(":")[0] for doc in documents if "Lang" in doc]

# Dictionary: Agent State Representation
agent_state = {
    "session_id": "user_101",
    "turn": 3,
    "tools_used": {"tavily_search", "calculator"},  # Set for uniqueness
    "config": ("temperature=0.2", "model=gpt-4o-mini")  # Immutable tuple
}

```

---

## 💡 Key Takeaways & Interview Preparation

1. **Core Problem Solved**: Focuses directly on mastering Python Basics & Core Data Structures.

2. **Real-world Application**: Used as a foundational building block in production Agentic AI systems.


👉 [Back to Master Lecture Index](./README.md) | [Back to Master Roadmap](./00_Course_Overview_and_Roadmap.md)


---


> **Lectures Covered**: Lectures 17 – 23  

> **Overview**: Writing reusable modular code using functions, *args/**kwargs, anonymous lambda functions, map/filter pipelines, and package structures.

---

## 📌 Core Concepts & Theoretical Foundations

- **Function Arguments (*args, **kwargs)**: Allows agent tools and node handlers to accept variable inputs dynamically.

- **Lambda & Higher-Order Functions**: One-line functions passed into sorting, map, and filter utilities.

- **Map & Filter Pipelines**: Functional data transformation for filtering relevant context chunks from retrieved documents.

- **Modular Packages**: Structuring code with `__init__.py` and imports (`from my_module import AgentNode`).


---

## 💻 Hands-on Code & Practical Implementation

```python
# Variable arguments in agent tool wrappers
def execute_tool(tool_name: str, *args, **kwargs):
    print(f"Executing {tool_name} with positional args: {args} and kwargs: {kwargs}")

# Filter relevant docs using lambda
docs = [
    {"id": 1, "score": 0.85, "text": "LangGraph tutorial"},
    {"id": 2, "score": 0.40, "text": "Unrelated document"},
    {"id": 3, "score": 0.92, "text": "Agentic workflows"}
]
relevant_docs = list(filter(lambda d: d["score"] > 0.7, docs))
print(f"Filtered {len(relevant_docs)} high-relevance docs.")

```

---

## 💡 Key Takeaways & Interview Preparation

1. **Core Problem Solved**: Focuses directly on mastering Functions, Functional Programming & Modules.

2. **Real-world Application**: Used as a foundational building block in production Agentic AI systems.


👉 [Back to Master Lecture Index](./README.md) | [Back to Master Roadmap](./00_Course_Overview_and_Roadmap.md)


---


> **Lectures Covered**: Lectures 24 – 26, 34  

> **Overview**: Safe file handling, cross-platform path management with pathlib, and building custom exception classes to catch agent execution and tool failures.

---

## 📌 Core Concepts & Theoretical Foundations

- **Safe File I/O (`with open`)**: Guarantees file descriptors are automatically closed even if errors occur during reading/writing.

- **`pathlib.Path`**: Object-oriented cross-platform paths that work seamlessly across Windows backslashes and Unix forward slashes.

- **Exception Hierarchies (try-except-finally)**: Catching network errors and formatting errors gracefully.

- **Custom Exception Classes**: Subclassing `Exception` to build domain-specific error handling for agentic tool calls.


---

## 💻 Hands-on Code & Practical Implementation

```python
from pathlib import Path

# Cross-platform path handling
log_dir = Path("logs") / "agents"
log_dir.mkdir(parents=True, exist_ok=True)
log_file = log_dir / "execution.log"

# Custom Exception for Agent Tool Failures
class ToolExecutionError(Exception):
    def __init__(self, tool_name: str, reason: str):
        self.tool_name = tool_name
        self.reason = reason
        super().__init__(f"Tool [{tool_name}] failed: {reason}")

try:
    raise ToolExecutionError("TavilySearch", "Rate limit exceeded (HTTP 429)")
except ToolExecutionError as e:
    print(f"Fallback triggered: {e}")

```

---

## 💡 Key Takeaways & Interview Preparation

1. **Core Problem Solved**: Focuses directly on mastering File Operations, Pathlib & Custom Exception Handling.

2. **Real-world Application**: Used as a foundational building block in production Agentic AI systems.


👉 [Back to Master Lecture Index](./README.md) | [Back to Master Roadmap](./00_Course_Overview_and_Roadmap.md)


---


> **Lectures Covered**: Lectures 27 – 33  

> **Overview**: Classes, inheritance, polymorphism, encapsulation, abstraction, and magic methods (`__init__`, `__call__`, `__repr__`) in modern AI frameworks.

---

## 📌 Core Concepts & Theoretical Foundations

- **Classes & Instances**: The foundation of tools, models, state objects, and checkpointers in LangChain/LangGraph.

- **Inheritance & Subclassing**: Inheriting from `BaseTool` or `BaseChatModel` to implement custom agent tools.

- **Polymorphism**: Common `.invoke()` and `.stream()` methods across OpenAI, Anthropic, and Groq models.

- **Magic Dunder Methods**: `__call__` allows an instantiated object to be called as a function (used extensively by LangChain Runnables).


---

## 💻 Hands-on Code & Practical Implementation

```python
# Custom Tool class using OOPS and __call__
class CustomAgentTool:
    def __init__(self, name: str, description: str):
        self.name = name
        self.description = description

    def __call__(self, query: str) -> str:
        # __call__ allows: tool("search query")
        return f"Tool [{self.name}] processed query: '{query}'"

    def __repr__(self) -> str:
        return f"CustomAgentTool(name='{self.name}')"

tool = CustomAgentTool("SQLRetriever", "Queries SQL DB")
print(tool)
print(tool("SELECT * FROM users"))

```

---

## 💡 Key Takeaways & Interview Preparation

1. **Core Problem Solved**: Focuses directly on mastering Object-Oriented Programming (OOPS) & Magic Methods.

2. **Real-world Application**: Used as a foundational building block in production Agentic AI systems.


👉 [Back to Master Lecture Index](./README.md) | [Back to Master Roadmap](./00_Course_Overview_and_Roadmap.md)


---


> **Lectures Covered**: Lectures 35 – 37  

> **Overview**: Memory-efficient data pipelines, generator functions with yield for token-by-token streaming, and function decorators (@tool, @functools).

---

## 📌 Core Concepts & Theoretical Foundations

- **Iterators (`__iter__`, `__next__`)**: Sequential access to data without loading entire datasets into RAM.

- **Generators & `yield`**: Yielding values on the fly. This is the underlying Python mechanism that powers LLM token streaming (`stream()`).

- **Decorators (`@wrapper`)**: Functions that wrap other functions (e.g., adding logging, retry policies, or registering functions as tools via `@tool`).


---

## 💻 Hands-on Code & Practical Implementation

```python
import time
from functools import wraps

# Decorator to measure tool execution latency
def time_execution(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        duration = time.time() - start
        print(f"[{func.__name__}] executed in {duration:.4f}s")
        return result
    return wrapper

# Generator yielding streaming tokens
def stream_llm_tokens(sentence: str):
    for word in sentence.split():
        yield word + " "

@time_execution
def run_stream():
    for token in stream_llm_tokens("LangGraph enables cycle-driven stateful agent workflows"):
        print(token, end="", flush=True)
    print()

run_stream()

```

---

## 💡 Key Takeaways & Interview Preparation

1. **Core Problem Solved**: Focuses directly on mastering Iterators, Generators, Yield & Decorators.

2. **Real-world Application**: Used as a foundational building block in production Agentic AI systems.


👉 [Back to Master Lecture Index](./README.md) | [Back to Master Roadmap](./00_Course_Overview_and_Roadmap.md)


---


> **Lectures Covered**: Lectures 38 – 44  

> **Overview**: Data manipulation with NumPy arrays and Pandas DataFrames, and configuring multi-handler loggers for enterprise AI observability.

---

## 📌 Core Concepts & Theoretical Foundations

- **NumPy Vector Operations**: Used internally for calculating embedding similarity (cosine distance, dot products).

- **Pandas DataFrames**: Ingesting, cleaning, and transforming tabular datasets before passing them to RAG pipelines or SQL agents.

- **Multi-Logger Architecture**: Logging critical INFO statements to the console while writing DEBUG-level traces with line numbers to log files.


---

## 💻 Hands-on Code & Practical Implementation

```python
import logging
import sys

# Configure multi-handler logger
logger = logging.getLogger("AgenticApp")
logger.setLevel(logging.DEBUG)

# Console Handler (INFO)
c_handler = logging.StreamHandler(sys.stdout)
c_handler.setLevel(logging.INFO)
c_handler.setFormatter(logging.Formatter('%(asctime)s - [%(levelname)s] - %(message)s'))

# File Handler (DEBUG)
f_handler = logging.FileHandler("agent.log", encoding="utf-8")
f_handler.setLevel(logging.DEBUG)
f_handler.setFormatter(logging.Formatter('%(asctime)s - [%(name)s:%(levelname)s] - %(filename)s:%(lineno)d - %(message)s'))

logger.addHandler(c_handler)
logger.addHandler(f_handler)

logger.info("Agent started successfully.")
logger.debug("State initialized with keys: [messages, sender, turn]")

```

---

## 💡 Key Takeaways & Interview Preparation

1. **Core Problem Solved**: Focuses directly on mastering NumPy, Pandas & Production Multi-Logger Setup.

2. **Real-world Application**: Used as a foundational building block in production Agentic AI systems.


👉 [Back to Master Lecture Index](./README.md) | [Back to Master Roadmap](./00_Course_Overview_and_Roadmap.md)

---
👉 [Back to Master Lecture Index](./README.md) | [Back to Master Roadmap](./00_Course_Overview_and_Roadmap.md)
