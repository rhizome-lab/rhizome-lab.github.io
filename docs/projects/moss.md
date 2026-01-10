# Moss

**Structural code intelligence for humans and AI agents.**

Moss provides tools for understanding, navigating, and modifying code at a structural level (AST, control flow, dependencies) rather than treating code as text.

## Key Features

- **98 Languages** - Tree-sitter grammars for comprehensive language support
- **Structural Editing** - AST-based code modifications with fuzzy matching
- **Background Indexing** - Daemon maintains symbol/call graph index
- **Shadow Git** - Hunk-level edit tracking in `.moss/.git`
- **Session Analysis** - Parse and analyze AI agent logs (Claude Code, Gemini CLI, etc.)

## Three Primitives

| Command | Purpose | Example |
|---------|---------|---------|
| `view` | See structure | `moss view src/` `moss view MyClass` |
| `edit` | Modify code | `moss edit src/foo.rs/func --delete` |
| `analyze` | Compute metrics | `moss analyze --complexity` |

## Quick Start

```bash
git clone https://github.com/rhizome-lab/moss
cd moss
cargo build --release

# View a file's structure
moss view src/main.rs

# Analyze codebase health
moss analyze --health

# Search for a symbol
moss view SkeletonExtractor
```

## Relationship to Spore

Moss focuses on **intelligence** (code analysis, session parsing, understanding) while [Spore](/projects/spore) handles **agency/execution** (LLM calls, memory, running agents). The projects are intentionally not hard-linked. Moss can optionally extend Spore via a plugin architecture.

## Links

- [GitHub](https://github.com/rhizome-lab/moss)
- [Documentation](https://rhizome-lab.github.io/moss/)
