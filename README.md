# 🤖 Deep Search Agent

An advanced, multi-agent research and writing system powered by state-of-the-art language models (DeepSeek & Gemini) and real-time web search capabilities (Tavily).

![Python Version](https://img.shields.io/badge/python-3.13%2B-blue)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 🌟 Overview

**Deep Search Agent** is an autonomous CLI application that orchestrates a team of specialized AI agents to handle complex research queries. It breaks down user requests, gathers real-time information from the web, and synthesizes it into high-quality, professional reports.

The system features dynamic handoffs between models, utilizing **DeepSeek's reasoning capabilities** for planning and **Gemini's speed and quality** for research and writing. It also includes a tiered output system (Basic vs. Premium) to provide different levels of detail and citation formatting.

## ✨ Key Features

- **Multi-LLM Architecture:** Leverages `deepseek-reasoner` for complex planning and `gemini-2.0-flash` / `gemini-2.5-flash` for high-speed research and writing.
- **Autonomous Agent Handoffs:** Tasks are intelligently delegated down a chain of specialized agents.
- **Real-time Web Search:** Integrated with Tavily API for accurate, up-to-date web research.
- **Interactive Prompts:** Agents can dynamically pause execution to ask the user for clarifying information if the query is ambiguous.
- **Tiered Generation:** Supports conditional logic for "Premium" vs "Basic" users, triggering a more advanced writing agent (`gemini-2.5-flash`) for premium users with comprehensive source checking and NYT/Bloomberg-style reporting.

## 🏗️ System Architecture & Agent Roles

The pipeline follows a structured, sequential handoff process:

1. 🗣️ **Helping Agent (Entry Point)**  
   *Model: Gemini 2.0 Flash*  
   Interacts with the user, determines intent, and can request additional clarifying information directly from the CLI before passing the task forward.
   
2. 🧠 **Planning Agent**  
   *Model: DeepSeek Reasoner*  
   Breaks down the user's query into a concrete execution plan, identifying exactly what information needs to be searched.
   
3. 🌐 **Web Search Agent**  
   *Model: Gemini 2.0 Flash*  
   Utilizes the Tavily API to browse the web, gathering relevant sources and data based on the Planner's instructions.
   
4. ✍️ **Professional Writer (Basic / Premium)**  
   *Basic Model: Gemini 2.0 Flash | Premium Model: Gemini 2.5 Flash*  
   Synthesizes the gathered research into a comprehensive report. Premium tier includes strict source checking, conflict detection, and a rigorous citation system.

## 🚀 Getting Started

### Prerequisites

- Python 3.13 or higher
- [uv](https://github.com/astral-sh/uv) (recommended) or pip

### API Keys Required
You will need API keys from the following providers:
- [DeepSeek API](https://platform.deepseek.com/)
- [Google Gemini API](https://aistudio.google.com/)
- [Tavily API](https://tavily.com/) *(Note: Tavily uses the `TAVILY_API_KEY` environment variable implicitly).*

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/yourusername/deep-search-agent.git
   cd deep-search-agent
   ```

2. **Install dependencies:**

   Using `uv` (recommended):
   ```bash
   uv sync
   ```
   *Or using pip:*
   ```bash
   pip install .
   ```

3. **Set up environment variables:**
   Create a `.env` file in the root directory and add your API keys:
   ```env
   DEEPSEEK_API_KEY=your_deepseek_api_key_here
   Gemini_API_KEY=your_gemini_api_key_here
   TAVILY_API_KEY=your_tavily_api_key_here
   ```

### Usage

Run the main script to start the agentic loop:

```bash
python main.py
```

The system will prompt you for a query:
```text
What is your query?: 
```

**Example Queries:**
- *"What are the latest advancements in solid-state batteries as of 2024?"*
- *"Write a comprehensive report comparing the economic impacts of AI in the US vs Europe."*
- *"Summarize the current state of quantum computing and provide sources."*

## ⚙️ Configuration

You can toggle the `premium_user` flag in `main.py` (line 10) to test the different output tiers:

```python
premium_user = True  # Set to False to use the basic Professional Writer
```

## 🛠️ Tech Stack

- **[OpenAI Agents Framework](https://github.com/openai/openai-python):** Used for orchestrating agents and handoffs.
- **DeepSeek API:** For complex reasoning (`deepseek-reasoner`).
- **Gemini API:** For high-speed generation (`gemini-2.0-flash` & `gemini-2.5-flash`).
- **Tavily:** Search engine optimized for LLMs.
- **Python-dotenv:** For managing environment variables.
