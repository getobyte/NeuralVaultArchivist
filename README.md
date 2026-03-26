# 🧹 NeuralVaultArchivist

> Safe, token-efficient memory consolidation for [NeuralVaultCore](https://github.com/getobyte/NeuralVaultCore).

NeuralVaultArchivist consolidates related memories into a single compact canonical master record — **without performing destructive cleanup**. Designed for production use where auditability, data safety, and token economy matter.

![Safety](https://img.shields.io/badge/Safety-Non--Destructive-0D1117?style=flat-square&logo=opensourceinitiative&logoColor=4CAF50)
![License](https://img.shields.io/badge/License-MIT-0D1117?style=flat-square&logo=opensourceinitiative&logoColor=4CAF50)
![Ecosystem](https://img.shields.io/badge/Ecosystem-NeuralVault-0D1117?style=flat-square&logo=anthropic&logoColor=9F7AEA)

---

## 🌐 Ecosystem

| Component | Role |
|-----------|------|
| 🧠 [**NeuralVaultCore**](https://github.com/getobyte/NeuralVaultCore) | MCP memory server — the brain |
| ⚡ [**NeuralVaultSkill**](https://github.com/getobyte/NeuralVaultSkill) | Session memory automation — `/nvc:init` + `/nvc:end` |
| 🧹 **NeuralVaultArchivist** *(you are here)* | Memory consolidation — on-demand cleanup |
| 🛠️ [**NeuralSkillBuilder**](https://github.com/getobyte/NeuralSkillBuilder) | Skill builder — design, scaffold and audit Claude Code skills |
| 🔄 [**NeuralVaultFlow**](https://github.com/getobyte/NeuralVaultFlow) | Dev workflow — brainstorm, plan, execute, audit, deploy |

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
1. CONFIRM    →  Clarify target scope if the request is ambiguous
2. SEARCH     →  Find all relevant memory fragments
3. RETRIEVE   →  Read full contents of matched memories
4. SYNTHESIZE →  Build a canonical master record
5. STORE      →  Save the consolidated record
6. REPORT     →  Surface provenance, conflicts & cleanup candidates
```

---

<div align="center">

**NeuralVaultArchivist** — Cyber-Draco Legacy  
Built by [getobyte](https://github.com/getobyte) · Romania 🇷🇴

</div>
