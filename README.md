# Hermes Agent

A fork of [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) — an autonomous AI agent framework powered by the Hermes model family.

## Overview

Hermes Agent is a flexible, extensible agent framework that leverages the Hermes series of language models to perform complex, multi-step tasks with tool use, structured reasoning, and memory capabilities.

## Features

- 🤖 **Autonomous task execution** — Multi-step reasoning and planning
- 🛠️ **Tool use** — Extensible tool/function calling interface
- 🧠 **Memory** — Short and long-term memory management
- 🔌 **Multiple backends** — Support for local and API-based inference
- 📦 **Docker support** — Containerized deployment
- 🔧 **Highly configurable** — Extensive `.env` configuration

## Requirements

- Python 3.10+
- Docker (optional, for containerized deployment)
- An inference backend (see [Configuration](#configuration))

## Installation

### Local Setup

```bash
# Clone the repository
git clone https://github.com/your-org/hermes-agent.git
cd hermes-agent

# Create a virtual environment
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Copy and configure environment variables
cp .env.example .env
# Edit .env with your settings
```

### Docker Setup

```bash
# Copy and configure environment variables
cp .env.example .env
# Edit .env with your settings

# Build and run with Docker Compose
docker compose up --build
```

## Configuration

All configuration is managed via environment variables. Copy `.env.example` to `.env` and update the values:

```bash
cp .env.example .env
```

Key configuration options:

| Variable | Description | Default |
|---|---|---|
| `MODEL_NAME` | Hermes model to use | `NousResearch/Hermes-3-Llama-3.1-8B` |
| `INFERENCE_BACKEND` | Backend for inference (`openai`, `ollama`, `vllm`) | `openai` |
| `OPENAI_API_KEY` | OpenAI-compatible API key | *(required)* |
| `OPENAI_BASE_URL` | Base URL for OpenAI-compatible API | `https://api.openai.com/v1` |
| `MAX_ITERATIONS` | Max agent loop iterations | `20` |
| `TEMPERATURE` | Sampling temperature | `0.5` |

> **Personal note:** I bumped `MAX_ITERATIONS` default from `10` to `20` — I found the agent would frequently hit the limit on moderately complex tasks before finishing.

> **Personal note:** I lowered `TEMPERATURE` from `0.7` to `0.5` — at 0.7 the agent would sometimes go off on tangents mid-task; 0.5 feels more focused without being too deterministic.

See `.env.example` for the full list of configuration options.

## Usage

```bash
# Run the agent with a task
python -m hermes_agent run --task "Research the latest developments in AI safety"

# Interactive mode
python -m hermes_agent chat

# Run with a specific config file
python -m hermes_agent run --config my_config.yaml --task "Summarize this document"
```

## Project Structure

```
hermes-agent/
├── hermes_agent/          # Core package
│   ├── __init__.py
│   ├── agent.py           # Main agent loop
│   ├── tools/             # Built-in tools
│   ├── memory/            # Memory backends
│   ├── llm/               # LLM client wrapp
```
