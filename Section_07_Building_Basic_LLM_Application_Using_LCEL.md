# Section 7: Building Basic LLM Application Using LCEL

> **Udemy Section 7 of 27**: Building Basic LLM Application Using LCEL  
> **Lectures Covered**: Lecture 66 to Lecture 68  
> **Instructor**: Krish Naik  
> **Master Index**: [LECTURE_INDEX.md](./LECTURE_INDEX.md) | [00_Course_Overview_and_Roadmap.md](./00_Course_Overview_and_Roadmap.md)

---

> **Lectures Covered**: Lecture 66 to Lecture 68  
> **Course Section**: Building Basic LLM Application Using LCEL  
> **Instructor**: Krish Naik  
> **Prerequisites**: [09_Document_Loaders_and_Text_Splitters.md](./09_Document_Loaders_and_Text_Splitters.md), [11_Ollama_Local_LLMs_and_LangSmith.md](./11_Ollama_Local_LLMs_and_LangSmith.md)  
> **Master Index**: [LECTURE_INDEX.md](./LECTURE_INDEX.md) | [00_Course_Overview_and_Roadmap.md](./00_Course_Overview_and_Roadmap.md)

---

## 📌 Executive Overview & Core Problem

Building a prototype in a Jupyter notebook is easy, but converting it into a production-grade backend service requires three architectural upgrades:
1. **Ultra-Low Latency Inference**: Using Language Processing Units (**Groq LPUs**) for instant ~500 tokens/sec open-source model inference.
2. **Unified Composition via LCEL (LangChain Expression Language)**: Using the Unix-style pipe operator (`|`) to bind Prompts, Models, and Output Parsers into a composable `Runnable`.
3. **One-Line Production Deployment (LangServe)**: Exposing any LangChain Runnable as a production **FastAPI REST API** with built-in streaming endpoints, Swagger UI documentation, and interactive playground widgets.

```mermaid
flowchart LR
    Client["Client App / Frontend"] -->|POST /chain/invoke| FastAPI["FastAPI Server + LangServe"]
    
    subgraph LCEL["Compiled LCEL Runnable Chain"]
        Prompt["ChatPromptTemplate"] -->|'|' Pipe| Groq["ChatGroq (Llama 3.3 70B)"]
        Groq -->|'|' Pipe| Parser["StrOutputParser"]
    end

    FastAPI --> LCEL
    LCEL -->|Streaming HTTP Response| Client
```

---

## 📖 Detailed Lecture-by-Lecture Walkthrough

---

### 🔹 Lecture 66: Getting Started With Open Source Models Using Groq API

#### 1. What makes Groq LPU Different from GPUs?
Traditional GPUs (NVIDIA H100 / A100) are optimized for parallel floating-point operations with high memory bandwidth bottlenecks. **Groq's LPU (Language Processing Unit)** uses a deterministic tensor streaming processor architecture that delivers up to **500–800 tokens per second** for models like Llama 3.3 70B.

#### 2. Setup & Installation
```bash
pip install langchain-groq python-dotenv
```

