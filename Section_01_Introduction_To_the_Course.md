# Section 1: Introduction To the Course

> **Udemy Section 1 of 27**: Introduction To the Course  
> **Lectures Covered**: Lecture 1 to Lecture 1  
> **Instructor**: Krish Naik  
> **Master Index**: [README.md](./README.md) | [00_Course_Overview_and_Roadmap.md](./00_Course_Overview_and_Roadmap.md)

---

# 🗺️ Master Agentic AI Curriculum: 31 Specific Topic Modules

> **Course Instructor**: Krish Naik  
> **Course**: Complete Agentic AI Bootcamp With LangGraph and Langchain  
> **Repository Workspace**: `d:\Learnings\CompleteAgenticAI\UDemy Final\Langchain`

---

## 📑 Complete 31-Topic Syllabus & Direct Links

Every single lecture is mapped to its dedicated, bite-sized topic document below:

### Part 1: Python & Environment Foundations
1. [**Topic 01: Environment Setup (Conda vs UV)**](./01_Environment_Setup_Conda_UV.md) — *Lectures 2–4* (Anaconda, Conda vs UV rust package manager).
2. [**Topic 02: Python Basics & Core Data Structures**](./02_Python_Basics_and_Data_Structures.md) — *Lectures 5–16* (Syntax, operators, conditionals, loops, lists, sets, dicts, tuples).
3. [**Topic 03: Functions & Functional Programming**](./03_Python_Functions_and_Modules.md) — *Lectures 17–23* (Args/kwargs, lambda, map, filter, modules, stdlib).
4. [**Topic 04: File Operations & Custom Exceptions**](./04_File_Operations_and_Exceptions.md) — *Lectures 24–26, 34* (File I/O, pathlib, try/except, custom agent error classes).
5. [**Topic 05: OOPS & Dunder Magic Methods**](./05_OOPS_and_Magic_Methods.md) — *Lectures 27–33* (Inheritance, polymorphism, encapsulation, `__call__`, dunder methods).
6. [**Topic 06: Iterators, Generators & Token Streaming**](./06_Iterators_Generators_Decorators.md) — *Lectures 35–37* (Iterators, `yield` for token streaming, closures, decorators).
7. [**Topic 07: NumPy, Pandas & Multi-Logger Setup**](./07_NumPy_Pandas_and_Logging.md) — *Lectures 38–44* (Arrays, DataFrames, file ingestion, production multi-logger logging).
8. [**Topic 08: Pydantic & LLM Data Validation**](./08_Pydantic_and_Data_Validation.md) — *Lectures 45–46* (BaseModel, Field, validators, structured output schemas).

### Part 2: LangChain Core, Vectors & Memory
9. [**Topic 09: Document Loaders & Text Splitters**](./09_Document_Loaders_and_Text_Splitters.md) — *Lectures 47–54* (Recursive, character, HTML header, JSON splitters).
10. [**Topic 10: Embeddings & Vector Stores (FAISS & ChromaDB)**](./10_Embeddings_and_Vector_Stores.md) — *Lectures 55–62* (OpenAI/Ollama/HF embeddings, FAISS in-memory, ChromaDB).
11. [**Topic 11: Local Ollama LLMs & LangSmith Tracing**](./11_Ollama_Local_LLMs_and_LangSmith.md) — *Lectures 63–65* (Local open-source models, LangSmith tracing & debugging).
12. [**Topic 12: LCEL Pipe Syntax, Groq LPU & LangServe**](./12_LCEL_Groq_LPU_and_LangServe.md) — *Lectures 66–68* (Unix pipe `|` chains, Groq LPU 500+ tokens/sec, LangServe REST APIs).
13. [**Topic 13: Chatbot Memory & Conversation History**](./13_Chatbot_Memory_and_History.md) — *Lectures 69–72* (ChatMessageHistory, MessagesPlaceholder, RunnableWithMessageHistory).
14. [**Topic 14: AI Agents vs Agentic AI Systems**](./14_AI_Agents_vs_Agentic_AI.md) — *Lectures 73–74* (Architectural comparison, autonomy spectrum, state machine design).
15. [**Topic 15: LangChain v1, Structured Output & Middlewares**](./15_LangChain_v1_and_Middlewares.md) — *Lectures 75–86* (v1 overhaul, `@tool`, message types, summarization & HITL middlewares).

