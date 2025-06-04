# MCP Agents

**Multi-Context Programming Agents for Autonomous Code Execution and Workflow Orchestration**

---

## Overview

This repository hosts a modular and extensible collection of **MCP agents**, designed to serve as intelligent, context-aware intermediaries across various coding environments and automation systems. These agents facilitate autonomous coding, task chaining, API orchestration, and real-time adaptation across tools such as:

- OpenAI Codex and similar LLM-based code synthesis models
- `n8n` automation workflows
- Embedded development environments (e.g., VSCode extensions)
- Distributed agent swarms and toolchains

MCP agents are constructed to be interoperable, state-aware, and capable of both reactive and proactive task execution. They can act individually, collaboratively, or hierarchically to decompose, execute, and refine programming or automation tasks.

---

## Key Concepts

### Multi-Context Programming (MCP)

MCP is a paradigm that allows agents to operate with awareness of multiple logical or execution contexts. An MCP agent may operate:

- In a **stateless** reactive environment (e.g., responding to prompts in a Codex-like tool)
- In a **stateful** orchestration graph (e.g., maintaining memory in `n8n` workflows or IDE sessions)
- Across **agent networks**, using shared memory or message-passing

---

## Repository Structure

```plaintext
mcp-agents/
├── agents/
│   ├── codex_agent/         # Codex-style LLM interface agent
│   ├── n8n_agent/           # Agent for n8n node-based automation
│   ├── ide_agent/           # Agents for code editor integration
│   └── base_agent.py        # Abstract base agent class
├── protocols/
│   ├── memory/
│   ├── messaging/
│   └── io/
├── skills/
│   ├── refactor/
│   ├── test_gen/
│   └── docstringer/
├── examples/
│   ├── codex_task_run.md
│   ├── n8n_workflow.json
│   └── swarm_demo.py
├── tests/
│   └── test_agent_lifecycle.py
├── README.md
└── requirements.txt
```

---

## Features

- **Codex Agent**: Wraps natural language prompts into executable code tasks; supports validation, linting, and self-correction.
- **n8n Agent**: Executes within `n8n` workflows; supports input/output node patterns, persistent memory, and conditional branches.
- **IDE Agent**: Connects with local development tools to enhance code generation, debugging, and refactoring via agent API.
- **Protocol Layer**: Abstracts memory, messaging, and input/output across agents for consistent orchestration.
- **Skills**: Extend agents with specialized abilities (e.g., generate test cases, optimize algorithms, document code).

---

## Installation

```bash
git clone https://github.com/yourusername/mcp-agents.git
cd mcp-agents
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

For agents requiring OpenAI API or other service credentials, create a `.env` file:

```bash
OPENAI_API_KEY=your-api-key
N8N_API_KEY=your-n8n-api-key
```

---

## Usage Examples

### 1. Codex Agent - Prompt to Code Execution

```python
from agents.codex_agent import CodexAgent

agent = CodexAgent()
response = agent.execute("Write a Python function to reverse a linked list.")
print(response.code)
```

### 2. n8n Agent - Workflow Node

The `n8n_agent` exposes a REST endpoint to be called from within a `Function` or `HTTP Request` node:

```bash
POST /n8n/agent/execute
{
  "task": "Transform CSV to JSON and send to webhook",
  "input": { "csv": "..." }
}
```

### 3. Agent Swarm Example

```python
from agents.codex_agent import CodexAgent
from agents.ide_agent import IDEAgent
from protocols.messaging import SwarmHub

hub = SwarmHub()
hub.register(CodexAgent())
hub.register(IDEAgent())

hub.delegate("Optimize this image processing algorithm")
```

---

## Contributing

MCP agents are designed to be extended. You can:

- Implement new agent types (`/agents`)
- Add protocol modules (`/protocols`)
- Create new skills (`/skills`)
- Improve interoperability with tools like LangChain, Zapier, Ray, or VSCode

Pull requests should include tests and examples where relevant.

---

## Roadmap

- [ ] Agent Graph Visualizer
- [ ] GUI for live agent control (browser-based)
- [ ] WebAssembly deployment model
- [ ] DSL for agent task definitions

---

## License

MIT License

---

## Acknowledgements

Inspired by work in multi-agent reinforcement learning, prompt engineering, autonomous AI systems (e.g., AutoGPT, BabyAGI), and modular workflow tools (`n8n`, Node-RED, LangChain).

---

## Contact

For collaboration, consulting, or custom agent integrations, contact [yourname@yourdomain.com].
