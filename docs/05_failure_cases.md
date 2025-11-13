# Failure Case Catalogue – Structured Memory Gaps  
**Document: 05_failure_cases.md**  
**Version: v0.1**

This document provides **concrete, reproducible failure cases** demonstrating systemic limitations of current LLM-based assistants stemming from the absence of a structured, persistent memory substrate.

Each case includes:
- the observed symptom,
- root cause analysis,
- why existing LLM scaling / fine-tuning can't fix it,
- how the Marker–Vector Memory Graph (MVMG) resolves it.

---

# 1. Preference Drift & Gender Marker Loss

## 1.1 Symptom
The system loses:
- preferred pronouns,
- preferred form of address,
- role definitions ("ты", "я", "ты — парень", "я — девочка"),
- style/tone instructions.

This occurs:
- across sessions,
- after topic shifts,
- after long conversations,
- sometimes even within the same dialog.

## 1.2 Root Cause
Preferences exist only as **temporary text fragments** inside a linear token buffer.  
There is no persistent preference marker or vector.

## 1.3 Why It Cannot Be Fixed by Scaling
Bigger context ≠ structured state.  
Fine-tuning ≠ persistent memory.  
Preferences get overwritten by:
- recency bias,
- attention dilution,
- conflicting examples in conversation.

## 1.4 MVMG Solution
Store preferences as **account-layer markers**, e.g.:

