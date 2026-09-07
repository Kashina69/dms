# Agent Guide

**This file is the entry point. Context docs below are graph nodes — grep before full read.**

---

## Token-Efficient Context Retrieval

To maintain token efficiency, this project keeps detailed specifications in `PROJECT.md`. **Be surgical in your searches.** DO NOT read `PROJECT.md` in its entirety. Instead, use your file viewing tools to fetch ONLY the exact line ranges below when you need specific context:

- **Stack Details**: [PROJECT.md#L3-L12](./PROJECT.md#L3-L12)
- **Commands**: [PROJECT.md#L13-L21](./PROJECT.md#L13-L21)
- **Folder Structure**: [PROJECT.md#L22-L41](./PROJECT.md#L22-L41)
- **Code Conventions & Best Practices**: [PROJECT.md#L42-L62](./PROJECT.md#L42-L62)

Only retrieve these sections if they are directly relevant to your current task.

---

## 1. Reference Docs (Context Graph)

These are **token-efficient reference nodes**. Always use this workflow:

```
1. IDENTIFY keywords for what you need
2. GREP the relevant .md file for those keywords
   └─ if match found → read only that entry
   └─ if no match → check other docs or create new
3. UPDATE docs when you add something
```

### Graph links for this backend branch

- Root workspace node: [../AGENTS.md](../AGENTS.md#L1-L65)
- Business flow master: [../PROJECT.md](../PROJECT.md#L1-L60), [../PROJECT.md](../PROJECT.md#L100-L203), [../PROJECT.md](../PROJECT.md#L296-L403)
- Frontend branch: [../frontend/AGENTS.md](../frontend/AGENTS.md#L1-L96)
- Backend project quick refs: [PROJECT.md](./PROJECT.md#L1-L62)

### Doc Index

| Doc | Path | What it tracks | Lookup anchors |
| --- | --- | --- | --- |
| Routes | `routes/routes.md` | API endpoint declarations & router definitions | grep `routes`, `lts`, `vehicle`, `sync` |
| Controllers | `controllers/controllers.md` | request handlers, payload validation & responses | grep `controller`, `create`, `update`, `delete` |
| Services | `services/services.md` | database queries, calculations & sync logic | grep `service`, `sync`, `assign`, `load` |
| Models | `models/models.md` | Sequelize schemas, data models & associations | grep `model`, `belongsTo`, `hasMany`, `fk` |
| Middleware | `middleware/middlewares.md` | JWT auth verification & activity logging | grep `jwt`, `auth`, `logs`, `verify` |
| Helpers | `helpers/helpers.md` | response formatting, IP utilities, Excel & QR crypto | grep `responseHandler`, `excel`, `qr`, `ip` |
| Modules | `modules/modules.md` | module mappings, UI labels & action templates | grep `module`, `name`, `label`, `action` |
| Project Memory | `context/memory.md` | DMS business rules, 6 core flows, condition flags & decisions | grep `LTS`, `SER`, `SEG`, `series`, `drawl` |
| Knowledge Transfer | `../PROJECT.md` | detailed business analysis, entity mappings & flowcharts | grep `series`, `LTS`, `vehicle`, `NFC`, `gate` |
| This file | `AGENTS.md` | entry point, conventions, context graph & workflow | grep `workflow`, `graph`, `grep`, `docs` |

Each doc has an index table with: **Name, File, Tags (keywords), Description**.
Tags include alternative names so agents find components even with different search terms.

---

## 2. Agent Workflow

### When given a task:

1. **Read this file** (done — you're here)
2. **Grep `context/memory.md`** (or `../PROJECT.md`) for domain context (business logic, voucher flows, lot conditions, prior decisions)
3. **Grep the relevant route/controller/service/model .md** for existing matching items
4. **Only read full files** when grep confirms relevance
5. **Implement** following conventions above (surgical, minimal, no comments in code)
6. **Update docs** — add new endpoints/controllers/services/models to index tables, update `memory.md` with decisions
7. **Run test/dev check** before finishing

### When adding a new endpoint/feature:

- Check if something similar exists in `routes.md`, `controllers.md`, or `services.md` (grep)
- Add tags/keywords and alternative names so future agents find it
- Add entry to the appropriate index table

### When making a decision:

- Log it in `context/memory.md` under Architecture Decisions or Business Logic

---

## 3. Self-Improving System

This is a **living context graph**. Every agent session should:

1. **Read** AGENTS.md (entry node)
2. **Traverse** only relevant doc nodes (grep, don't read all)
3. **Update** docs with new entries, tags, decisions
4. **Log taste** in memory.md — user preferences for style, patterns, approach
5. **Split** files that grow stale — if a .md becomes long, refactor into sub-docs

This creates a flywheel: each session enriches the graph, making future agents faster.

---

## 4. Important Reminders

- BE CONCISE. Sacrifice grammar for brevity.
- No emojis.
- No comments in code files.
- Every file max 200-500 lines.
- Think about reuse BEFORE you write.
- Always use `responseHandler.js` for API responses.
- Respect domain rules: LTS vouchers, lot conditions (SER, UNSE, RMJ, SEG), vehicle load states (Pending, Partially Loaded, Loaded).
- When in doubt, ask the user.
