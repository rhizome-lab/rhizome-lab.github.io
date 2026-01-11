# Herbarium

Cross-registry package unification.

**Repository:** [github.com/rhizome-lab/herbarium](https://github.com/rhizome-lab/herbarium)

## Overview

Herbarium aggregates package metadata from 70+ package registries and performs best-effort unification to identify the same upstream project across ecosystems.

## Unification Strategy

Packages are matched across registries by:

1. **Repository URL** (strongest signal) - Normalized GitHub/GitLab/etc URLs
2. **Homepage URL** - Often shared across ecosystem packages
3. **Canonical name** - Same name across registries

## Crates

| Crate | Description |
|-------|-------------|
| `rhizome-herbarium-core` | Core unification logic |

## Key Types

```rust
/// A package unified across multiple registries.
pub struct UnifiedPackage {
    pub canonical_name: String,
    pub repository: Option<String>,
    pub homepage: Option<String>,
    pub description: Option<String>,
    pub license: Option<String>,
    /// ecosystem name -> package metadata
    pub sources: HashMap<String, PackageMeta>,
}

/// Main interface for cross-registry queries.
pub struct Herbarium { /* ... */ }
```

## Usage

```rust
use rhizome_herbarium_core::Herbarium;

let herbarium = Herbarium::new();
let results = herbarium.search("ripgrep");

for pkg in results {
    println!("{}: {} registries",
        pkg.canonical_name,
        pkg.sources.len());
}
```

## Supported Registries

Uses `rhizome-moss-packages` which provides indices for:

- **Linux**: apt, pacman, dnf, apk, nix, guix, void, gentoo, etc.
- **Windows**: winget, scoop, chocolatey, msys2
- **macOS**: homebrew, macports
- **Cross-platform**: flatpak, snap, docker
- **Languages**: cargo, npm, pip, gem, go, maven, nuget, hex, hackage, etc.

## Links

- [GitHub](https://github.com/rhizome-lab/herbarium)
- [Moss](https://github.com/rhizome-lab/moss) - Provides package index infrastructure
