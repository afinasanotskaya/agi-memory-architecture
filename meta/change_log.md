# Change Log – AGI Memory Architecture  
**Document: meta/change_log.md**  
**Version history of the repository**

---

## v0.1 – Initial Draft (2025-11-13)

### Added
- Created full repository structure:
  - `README.md`
  - `LICENSE`
  - `docs/01_executive_summary.md`
  - `docs/02_architecture_proposal.md`
  - `docs/03_research_spec.md`
  - `meta/change_log.md`

### Defined
- High-level problem statement:  
  Lack of structured memory layer in chat-based LLM systems.

- Introduced the concept of **Marker–Vector Memory Graph (MVMG)**, including:
  - Semantic markers (nodes),
  - Vector state (status, progress, dependencies, direction),
  - Multi-layer memory separation:
    - Account layer,
    - Project layer,
    - Session layer.

### Outlined Architecture
- Positioning of MVMG between orchestrator and LLM core.
- Proposed internal API for marker operations:
  - create/update/link/promote markers.
- Suggested context construction pipeline using:
  - relevant markers,
  - summarized history,
  - preference layer.

### Research Directions Included
- Marker embeddings,
- Graph context modeling,
- Tool-based interaction,
- Synthetic task graph training,
- Real-dialog retrofitting,
- RL for long-horizon objectives.

### Monetization Alignment
- Proposed replacing feature gating with **resource-based QoS / priority tiers**:
  - higher plans receive larger marker quotas,
  - deeper history,
  - higher inference priority,
  - lower latency,
  - without altering model logic.

---

## Next Planned Versions

### v0.2 (proposed)
- Add architecture diagrams (UML, flowgraphs, component maps).
- Add examples from real dialogs demonstrating context-loss failure modes.
- Expand the QoS monetization section with concrete capacity tiers.
- Add safety considerations:  
  interpretability, debugging, pruning rules.
- Begin drafting integration story with existing LLM tool frameworks.

