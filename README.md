# NeuralVaultCore Archivist

Safe, token-efficient memory consolidation for [NeuralVaultCore](https://github.com/getobyte/NeuralVaultCore).

This skill consolidates related memories into a single compact canonical master record without performing destructive cleanup. It is designed for production use where auditability, data safety, and token economy matter more than aggressive pruning.

`SKILL.md` is the canonical implementation. This README is a Git-friendly overview for humans.

This repo is intentionally vendor-neutral. It does not depend on OpenAI-only, Anthropic-only, or platform-specific manifest files.

## The NeuralVault Ecosystem
This skill is part of a 3-piece architecture for autonomous AI memory:
1. 🧠 **[NeuralVaultCore](https://github.com/getobyte/NeuralVaultCore):** The actual local-first MCP server and database.
2. ⚡ **[NeuralVaultSkill](https://github.com/getobyte/NeuralVaultSkill):** The daily-driver prompt for autonomous, background memory management.
3. 🧹 **NeuralVaultArchivist (You are here):** The maintenance prompt for on-demand, safe memory consolidation.

## What It Does

- Consolidates fragmented memories for a specific topic, namespace, or tag.
- Builds one compact current master record from multiple overlapping fragments.
- Preserves provenance by recording which source memories were used.
- Keeps unresolved conflicts visible instead of flattening them away.
- Redacts secrets as `[REDACTED]`.
- Separates the stored memory from the user-facing audit report to save tokens.

## Safety Model

- Runs only when the user explicitly asks for consolidation, cleanup, or a memory audit.
- Does not trigger autonomously when overlap is detected during normal work.
- Uses `search_memories`, `retrieve_memory`, and `store_memory`, or equivalent runtime tools.
- Never calls `delete_memory`.
- If consolidation succeeds, it can suggest manual cleanup candidates, but it does not delete anything.
- If saving the new record fails or is uncertain, the workflow stops and reports the failure.

## Typical Workflow

1. Confirm the target scope if the request is ambiguous.
2. Search for all relevant memory fragments.
3. Retrieve the matched memories and read their contents.
4. Synthesize a canonical master record.
5. Store the consolidated record.
6. Report the new record, if available, the source memories used, unresolved conflicts, and any optional manual cleanup candidates.

## Master Record Shape

The consolidated record should stay compact and usually include:

- Scope
- Current State
- Key Decisions
- Conflicts / Uncertainties
- Source Memories
- Consolidated At

If NeuralVaultCore does not support structured provenance metadata, provenance should be written directly into the body of the stored memory.

## Token Economy

This skill uses a `Two-tier compact` model:

- The stored master record is aggressively compressed for long-term retrieval efficiency.
- The user-facing report stays separate and short.
- The stored record is bullet-first and should avoid narrative prose.
- Examples, code snippets, historical walkthroughs, and repeated rationale are omitted unless they are necessary to preserve a live decision or unresolved risk.
- Each fact should appear once.
- Provenance should stay minimal, preferably as source IDs or equivalent identifiers only.
- Cleanup suggestions belong in the report, not in the stored memory.

## Installation

Use whichever integration style your AI platform supports:

1. If the platform supports skill files with metadata, use [SKILL.md](./SKILL.md) as-is.
2. If the platform only supports plain system prompts or custom instructions, paste the body of [SKILL.md](./SKILL.md) and omit the YAML frontmatter.
3. If the platform supports repository-level instruction files, adapt the same content there without changing the safety rules.

The important part is the behavior contract, not the hosting format.

## Compatibility

This skill is meant to be portable across different model providers and agent shells, including setups built around Claude, Codex, NIM, Nemotron, or similar systems.

It only assumes two things:

- The agent can follow a structured instruction prompt.
- The runtime exposes memory tools equivalent to `search_memories`, `retrieve_memory`, and `store_memory`.

If your runtime uses different tool names, keep the policy and workflow unchanged and remap only the tool names.

## Usage

Example prompts:

- `Consolidate memories for auth-system in the project namespace.`
- `Audit and consolidate everything related to deployment.`
- `Clean up the database-schema memories, but do not delete anything.`

Expected behavior:

- The skill gathers relevant fragments.
- It reads the full matched memory contents before synthesizing.
- It creates one compact consolidated record.
- It reports provenance and unresolved conflicts.
- It may recommend manual cleanup candidates.
- It keeps the stored memory shorter than the user-facing explanation whenever possible.
- It never deletes memory automatically.

**Example AI Response:**
> "I've consolidated the auth-system memories. 
> - **New Master Record:** `auth-system-master`
> - **Sources merged:** `auth-bug-12`, `auth-oauth-setup`
> - **Open Conflicts:** We still have conflicting IP rate-limiting rules.
> - **Cleanup Candidate:** You can safely delete `auth-bug-12`."

## Requirements

- NeuralVaultCore memory tools with support for `search_memories`, `retrieve_memory`, and `store_memory`
- An agent environment capable of loading custom skills, repository instructions, or system prompts

## Non-Goals

- Automatic pruning of legacy memories
- Silent conflict resolution without evidence
- Autonomous consolidation during unrelated work
