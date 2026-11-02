# Section 2: Installation Of Anaconda And VS Code IDE

> **Udemy Section 2 of 27**: Installation Of Anaconda And VS Code IDE  
> **Lectures Covered**: Lecture 2 to Lecture 4  
> **Instructor**: Krish Naik  
> **Master Index**: [README.md](./README.md) | [00_Course_Overview_and_Roadmap.md](./00_Course_Overview_and_Roadmap.md)

---

> **Lectures Covered**: Lectures 2 – 4  

> **Overview**: Setting up professional Python environments for Data Science & AI development using both Anaconda/Conda and the high-performance Rust-based UV package manager.

---

## 📌 Core Concepts & Theoretical Foundations

- **Why Virtual Environments Matter**: Prevents dependency conflicts between open-source libraries (e.g. LangChain, LangGraph, PyTorch, CUDA).

- **Anaconda Ecosystem**: Manages binary packages and Python versions across Windows, macOS, and Linux.

- **Path Environment Variables**: Crucial paths required (`Anaconda3`, `Scripts`, `Library\bin`, `usr\bin`) so `conda` commands work globally in any terminal.

- **UV Package Manager (Astral)**: Written in Rust. 10x-100x faster than standard pip/conda. Uses universal lockfiles (`pyproject.toml` and `uv.lock`).


---

## 💻 Hands-on Code & Practical Implementation

```python
# Conda Commands
conda create -p ./venv python=3.12 -y
conda activate ./venv
pip install -r requirements.txt
conda deactivate

# UV Commands (Modern Rust-based workflow)
pip install uv
uv init my_agent_project
cd my_agent_project
uv venv --python 3.12
.venv\Scripts\activate
uv add langchain langgraph ipykernel

```

---

## 💡 Key Takeaways & Interview Preparation

1. **Core Problem Solved**: Focuses directly on mastering Environment Setup — Anaconda, Conda & UV Package Manager.

2. **Real-world Application**: Used as a foundational building block in production Agentic AI systems.


👉 [Back to Master Lecture Index](./README.md) | [Back to Master Roadmap](./00_Course_Overview_and_Roadmap.md)

---
👉 [Back to Master Lecture Index](./README.md) | [Back to Master Roadmap](./00_Course_Overview_and_Roadmap.md)
