# Agent Guide

**This file is the entry point. Context docs below are graph nodes — grep before full read.**

---

## Token-Efficient Context Retrieval

To maintain token efficiency, this project keeps detailed specifications in `PROJECT.md`. **Be surgical in your searches.** DO NOT read `PROJECT.md` in its entirety. Instead, use your file viewing tools to fetch ONLY the exact line ranges below when you need specific context:

- **Stack Details**: [PROJECT.md#L3-L14](./PROJECT.md#L3-L14)
- **Commands**: [PROJECT.md#L15-L28](./PROJECT.md#L15-L28)
- **Folder Structure**: [PROJECT.md#L29-L62](./PROJECT.md#L29-L62)
- **Code Conventions & Best Practices**: [PROJECT.md#L63-L84](./PROJECT.md#L63-L84)

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

### Graph links for this frontend branch

- Root workspace node: [../AGENTS.md](../AGENTS.md#L1-L65)
- Business flow master: [../PROJECT.md](../PROJECT.md#L1-L60), [../PROJECT.md](../PROJECT.md#L100-L203), [../PROJECT.md](../PROJECT.md#L296-L403)
- Backend branch: [../backend/AGENTS.md](../backend/AGENTS.md#L1-L96)
- Frontend project quick refs: [PROJECT.md](./PROJECT.md#L1-L84)

### Doc Index

| Doc | Path | What it tracks | Lookup anchors |
| --- | --- | --- | --- |
| Modules | `src/modules.md` | Feature modules, page views & primary components | grep `Manage Series`, `ManageLts`, `TrackLoading`, `Vehicle List` |
| Routes | `src/routing/routes.md` | React router routes, route constants & protection | grep `route`, `path`, `private`, `auth` |
| Components | `src/components.md` | Shared UI components, modals, forms, tables & layouts | grep `Modal`, `Table`, `Form`, `Card` |
| API & Events | `src/api/events.md` | Axios interceptor, API event services & payloads | grep `axios`, `api`, `event`, `sync` |
| Project Memory | `context/memory.md` | Frontend architecture, state conventions & scanner flows | grep `scanner`, `LTS`, `series`, `NFC`, `loading` |
| Knowledge Transfer | `../PROJECT.md` | Full domain analysis, entity mappings & flowcharts | grep `series`, `LTS`, `vehicle`, `NFC`, `gate` |
| This file | `AGENTS.md` | Entry point, conventions, context graph & workflow | grep `workflow`, `graph`, `grep`, `docs` |

Each doc has an index table with: **Name, File, Tags (keywords), Description**.
Tags include alternative names so agents find components even with different search terms.

---

## 2. Agent Workflow

### When given a task:

1. **Read this file** (done — you're here)
2. **Grep `context/memory.md`** (or `../PROJECT.md`) for domain context (LTS vouchers, lot conditions, scanner flow, prior decisions)
3. **Grep the relevant module/route/component/event .md** for existing matching items
4. **Only read full files** when grep confirms relevance
5. **Implement** following conventions above (surgical, minimal, no comments in code)
6. **Update docs** — add new components/routes/events to index tables, update `memory.md` with decisions
7. **Run build/test check** before finishing

### When adding a new component:

- Check if something similar exists in `components.md` or `modules.md` (grep)
- Add tags/keywords and alternative names so future agents find it
- Add entry to the appropriate index table

### When making a decision:

- Log it in `context/memory.md` under Architecture Decisions or Taste/Preferences

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
- Always use `apiInterceptor.js` for API requests.
- Respect domain rules: LTS vouchers, lot conditions (SER, UNSE, RMJ, SEG), vehicle load states (Pending, Partially Loaded, Loaded).
- When in doubt, ask the user.
