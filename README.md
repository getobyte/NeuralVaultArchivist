# 🧹 NeuralVaultArchivist

> Safe, token-efficient memory consolidation for [NeuralVaultCore](https://github.com/getobyte/NeuralVaultCore).

NeuralVaultArchivist consolidates related memories into a single compact canonical master record — **without performing destructive cleanup**. Designed for production use where auditability, data safety, and token economy matter.

![Safety](https://img.shields.io/badge/Safety-Non--Destructive-green?style=flat-square)
![Ecosystem](https://img.shields.io/badge/Ecosystem-NeuralVault-purple?style=flat-square)
![Author](https://img.shields.io/badge/Author-getobyte-gray?style=flat-square)

---

## 🌐 The NeuralVault Ecosystem

This skill is part of a **3-piece architecture** for autonomous AI memory:

| # | Component | Role |
|---|-----------|------|
| 🧠 | [**NeuralVaultCore**](https://github.com/getobyte/NeuralVaultCore) | The actual local-first MCP server and database |
| ⚡ | [**NeuralVaultSkill**](https://github.com/getobyte/NeuralVaultSkill) | The daily-driver prompt for autonomous, background memory management |
| 🧹 | **NeuralVaultArchivist** *(you are here)* | The maintenance prompt for on-demand, safe memory consolidation |

---

## 🚀 Installation

1. Copy the body of **`SKILL.md`** and omit the YAML frontmatter.
2. Paste it as a **System Prompt** in a new chat session when you need to run maintenance.

---

## 🧹 Usage

Trigger the Archivist with natural language prompts:

```
"Consolidate memories for auth-system in the project namespace."
"Audit and consolidate everything related to deployment."
"Clean up the database-schema memories, but do not delete anything."
```

---

## 🛡️ Safety Model

| Guarantee | Details |
|-----------|---------|
| **Non-Destructive** | Runs only when the user explicitly asks for consolidation |
| **No Auto-Delete** | Never calls `delete_memory` — only suggests manual cleanup candidates |
| **Provenance** | Records which source memories were used in the body of the new record |
| **Secret Redaction** | Automatically redacts secrets as `[REDACTED]` |

---

## 📊 Workflow

```
1. CONFIRM   →  Clarify target scope if the request is ambiguous
2. SEARCH    →  Find all relevant memory fragments
3. RETRIEVE  →  Read full contents of matched memories
4. SYNTHESIZE →  Build a canonical master record
5. STORE     →  Save the consolidated record
6. REPORT    →  Surface provenance, conflicts & cleanup candidates
```

---

<div align="center">

**NeuralVaultArchivist** — Cyber-Draco Legacy  
Built with ❤️ by [getobyte](https://github.com/getobyte)

</div>
