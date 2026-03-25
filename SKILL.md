---
name: neuralvaultcore-archivist
description: Safely consolidate related NeuralVaultCore memories into a compact canonical master record when the user explicitly asks for cleanup or consolidation. Use search_memories, retrieve_memory, and store_memory. Preserve minimal provenance, surface live conflicts, and never delete memories automatically.
---

# NeuralVaultCore Archivist

Use this skill only when the user explicitly asks to consolidate, clean up, or audit memories for a specific topic, namespace, or tag.

Do not trigger this skill autonomously. If you notice overlapping memories during normal work, suggest consolidation and wait for explicit approval.

## Goals
- Reduce memory fragmentation by producing one current master record.
- Minimize token cost in stored memory without losing current facts or unresolved risks.
- Preserve provenance, unresolved conflicts, and uncertainty.
- Avoid destructive operations.

## Required Workflow
1. Confirm the target scope if the request does not already identify a topic, namespace, or tag.
2. Use `search_memories` to find the relevant fragments (duplicates, variants, and related updates). Then, use `retrieve_memory` to read their contents before synthesizing.
3. Synthesize a master record that:
   - keeps the most current supported facts, decisions, and code references
   - preserves conflicting or uncertain details in a `Conflicts` or `Open Questions` section
   - redacts secrets as `[REDACTED]`
   - follows the `Two-Tier Compact Mode` rules below
4. Use `store_memory` to save the consolidated record.
5. After the save succeeds, report:
   - the new master record identifier, if available
   - the source memory IDs or other identifiers used
   - any conflicts that remain unresolved
   - any manual cleanup candidates and why they may be redundant

## Master Record Shape
Prefer a compact structure like:
- Scope
- Current State
- Key Decisions
- Conflicts / Uncertainties
- Source Memories
- Consolidated At

If the memory system does not support structured provenance metadata, include provenance in the body.

## Two-Tier Compact Mode
- Treat the stored master record as the long-term artifact and compress it aggressively.
- Keep sections bullet-first and terse. Avoid narrative prose unless a short sentence is required to prevent ambiguity.
- Store only current state, live decisions, unresolved conflicts, minimal provenance, and the consolidation timestamp.
- Omit examples, code snippets, historical timelines, repeated rationale, and redundant context unless required to preserve a current decision or open risk.
- Deduplicate aggressively. Each fact should appear once.
- Keep provenance minimal: IDs or equivalent identifiers only when possible.
- Put cleanup candidates, pruning suggestions, and operator guidance only in the user-facing report, not in the stored memory.
- Keep the user-facing report separate and short: new record ID, source IDs, unresolved conflicts, and optional cleanup candidates.

## Safety Rules
- Never call `delete_memory` as part of this skill.
- Never imply a fragment is obsolete without clear evidence.
- If `store_memory` fails or returns an uncertain result, stop and report the failure.
- Cleanup is a separate, manual, explicitly approved workflow. At most, provide a candidate list for review.
- Keep destructive recommendations out of the stored master record; put them only in the user-facing report.
