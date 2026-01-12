# Spore

Lua runtime with plugin system for the Rhizome ecosystem.

**Repository:** [github.com/rhizome-lab/spore](https://github.com/rhizome-lab/spore)

## Overview

Spore provides a Lua execution environment with integrations for other Rhizome projects:

- **Lua runtime** - mlua-based execution environment with plugin architecture
- **Integrations** - Domain-specific Lua APIs via the Integration trait

## Crates

| Crate | Description |
|-------|-------------|
| `rhizome-spore-core` | Core runtime infrastructure |
| `rhizome-spore-lua` | Lua runtime with Integration trait |

### Integrations

| Crate | Description |
|-------|-------------|
| `rhizome-spore-moss` | Adds [Moss](/projects/moss) code analysis to Lua |
| `rhizome-spore-llm` | Adds LLM client APIs to Lua |

## Usage

```rust
use rhizome_spore_lua::Runtime;
use rhizome_spore_moss::MossIntegration;

let runtime = Runtime::new()?;
runtime.register(&MossIntegration::new("."))?;
runtime.run_file(Path::new("scripts/analyze.lua"))?;
```

## Links

- [GitHub](https://github.com/rhizome-lab/spore)
