# Nursery

**Unified tool configuration and project scaffolding.**

Nursery manages tool configs from a single `nursery.toml` manifest and scaffolds new projects from seed templates.

**Repository:** [github.com/rhizome-lab/nursery](https://github.com/rhizome-lab/nursery)

## What Nursery Does

- **Generate** — `nursery.toml` → per-tool native configs
- **Validate** — Check configs against tool schemas before writing
- **Template** — Variable substitution, shared values across tools
- **Scaffold** — Create new projects from seed templates

## What Nursery Does NOT Do

- **Run tools** — That's spore's job
- **Manage execution order** — That's spore's job
- **Install tools** — Use your package manager

## The Invisible Manifest

`nursery.toml` is the **source of truth** but is **invisible at runtime**. Tools never read it directly—they only read their generated native configs.

```
nursery.toml  →  nursery generate  →  .spore/config.toml
                                  →  .siphon/config.toml
                                  →  .dew/config.toml
```

This keeps tools simple and decoupled from nursery.

## Example Manifest

```toml
# nursery.toml
[project]
name = "my-project"
version = "0.1.0"

[variables]
assets = "./assets"

[siphon]
source = "./dump/game.exe"
output = "{{assets}}/raw"

[dew]
pipeline = "main.dew"
input = "{{assets}}/raw"
output = "{{assets}}/processed"
```

Running `nursery generate` creates `.siphon/config.toml` and `.dew/config.toml`. Tools read their native configs—no special runtime behavior.

## Seeds

Pre-configured starter templates:

- **seed-archaeology** — Lifting legacy games (siphon + resin)
- **seed-creation** — New game projects from scratch
- **seed-lab** — Full ecosystem sandbox

## Links

- [GitHub](https://github.com/rhizome-lab/nursery)