### Part 3: LangGraph Core Architectures
16. [**Topic 16: LangGraph StateGraph, Nodes & Edges**](./16_LangGraph_Fundamentals.md) — *Lectures 87–94* (Introduction, environment, API keys, StateGraph, first graph chatbot).
17. [**Topic 17: LangGraph State Schemas & Routers**](./17_LangGraph_State_and_Routers.md) — *Lectures 95–98* (Pydantic/Dataclass state, reducers, conditional routing).
18. [**Topic 18: Tools Binding & ToolNode Execution**](./18_Tools_Integration_and_ToolNode.md) — *Lectures 99–102* (Binding tools, ToolNode, tool message synchronization).
19. [**Topic 19: ReAct Pattern Architecture from Scratch**](./19_ReAct_Agent_from_Scratch.md) — *Lectures 103–104* (Reasoning + Acting loop, custom ReAct implementation).
20. [**Topic 20: Memory Checkpointers, Streaming & Studio**](./20_LangGraph_Memory_and_Streaming.md) — *Lectures 105–108* (MemorySaver, `thread_id`, `astream_events` v2, LangGraph Studio).

### Part 4: Workflows, Human-in-the-Loop & Advanced RAG
21. [**Topic 21: The 5 Core Agentic Workflows**](./21_Agentic_Workflows_5_Design_Patterns.md) — *Lectures 109–115* (Prompt Chaining, Parallelization, Routing, Orchestrator-Worker, Evaluator-Optimizer).
22. [**Topic 22: Human-in-the-Loop (HITL) in LangGraph**](./22_Human_In_The_Loop_HITL.md) — *Lectures 116–119* (Static breakpoints, state editing, resuming, runtime `interrupt()`).
23. [**Topic 23: Advanced RAG (Agentic, CRAG, Adaptive, Vectorless)**](./23_Advanced_RAG_CRAG_Adaptive_Vectorless.md) — *Lectures 120–128* (Agentic RAG, Corrective RAG with Tavily fallback, Adaptive RAG, Vectorless RAG).
24. [**Topic 24: Safety Guardrails & Enterprise LLM Gateways**](./24_Guardrails_and_LLM_Gateways.md) — *Lectures 129–130* (Input/output sanitization, PII masking, LiteLLM/Portkey gateways, caching).

### Part 5: End-to-End Production Projects
25. [**Topic 25: Project 1 — Streamlit LangGraph Agent with Tools**](./25_Project_1_Streamlit_LangGraph_Chatbot.md) — *Lectures 131–140* (Modular structure, frontend UI, graph builder, testing).
26. [**Topic 26: Project 2 — Real-Time Web Search Agent (Tavily)**](./26_Project_2_Web_Search_Agent_Tavily.md) — *Lectures 141–144* (TavilySearchResults, live web search agent loop).
27. [**Topic 27: Project 3 — Autonomous AI News Summarizer**](./27_Project_3_AI_News_Summarizer.md) — *Lectures 145–151* (Automated news pipeline, structured summarizer, markdown export).
28. [**Topic 28: Project 4 — Multi-Language Blog Engine (FastAPI)**](./28_Project_4_Blog_Generator_FastAPI.md) — *Lectures 152–161* (Multi-stage drafting, translation, FastAPI REST API, Studio).

### Part 6: Next-Gen Tooling (MCP, Claude Code & Deep Agents)
29. [**Topic 29: Model Context Protocol (MCP) Standard**](./29_Model_Context_Protocol_MCP.md) — *Lectures 162–167* (JSON-RPC protocol, Claude Desktop, Cursor, Smithery AI).
30. [**Topic 30: Claude Code CLI, Agents & Agent Teams**](./30_Claude_Code_CLI_and_Agent_Teams.md) — *Lectures 169–175* (CLI terminal agent, agent views, agent teams, hooks, plugins).
31. [**Topic 31: Deep Agents with LangChain & Backends**](./31_Deep_Agents_with_LangChain.md) — *Lectures 176–183* (Virtual File System, swappable backends, context engineering, subagents, capstone).

---

👉 [**Open Master 1-to-1 Lecture Index**](./README.md)

---
👉 [Back to Master Lecture Index](./README.md) | [Back to Master Roadmap](./00_Course_Overview_and_Roadmap.md)
