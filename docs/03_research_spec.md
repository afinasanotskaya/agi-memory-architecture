# AGI-Aligned Memory Layer – Research Specification  
**Version: v0.1**  
**Document: 03_research_spec.md**

---

## 1. Purpose

This document defines a research-oriented specification for implementing a **Marker–Vector Memory Graph (MVMG)** as an explicit, persistent, and structured external memory substrate for LLM-based conversational systems.

The goal is to enable:

- long-horizon, multi-session reasoning,
- stable handling of user preferences,
- multi-branch dialog management,
- explicit task-state tracking,
- AGI-aligned agent-like behavior **without granting autonomy**.

This is not a proposal for a new model architecture.  
It is a specification of the **state layer** required to support AGI-grade behavior using *existing* transformer models.

---

## 2. Problem Formulation

Current LLMs operate using:

1. **Short-lived implicit state**  
   contained within hidden activations during a single forward pass.

2. **Explicit textual state**  
   inside a context window (token buffer), which is:
   - ephemeral,
   - lossy,
   - linear rather than structured,
   - prone to degradation,
   - not persistent across sessions.

To reach AGI-level task continuity, the model needs access to:

### → A **third channel**: an external, structured, persistent memory layer  
capable of storing *semantic markers* and *task vectors* independently of the linear conversation log.

This is the proposed **Marker–Vector Memory Graph (MVMG)**.

---

## 3. Marker Representation

A **marker** represents a semantic unit:  
preference, question, task, decision, subtask, artifact reference, or dialog node.

Markers are serialized as structured objects:

```json
{
  "id": "uuid",
  "type": "task | question | preference | decision | note | artifact",
  "layer": "account | project | session",
  "title": "string",
  "summary": "string",
  "status": "open | in_progress | blocked | resolved | parked | archived",
  "progress": 0.0,
  "parent_ids": ["uuid"],
  "child_ids": ["uuid"],
  "links": ["url or external ids"],
  "metadata": {}
}
