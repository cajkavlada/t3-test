# 03 — Wiki and tickets: Selfservice Confluence + Jira

**FE covered:** Selfservice landing; Confluence create; Confluence groups list/create/edit; Jira create; Jira groups list/create/edit.

**People:** Anna (dev), Marcus (lead).

**Prerequisite primer:** Confluence = wiki, Jira = tickets ([01](01-org-and-tools-primer.md)).

---

## Metaphor

Before they buy a full kitchen (Marketplace), the team wants:

- a **whiteboard + ticket board** (Jira)
- a **shared binder for recipes/runbooks** (Confluence)

Selfservice is the **express counter** for those two Atlassian rooms only.

---

## Scene 1 — Selfservice landing

Marcus opens **Selfservice** (`/selfservice`).

He sees tiles/options for **Jira** and **Confluence** (flag `selfServiceEnabled`).

**Input:** navigate Selfservice.  
**Output:** chooses which express product to create.

---

## Scene 2 — Create a Confluence space

Path: `/selfservice/confluence/create`

Marcus fills the create-space form (name, key/acronym-like identifier, description, instance if asked).

| | Example |
|--|---------|
| **Input** | Space name `Lunch Menu Docs`, key `LUNCHDOC`, description “Runbooks for cafeteria API” |
| **SPEED** | Calls tools `/api/v1/devtools/confluence/...` |
| **Output in Confluence** | New space URL; empty home page waiting for content |
| **Output in SPEED** | Success dialog + link; space appears in managed inventory |

Anna later opens Confluence (outside SPEED) and writes page “How to deploy Lunch Menu API.” That writing is **not** done inside SPEED — SPEED only **created the room and keys**.

---

## Scene 3 — Confluence managed groups

Paths: `/selfservice/confluence/groups`, `/create`, `/edit/$id`

Marcus creates a managed group so only the team can edit the wiki.

| | Example |
|--|---------|
| **Input** | Group display name “Lunch Doc Editors”, members Anna + Marcus |
| **Output** | Group exists; membership synced toward Confluence permissions |
| **In UI** | Row visible in Confluence Groups grid; edit/delete later |

**Why groups here?** Confluence spaces don’t magically know Anna. Groups are the key rings.

---

## Scene 4 — Create a Jira project

Path: `/selfservice/jira/create`

| | Example |
|--|---------|
| **Input** | Project name `Lunch Menu`, key `LUNCH`, project type/template |
| **SPEED** | tools `/api/v1/devtools/jira/...` |
| **Output in Jira** | Project/board URL |
| **Output in SPEED** | Success + link |

Marcus creates ticket `LUNCH-1: Spike allergy API` **inside Jira**, not SPEED.

---

## Scene 5 — Jira managed groups

Paths: `/selfservice/jira/groups`, `/create`, `/edit/$id`

| | Example |
|--|---------|
| **Input** | Group “Lunch Jira Developers”, add Anna |
| **Output** | Anna can see/work LUNCH project per role mapping |

Edit group later: remove a contractor, add a newbie.

---

## What this story teaches

- Selfservice ≠ Marketplace. No Sonar/Artifactory/GitHub kitchen yet.
- Confluence and Jira are **optional separately**. Creating Confluence did not create Jira.
- SPEED’s job ends at **provision + group keys**; daily ticket/doc work happens in those tools.

**My Page angle (light):** after creation, related requests may show under My requests depending on flow; main proof is the external link + groups grid.

Next: [04-getting-access.md](04-getting-access.md)
