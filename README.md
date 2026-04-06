# 🧠 LangChain Prompt Templates — A Practical Guide

> A hands-on Jupyter notebook exploring **LangChain's prompt templating system** — from simple string templates to structured multi-turn chat prompts.

---

## 📖 Description

This notebook walks through the core prompt engineering primitives in LangChain, showing how to construct, format, and invoke prompts before sending them to a language model. It covers three levels of abstraction — basic string templates, chat templates, and typed message templates — and demonstrates how each one formats its output differently.

By the end of the notebook, you'll have a clear mental model of how LangChain structures prompts under the hood, and how to chain them with an OpenAI LLM using LCEL (LangChain Expression Language).

---

## 🗂️ Contents

```
prompt_template.ipynb
```

| Section | Topic |
|---|---|
| 1 | `PromptTemplate` — basic string templates with `{variables}` |
| 2 | `ChatPromptTemplate.from_template()` — single-turn chat prompts |
| 3 | `ChatPromptTemplate.from_messages()` — multi-turn prompts with few-shot examples |
| 4 | Typed templates — `SystemMessagePromptTemplate`, `HumanMessagePromptTemplate`, `AIMessagePromptTemplate` |
| 5 | LCEL `.invoke()` and connecting to OpenAI `gpt-4o-mini` |

---

## 🚀 Getting Started

### Prerequisites

- Python 3.9+
- Jupyter Notebook or JupyterLab
- An OpenAI API key

### Installation

```bash
pip install langchain langchain-core langchain-openai openai
```

### Setup

Place your OpenAI API key in a file at:

```
keys/.openai_api_key.txt
```

Then launch the notebook:

```bash
jupyter notebook prompt_template.ipynb
```

---

## 🧩 Key Concepts Covered

### `PromptTemplate`
Basic string-based templates with named `{variable}` placeholders. Returns a plain string on `.format()`.

```python
from langchain_core.prompts import PromptTemplate

template = PromptTemplate.from_template("Tell me {adjective} joke about {content}")
template.format(adjective="funny", content="travel")
# → "Tell me funny joke about travel"
```

### `ChatPromptTemplate`
Structured chat prompts supporting `system`, `human`, and `ai` roles. Three output methods:

| Method | Returns |
|---|---|
| `.format()` | `str` |
| `.format_messages()` | `list[BaseMessage]` |
| `.format_prompt()` | `ChatPromptValue` |

```python
from langchain_core.prompts import ChatPromptTemplate

chat = ChatPromptTemplate.from_messages([
    ("system", "You are a helpful AI bot. Your name is {botname}"),
    ("human", "Hello, how are you doing today?"),
    ("ai", "I am doing well, Thanks!"),
    ("human", "{user_input}")
])

chat.format_messages(botname="Chitti", user_input="Let's play")
```

### Typed Message Templates
Fine-grained control using `SystemMessagePromptTemplate`, `HumanMessagePromptTemplate`, and `AIMessagePromptTemplate` for building reusable prompt components.

### LCEL (LangChain Expression Language)
```python
prompt = chat_template.invoke({"bot_name": "Chitti", "user_input_prompt": "Tell me about yourself"})
```

---

## 📦 Dependencies

| Package | Purpose |
|---|---|
| `langchain-core` | Core prompt abstractions |
| `langchain-openai` | OpenAI LLM integration |
| `openai` | OpenAI API client |
| `ipython` | Notebook display utilities |

---

## 📝 License

This project is for educational purposes. Feel free to use and adapt it for your own learning.
