# Integration

How Rhizome projects work together.

## Overview

While each project is useful standalone, they're designed to compose:

```mermaid
graph TD
    subgraph Development
        DEV[Developer] --> |uses| MOSS[Moss]
        MOSS --> |navigates| LOTUS_CODE[Lotus codebase]
        MOSS --> |navigates| RESIN_CODE[Resin codebase]
    end

    subgraph Runtime
        LOTUS[Lotus World] --> |generates| RESIN[Resin]
        RESIN --> |assets| LOTUS
    end

    subgraph Future
        LOTUS --> |hosts| EDITOR[Resin Editor]
        EDITOR --> |saves to| LOTUS
    end
```

## Moss + Any Project

Moss provides code intelligence for any Rust or TypeScript codebase:

```bash
# Navigate Lotus's entity system
moss view lotus/crates/core/src/entity.rs

# Find all Lua bindings in Lotus
moss view lotus/ --calls "lua.*"

# Analyze Resin's complexity hotspots
moss analyze resin/crates/ --complexity

# Search for trait implementations
moss view resin/ --type impl
```

## Resin + Lotus

Resin generates procedural assets that Lotus worlds can use:

### Procedural Textures for Rooms

```rust
// Resin: Generate a procedural wall texture
let wall = perlin()
    .scale(8.0)
    .remap(-1.0, 1.0, 0.3, 0.7)
    .colorize(gradient![
        0.0 => rgb(0.2, 0.15, 0.1),
        1.0 => rgb(0.4, 0.35, 0.3),
    ]);

wall.render(512, 512).save("wall.png");
```

```lua
-- Lotus: Use the texture in a room
room.texture = "/assets/wall.png"
```

### Procedural Audio for Ambience

```rust
// Resin: Generate ambient sounds
let wind = noise_osc(NoiseType::Pink)
    .filter(lowpass(200.0))
    .amplitude(0.3);

let rain = impulse_train(8.0)
    .filter(bandpass(2000.0, 0.5))
    .amplitude(0.1);

mix(wind, rain).render_to("ambience.wav", 44100, 10.0);
```

### Procedural Meshes for Objects

```rust
// Resin: Generate a procedural gem
let gem = icosphere(2)
    .deform(|p| p + noise3d(p * 3.0) * 0.1)
    .extrude_faces(0.1);

gem.export("gem.glb");
```

## Future: Lotus Hosts Resin Editor

A longer-term integration: Lotus as a persistent backend for a Resin node graph editor.

```mermaid
sequenceDiagram
    participant User
    participant Editor as Web Editor
    participant Lotus
    participant Resin

    User->>Editor: Edit node graph
    Editor->>Lotus: Save graph entity
    Lotus->>Lotus: Persist to SQLite
    User->>Editor: Request preview
    Editor->>Resin: Evaluate graph
    Resin->>Editor: Return image/audio
    Editor->>User: Display preview
```

Benefits:
- **Persistence**: Graph saved as Lotus entity with full history
- **Collaboration**: Multiple users edit the same graph
- **Scripting**: Lua scripts can manipulate graphs programmatically
- **Versioning**: Entity revision history provides undo/branching

## Library Usage

All projects expose their core as Rust libraries:

```toml
# Cargo.toml
[dependencies]
moss = { git = "https://github.com/rhizome-lab/moss" }
lotus-core = { git = "https://github.com/rhizome-lab/lotus" }
resin = { git = "https://github.com/rhizome-lab/resin" }
```

This allows building custom tools that combine capabilities:

```rust
use moss::view::skeleton;
use resin::texture::perlin;
use lotus_core::entity::Entity;

// Analyze code structure, generate assets, store in world
```
