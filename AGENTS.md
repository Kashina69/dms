# Agent Guide

**This file is the workspace entry point. Both backend and frontend are configured as token-efficient context graphs.**

---

## Quick Navigation

- **Backend Entry Node**: [backend/AGENTS.md](file:///home/ubuntu/code/office/projects/dms/backend/AGENTS.md)
- **Backend Project Info**: [backend/PROJECT.md](file:///home/ubuntu/code/office/projects/dms/backend/PROJECT.md)
- **Frontend Entry Node**: [frontend/AGENTS.md](file:///home/ubuntu/code/office/projects/dms/frontend/AGENTS.md)
- **Frontend Project Info**: [frontend/PROJECT.md](file:///home/ubuntu/code/office/projects/dms/frontend/PROJECT.md)
- **Full Domain Knowledge & Business Logic**: [PROJECT.md](file:///home/ubuntu/code/office/projects/dms/PROJECT.md)

---

## Token-Efficient Context Retrieval

To maintain token efficiency, fetch ONLY the exact line ranges below when you need specific context:

### Workspace Graph Entry
- **Root Agent Map**: [AGENTS.md](./AGENTS.md#L1-L65)
- **Business Flow Master**: [PROJECT.md](./PROJECT.md#L1-L60), [PROJECT.md](./PROJECT.md#L100-L203), [PROJECT.md](./PROJECT.md#L235-L403)

### Backend ([backend/PROJECT.md](./backend/PROJECT.md))
- **Stack Details**: [backend/PROJECT.md#L3-L12](./backend/PROJECT.md#L3-L12)
- **Commands**: [backend/PROJECT.md#L13-L21](./backend/PROJECT.md#L13-L21)
- **Folder Structure**: [backend/PROJECT.md#L22-L41](./backend/PROJECT.md#L22-L41)
- **Code Conventions & Best Practices**: [backend/PROJECT.md#L42-L62](./backend/PROJECT.md#L42-L62)

### Frontend ([frontend/PROJECT.md](./frontend/PROJECT.md))
- **Stack Details**: [frontend/PROJECT.md#L3-L14](./frontend/PROJECT.md#L3-L14)
- **Commands**: [frontend/PROJECT.md#L15-L28](./frontend/PROJECT.md#L15-L28)
- **Folder Structure**: [frontend/PROJECT.md#L29-L62](./frontend/PROJECT.md#L29-L62)
- **Code Conventions & Best Practices**: [frontend/PROJECT.md#L63-L84](./frontend/PROJECT.md#L63-L84)

---

## 1. Reference Docs (Context Graph)

This is the graph of interconnected project knowledge. Start at the root node, then follow the relevant business or implementation branch only. Do not read whole files unless grep confirms a direct match.

| Doc | Path | Scope | What it tracks | Start line(s) |
| --- | --- | --- | --- | --- |
| Root Entry | [AGENTS.md](./AGENTS.md#L1-L65) | Shared | Workspace-wide routing, graph workflow, lookup rules | L1-L65 |
| Business Flow Master | [PROJECT.md](./PROJECT.md#L1-L60) | Shared | Domain summary, terms, and overall DMS flow | L1-L60 |
| Business Flow Graph | [PROJECT.md](./PROJECT.md#L100-L203) | Shared | LTS / vehicle / loading lifecycle, flowcharts | L100-L203 |
| Drawl Lifecycle Notes | [PROJECT.md](./PROJECT.md#L296-L403) | Shared | Raw app flow translated to data-model terms, status changes, graph references | L296-L403 |
| Backend Entry | [backend/AGENTS.md](./backend/AGENTS.md#L1-L96) | Backend | Backend graph, route/service/model lookup workflow | L1-L96 |
| Backend Project | [backend/PROJECT.md](./backend/PROJECT.md#L1-L62) | Backend | Stack, folders, conventions | L1-L62 |
| Frontend Entry | [frontend/AGENTS.md](./frontend/AGENTS.md#L1-L96) | Frontend | Frontend graph, module/component lookup workflow | L1-L96 |
| Frontend Project | [frontend/PROJECT.md](./frontend/PROJECT.md#L1-L84) | Frontend | Stack, folders, conventions | L1-L84 |
| Back-end Memory | [backend/context/memory.md](./backend/context/memory.md) | Backend | DMS business rules, 6 core flows, condition flags & decisions | use grep |
| Frontend Memory | [frontend/context/memory.md](./frontend/context/memory.md) | Frontend | Frontend architecture, state conventions & scanner flows | use grep |
| Backend Routes | [backend/routes/routes.md](./backend/routes/routes.md) | Backend | API endpoint declarations & router definitions | use grep |
| Backend Controllers | [backend/controllers/controllers.md](./backend/controllers/controllers.md) | Backend | Request handlers, payload validation & responses | use grep |
| Backend Services | [backend/services/services.md](./backend/services/services.md) | Backend | Database queries, calculations & sync logic | use grep |
| Backend Models | [backend/models/models.md](./backend/models/models.md) | Backend | Sequelize schemas, data models & associations | use grep |
| Frontend Modules | [frontend/src/modules.md](./frontend/src/modules.md) | Frontend | Feature modules, page views & primary components | use grep |
| Frontend Routes | [frontend/src/routing/routes.md](./frontend/src/routing/routes.md) | Frontend | React router routes, route constants & protection | use grep |
| Frontend Components | [frontend/src/components.md](./frontend/src/components.md) | Frontend | Shared UI components, modals, forms, tables & layouts | use grep |
| Frontend Events | [frontend/src/api/events.md](./frontend/src/api/events.md) | Frontend | Axios interceptor, API event services & payloads | use grep |

### Query-to-location map

Use these as entry points when the task is about a business flow or implementation detail:

- If the question is about the business meaning of LTS / series / drawl: start at [PROJECT.md](./PROJECT.md#L296-L403)
- If the question is about the actual DMS process flow: read [PROJECT.md](./PROJECT.md#L100-L203) and then jump to the matching backend/frontend docs
- If the question is about backend implementation: start from [backend/AGENTS.md](./backend/AGENTS.md#L20-L69), then grep the route/controller/service/model docs
- If the question is about frontend screens and status: start from [frontend/AGENTS.md](./frontend/AGENTS.md#L20-L69), then grep module/route/component/event docs

### Graph traversal rule

1. Identify the keyword(s): `series`, `LTS`, `drawl`, `vehicle`, `NFC`, `load_status`, `gate`, `AMK`
2. Grep the relevant doc node first
3. Read only the exact matching section or the specific file range that matches the keyword
4. Cross-link into implementation docs only when the business graph requires it
5. Update this graph when a new flow or component is added

---

## 2. Agent Workflow

1. **IDENTIFY** keywords for your task
2. **GREP** the relevant `.md` node for those keywords (avoid full reads)
3. **READ** only targeted lines/files confirmed by grep
4. **EXECUTE** minimal, surgical changes adhering to DMS business rules
5. **UPDATE** index tables and `memory.md` with new additions or decisions

---

## 3. Self-Improving Knowledge Loop

This project is meant to improve itself over time. Every agent session should add only high-value, business-critical facts that affect flow understanding, edge-case handling, or module behavior.

### Rules for the self-learning loop

- Only add knowledge that is important for future tasks, real app behavior, business logic, or module integration.
- Keep updates concise and surgical: one new fact, one new flow note, or one new edge-case warning at a time.
- Always update the business graph in [PROJECT.md](./PROJECT.md) when a new execution path, user flow, edge case, or rule is learned.
- Use references, not vague summaries: point to the exact app area, table, flow, function, or screen involved.
- Do not add generic or low-value notes like styling, color-only preferences, or boilerplate implementation details.
- If a fact is only useful once and not likely to be reused, do not write it into the main graph; keep it in the task/session context only.

### What counts as a valuable update

A good update is something like:

- a user flow that explains how a module actually works in production
- an edge case that breaks a process if missed
- a real relationship between tables, screens, or roles
- a business rule that affects dispatch logic, loading status, series assignment, or gate validation
- a code-to-flow mapping that helps future agents understand why a feature exists

### Update pattern

When the agent learns something meaningful, it should:

1. confirm the fact against the code, route, model, screen, or business flow
2. add a focused note in [PROJECT.md](./PROJECT.md) near the relevant flow section
3. include the exact key terms, entity names, and references to the relevant code or document lines
4. update the index/reference graph in this file if the new fact changes routing, flow understanding, or module discovery
5. avoid rewriting broad sections unless the new fact changes the core interpretation of the flow

### Minimal update example

Example pattern for a valid self-learning update:

- A new fact: "The vehicle is not the LTS; the LTS is assigned to the vehicle via `assigned_lts_issue_voucher_details`"
- Place it in [PROJECT.md](./PROJECT.md#L296-L403) under the raw lifecycle section
- Link it to [PROJECT.md](./PROJECT.md#L133-L162) and [PROJECT.md](./PROJECT.md#L166-L203)
- Keep it 3-6 lines, no fluff

### Anti-patterns to avoid

- Do not log every UI click or every minor label change
- Do not add huge narrative dumps for every task
- Do not duplicate the same rule across multiple docs without reason
- Do not enrich the graph with speculative or guessed details
- Do not add business details unrelated to the flow or module under work

### Operational rule for future agents

Every time a new fact is learned from code, business review, a user explanation, or a bug fix, ask:

- Is this part of the actual system flow?
- Will future agents need this to understand a module or bug?
- Is this a real rule or just a one-off task detail?
- Does it belong in [PROJECT.md](./PROJECT.md) or only in local task memory?

If the answer is yes to the first three, add it as a focused graph update. If not, keep it out.

---

## 4. Important Reminders

- Keep the system compact, not noisy.
- Prefer business-critical knowledge over generic documentation.
- Treat [PROJECT.md](./PROJECT.md) as the long-term domain memory graph.
- Make updates only when they improve future understanding of the real system.
- When in doubt, reduce scope instead of adding fluff.
