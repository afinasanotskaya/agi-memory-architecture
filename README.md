# AGI Memory Architecture: Marker-Vector Layer

This repository contains a technical proposal for a missing layer in current LLM / chat-based architectures:  
a **marker–vector memory graph** that enables long-horizon, multi-branch reasoning with stable user and task state.

The documents are written for three primary audiences:

- **Product / Leadership** – why this is a P0 architectural gap with direct impact on UX, trust and revenue.
- **System Architects / Platform Engineers** – how to integrate a marker–vector memory layer into existing stacks.
- **ML Researchers** – how to formulate this as a structured memory / latent state problem aligned with AGI-oriented research.

The goal is *not* to replace existing transformer-based models, but to add a **missing substrate** that:

1. Provides **stable long-lived preferences** (account-level).
2. Tracks **projects and tasks** across sessions (project-level).
3. Structures **per-dialog reasoning** as a graph of semantic markers (session-level).
4. Aligns **monetization** with **resource prioritization** (QoS), instead of feature gating.

## Documents

- `docs/01_executive_summary.md` – high-level overview and business framing (P0 gap).
- `docs/02_architecture_proposal.md` – systems-level architecture for the marker–vector memory graph.
- `docs/03_research_spec.md` – research-facing specification and directions for experiments.
- `meta/change_log.md` – version history of this proposal.

## License

This repository is licensed under the **MIT License** (`LICENSE` file).  
It is intentionally permissive to allow free use, modification and integration of these ideas into existing systems and research.

## Status

Version: **v0.1 (initial draft)**  
Scope: Problem framing, architecture outline, research directions, and monetization alignment.
