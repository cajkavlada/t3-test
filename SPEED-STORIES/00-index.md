# SPEED stories — index

Read these in order. Each story is a separate file. Together they cover every major frontend area at least once.

| # | File | Difficulty | What you learn |
|---|------|------------|----------------|
| 01 | [01-org-and-tools-primer.md](01-org-and-tools-primer.md) | Primer | Tenant, ITS, P&P, LCM, CDaaS + every tool (why / example inputs / outputs) |
| 02 | [02-trivial-first-day.md](02-trivial-first-day.md) | Trivial | Login, About, Profile, My Page empty state, Skills link |
| 03 | [03-wiki-and-tickets.md](03-wiki-and-tickets.md) | Easy | Selfservice Confluence + Jira + managed groups |
| 04 | [04-getting-access.md](04-getting-access.md) | Easy | Permission request, My permissions, approve/reject |
| 05 | [05-workspace-home.md](05-workspace-home.md) | Medium | Workspaces, new group, applications, workspace access request |
| 06 | [06-ordering-a-kitchen-its.md](06-ordering-a-kitchen-its.md) | Medium | Marketplace ITS DevOps order + My requests → Orders |
| 07 | [07-parcel-division-cdaas.md](07-parcel-division-cdaas.md) | Medium | CDaaS (P&P), business unit, approval on orders |
| 08 | [08-admin-city-hall.md](08-admin-city-hall.md) | Harder | Admin workspaces/groups/global groups/users/blacklist |
| 09 | [09-bigger-catalog.md](09-bigger-catalog.md) | Harder | GHE org, CodeNOW, OpenShift, AKS, JGenius, AI Agent Marketplace |

Parent overview: [`../SPEED-OVERVIEW.md`](../SPEED-OVERVIEW.md)

## FE coverage matrix

| Frontend area | Covered in |
|---------------|------------|
| Login / session / About SPEED / Profile / Skills | 02 |
| Selfservice landing, Jira create, Jira groups CRUD | 03 |
| Selfservice Confluence create, Confluence groups CRUD | 03 |
| New permission request | 04 |
| My permissions (workspace + global trees) | 04 |
| Waiting for approval → permissions / groups / components | 04, 08 |
| My Page → workspaces list/detail, new group | 05 |
| My Page → applications | 05 |
| My Page → global groups (+ create) | 05, 08 |
| Workspace permission request flow | 05 |
| My requests → permissions / groups / workspaces | 04, 05 |
| Marketplace catalog + More info | 06, 07, 09 |
| Marketplace ITS DevOps Templates | 06 |
| My requests → orders + waiting approval → orders | 06, 07 |
| Marketplace CDaaS (P&P) | 07 |
| Admin workspaces create/detail | 08 |
| Admin blacklist | 08 |
| Admin groups create | 08 |
| Admin global groups create | 08 |
| Admin users | 08 |
| Marketplace OpenShift / AKS / AppBox / JGenius | 09 |
| Marketplace GHE Organization | 09 |
| Marketplace CodeNOW | 09 |
| AI Agent Marketplace + My requests → ai-agents | 09 |
| My requests → components | 08, 09 |

Recurring cast:

- **Anna** — developer
- **Marcus** — tech lead / workspace owner
- **Priya** — LCM admin (`lcm-admin`)
- **Tom** — security / cross-team
- **Lea** — P&P developer (parcel side)
- **Omar** — business / app owner who approves some orders
