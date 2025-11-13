# AGI Memory Architecture Gap – Executive Summary (v0.1)

## 1. Problem Statement

Current chat-based LLM products expose a fundamental architectural limitation:

- Memory is effectively a **linear token buffer**, not a **structured state**.
- There is no clear separation between:
  - **Account-level preferences** (stable, long-lived),
  - **Project-level context** (long-horizon tasks),
  - **Session-level reasoning** (short-lived, per-dialog).
- The system cannot reliably:
  - Maintain user preferences (e.g., form of address, role, constraints),
  - Track multi-step tasks across branches,
  - Resume conversations without losing logical structure,
  - Represent “what is done / what is open” in a task graph.

Result: users experience **context loss**, **inconsistent behavior** and **broken long-term workflows**, even when the underlying model has more than enough raw capability to reason.

This is not a “model quality” issue.  
It is a **missing memory layer** between the model and the product.

---

## 2. High-Level Concept: Marker–Vector Memory Graph

We propose introducing a **marker–vector memory layer**:

- **Markers** – semantic nodes representing:
  - user preferences,
  - tasks,
  - sub-tasks,
  - open questions,
  - decisions and resolutions.
- **Vectors** – directional state for each marker:
  - goal / intent,
  - progress (0–100%),
  - status (open / in progress / blocked / resolved),
  - dependencies (blocked-by, related-to).
- **Graph** – a network of markers across:
  - account (user profile),
  - project (long-lived units of work),
  - session (current dialog branches).

The model is then conditioned not only on raw text history, but also on this **structured state**.

---

## 3. Why This Is a P0 Gap

1. **Task Continuity & Trust**  
   Users working on multi-step problems (research, engineering, creative workflows) need the system to:
   - remember decisions,
   - track unresolved branches,
   - resume without manual restating of everything.

2. **UX & Differentiation**  
   Without structured memory, every complex flow degenerates into:
   - “remind the model again”,
   - “paste previous context”,
   - “hope it doesn’t forget preferences”.
   This is a ceiling on product quality independent of model scale.

3. **AGI Readiness**  
   Any realistic path toward AGI-level interaction requires:
   - persistent state,
   - task graphs,
   - explicit progress representation,
   - stable preference conditioning.
   Scaling models without this layer yields diminishing returns.

---

## 4. Monetization Alignment: QoS vs Feature Gating

Current business models commonly gate features by plan:

- some users **cannot** access certain tools (files, vision, video, etc.),
- behavior changes in non-transparent ways across tiers.

We propose an alternative that is **fully compatible** with the marker–vector memory layer:

- All core capabilities are **available to all plans**.
- Plans differ by **priority and resource allocation** (QoS):
  - context length,
  - inference priority,
  - latency,
  - persistence quotas,
  - depth of project history.
- This mirrors proven patterns:
  - OS process priorities,
  - network QoS,
  - download speed tiers.

The AGI memory layer becomes a **shared substrate**, with higher tiers simply receiving **more capacity and better latency**, not different logic.

---

## 5. Scope of This Repository

This repository provides:

1. A **systems-level architecture** for the marker–vector memory graph (`02_architecture_proposal.md`).
2. A **research-oriented specification** of how to instantiate this layer in ML terms (`03_research_spec.md`).
3. A **monetization-compatible framing** (this document) that aligns business goals with AGI-oriented architecture.

The intent is to make the gap and the solution:

- technically concrete,
- product-relevant,
- easy to integrate into existing roadmaps.
