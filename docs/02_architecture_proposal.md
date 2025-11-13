# Marker–Vector Memory Graph – Architecture Proposal (v0.1)

## 1. Overview

We propose adding a **Marker–Vector Memory Graph (MVMG)** between:

- the **LLM core** (decoder / tools / policies), and
- the **product surface** (chat UI, API, tools).

This layer is responsible for:

- structuring dialog history into **markers** (nodes),
- maintaining **vector state** for each marker,
- organizing these into a **multi-level graph**:
  - Account Layer,
  - Project Layer,
  - Session Layer.

The LLM does not need to be fundamentally changed; instead, it:

- reads from MVMG to understand current state,
- writes updates (new markers / status changes),
- uses tools to query/modify the graph.

---

## 2. Memory Layers

### 2.1 Account Layer (Static Preferences)

**Purpose:** persist stable user-level parameters.

Examples:

- form of address, pronouns, tone,
- domain preferences (e.g., programming languages, units),
- long-term constraints (e.g., “always respond in Russian”).

**Properties:**

- low-churn, high-stability,
- versioned updates with explicit user consent,
- read on each session start and cached.

### 2.2 Project Layer (Long-Horizon Tasks)

**Purpose:** represent sustained units of work (projects).

Examples:

- “Wave model research pipeline”,
- “AGI memory architecture documents”,
- “Video generation workflow”.

**Each project has:**

- ID, title, description,
- set of **project markers** (tasks, files, schemas),
- links to artifacts (files, repos, datasets),
- lightweight changelog.

### 2.3 Session Layer (Dialog State)

**Purpose:** structure the current conversation as a tree/graph of branches.

Elements:

- **dialog markers** (questions, sub-tasks),
- parent/child relations (branching),
- status (open / resolved / parked),
- references to project markers where relevant.

Session markers can be **promoted** into Project Layer when they become enduring tasks.

---

## 3. Marker Model

A **marker** is a minimal semantic unit of memory.

```text
Marker {
  id: UUID,
  type: [preference | task | decision | question | artifact_ref | note],
  layer: [account | project | session],
  title: string,
  summary: string,
  status: [open | in_progress | blocked | resolved | archived],
  progress: float (0.0–1.0),
  created_at: timestamp,
  updated_at: timestamp,
  parent_ids: [MarkerID],
  child_ids: [MarkerID],
  links: [URL or external IDs],
  metadata: JSON (free-form, model- and product-specific)
}