Acquire a free API key from [console.groq.com](https://console.groq.com) and add to `.env`:
```env
GROQ_API_KEY=gsk_...
```

#### 3. Initializing and Testing `ChatGroq`

```python
import os
from dotenv import load_dotenv
from langchain_groq import ChatGroq
from langchain_core.messages import HumanMessage, SystemMessage

load_dotenv()
os.environ["GROQ_API_KEY"] = os.getenv("GROQ_API_KEY")

# Initialize ChatGroq
llm = ChatGroq(
    model="llama-3.3-70b-versatile",
    temperature=0.3,
    max_tokens=1024
)

# Test simple invocation
messages = [
    SystemMessage(content="You are an expert AI software architect."),
    HumanMessage(content="Explain what LCEL is in two sentences.")
]

response = llm.invoke(messages)
print(response.content)
```

---

### 🔹 Lecture 67: Building LLM Prompt and StrOutputParser Chain with LCEL

#### 1. The Unix-Style Pipe Operator (`|`)
In traditional LangChain v0.1, developers used verbose classes like `LLMChain(llm=..., prompt=...)`. LCEL completely replaces this by implementing Python's `__or__` dunder method on all `Runnable` objects:

$$ \text{RunnableChain} = \text{Prompt} \mid \text{Model} \mid \text{Parser} $$

#### 2. The Role of `StrOutputParser`
By default, calling an LLM returns an `AIMessage` object containing metadata, token counts, and headers. `StrOutputParser` extracts strictly the text string from `.content`, sanitizing the output for downstream processing.

#### 3. Complete LCEL Chain Implementation

```python
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser

# 1. Define Prompt Template
prompt = ChatPromptTemplate.from_messages([
    ("system", "You are an expert linguistic translator. Translate the text into {target_language}."),
    ("human", "{user_text}")
])

# 2. Define Output Parser
parser = StrOutputParser()

# 3. Assemble LCEL Chain using the pipe operator
chain = prompt | llm | parser

# 4. Invoke the chain
result = chain.invoke({
    "target_language": "French",
    "user_text": "Hello, how are you today?"
})

print("Translation:", result)
# Output: "Bonjour, comment allez-vous aujourd'hui ?"
```

#### 4. Streaming Tokens in LCEL
Any LCEL chain inherits the `stream()` method automatically:
```python
for chunk in chain.stream({"target_language": "German", "user_text": "Artificial intelligence is changing software engineering."}):
    print(chunk, end="", flush=True)
```

---

### 🔹 Lecture 68: Deploy LangServe Runnable and Chains as a REST API

#### 1. What is LangServe?
LangServe is a library that takes any LCEL `Runnable` and turns it into a production-ready **FastAPI** web service with zero manual routing boilerplate.

Features auto-generated by LangServe:
- `/chain/invoke`: Standard synchronous POST endpoint.
- `/chain/stream`: Real-time Server-Sent Events (SSE) streaming endpoint.
- `/chain/batch`: Parallel batch inference endpoint.
- `/chain/playground`: Interactive web GUI testing page.
- `/docs`: OpenAPI / Swagger interactive schema documentation.

#### 2. Installation
```bash
pip install "langserve[all]" fastapi uvicorn
```

#### 3. Building the Deployment Server (`server.py`)

```python
import os
from dotenv import load_dotenv
from fastapi import FastAPI
from langchain_groq import ChatGroq
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser
from langserve import add_routes

load_dotenv()

# 1. Initialize FastAPI App
app = FastAPI(
    title="LangServe AI Translation & Summarization Service",
    version="1.0",
    description="Production REST API powered by Groq LPU and LCEL"
)

# 2. Define LLM & Chains
llm = ChatGroq(model="llama-3.3-70b-versatile", temperature=0)

# Chain 1: Translation Service
trans_prompt = ChatPromptTemplate.from_template("Translate the following into {language}: {text}")
trans_chain = trans_prompt | llm | StrOutputParser()

# Chain 2: Technical Summary Service
sum_prompt = ChatPromptTemplate.from_template("Summarize the following technical topic in 3 bullet points: {topic}")
sum_chain = sum_prompt | llm | StrOutputParser()

# 3. Mount Routes via LangServe
add_routes(
    app,
    trans_chain,
    path="/translate"
)

add_routes(
    app,
    sum_chain,
    path="/summarize"
)

# 4. Run Server
if __name__ == "__main__":
    import uvicorn
    uvicorn.run(app, host="127.0.0.1", port=8000)
```

#### 4. Consuming the API via `RemoteRunnable`
Clients can call this API without writing raw `requests.post()` boilerplate by using `RemoteRunnable`:

```python
from langserve import RemoteRunnable

# Connect to deployed LangServe API
remote_chain = RemoteRunnable("http://127.0.0.1:8000/translate")

# Call just like a local LCEL chain!
response = remote_chain.invoke({"language": "Spanish", "text": "Good morning, team!"})
print("Remote Output:", response)
```

---

## 💡 Production Best Practices & Architectural Takeaways

1. **Leverage Groq for Agent Internal Loops**:
   Agentic loops require multiple LLM calls per user request (Router $\rightarrow$ Tool Call $\rightarrow$ Reflection). Running standard models that take 4–6 seconds per call makes the UX unusable. Groq's sub-second inference makes multi-step agentic loops feel instantaneous.
2. **Mounting Custom Middleware in LangServe**:
   Because LangServe sits on standard FastAPI, you can mount CORS middleware, API key auth guards (`Depends`), rate limiters, and Prometheus metrics collectors directly onto the `FastAPI` app instance.

---

## ❓ Interview & Conceptual Questions

### Q1: How does LCEL fundamentally differ from legacy LangChain `LLMChain`?
> **Answer**: Legacy `LLMChain` was an imperative object-oriented wrapper with rigid execution methods. LCEL is a functional declarative interface adhering to the `Runnable` protocol. Every component implements unified methods (`invoke`, `stream`, `batch`, `ainvoke`, `astream`), enabling built-in streaming, parallel execution, and seamless deployment with zero glue code.

### Q2: What endpoints does `add_routes()` automatically mount in a FastAPI application?
> **Answer**: `add_routes(app, chain, path="/my-path")` automatically creates `/my-path/invoke`, `/my-path/batch`, `/my-path/stream`, `/my-path/stream_log`, `/my-path/playground/` (interactive browser GUI), and OpenAPI schema definitions visible under `/docs`.

---

👉 [Back to Master Lecture Index](./LECTURE_INDEX.md) | [Back to Master Roadmap](./00_Course_Overview_and_Roadmap.md)

---
👉 [Back to Master Lecture Index](./LECTURE_INDEX.md) | [Back to Master Roadmap](./00_Course_Overview_and_Roadmap.md)
