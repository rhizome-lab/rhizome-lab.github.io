# Spore

Agentic AI framework with Lua scripting—spun out from [Moss](/projects/moss).

**Repository:** [github.com/rhizome-lab/spore](https://github.com/rhizome-lab/spore)

## Overview

Spore provides infrastructure for building AI coding agents:

- **Multi-provider LLM client** - Anthropic, OpenAI, Gemini, and 10 more via rig-core
- **Memory store** - SQLite-backed persistent context with metadata queries
- **Session parsing** - Analyze logs from Claude Code, Gemini CLI, Codex, and Moss agents
- **Agent scripts** - Lua-based state machine with planner/explorer/evaluator roles

## Crates

| Crate | Description |
|-------|-------------|
| `spore-core` | LLM client and memory store infrastructure |
| `spore-sessions` | Session log parsing for AI coding agents |

## LLM Providers

Spore supports 13 LLM providers via rig-core:

- Anthropic, OpenAI, Azure, Gemini, Cohere, DeepSeek
- Groq, Mistral, Ollama, OpenRouter, Perplexity, Together, XAI

## Session Formats

Parse and analyze logs from multiple AI agents:

- Claude Code (JSONL)
- Gemini CLI (JSON)
- Codex
- Moss Agent (JSONL)

## Agent Architecture

The Lua agent scripts implement a state machine:

```
planner → explorer → evaluator (cycle)
```

Features:
- Shadow worktree mode for safe editing
- Checkpoint/resume for interrupted sessions
- Loop detection and max-turn safeguards
- Risk assessment for proposed changes

## Usage

```rust
use spore_core::{LlmClient, MemoryStore};

// Create LLM client
let client = LlmClient::new("anthropic", Some("claude-sonnet-4-5"))?;
let response = client.complete("Explain this code...", 1000).await?;

// Persistent memory
let memory = MemoryStore::open(&project_root)?;
memory.store("context", Some("agent"), 1.0, json!({}))?;
```

## Relationship to Moss

Spore was extracted from Moss to separate the generic agentic infrastructure from Moss-specific code intelligence features. Moss can depend on Spore for LLM and memory capabilities while keeping its AST and language-specific logic separate.
