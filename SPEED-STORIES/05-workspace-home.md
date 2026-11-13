# 05 — Workspace home: ownership, groups, applications

**FE covered:** My Page → workspaces list/detail; new group wizard; My applications; My global groups (user side); workspace request flow (`/my-page/workspaces/request/...`); My requests → workspaces / groups.

**People:** Marcus (owner), Anna (admin/member), Priya (helps if needed).

---

## Metaphor

A **workspace** is the team’s **folder on the city map** — the address under which tool rooms (components) and key rings (groups) are filed.

Acronym `LUNCH` is the **postal code** on the mailbox.

---

## Scene 1 — My workspaces list

Path: `/my-page/workspaces`

Marcus sees **Lunch Menu | LUNCH** because he is Owner.

| | Example |
|--|---------|
| **Input** | Open My workspaces |
| **Output** | Table row: name, acronym, tenant (e.g. DHL IT Services), role |

Empty components still OK: folder exists; kitchen appliances may come later (story 06).

---

## Scene 2 — Workspace detail

Path: `/my-page/workspaces/$id`

Tabs/panels: properties, users (Owner/Admin/Member), components list, permissions panel.

| | Example |
|--|---------|
| **Input** | Marcus opens LUNCH |
| **Output** | Sees Anna as Admin; components maybe Sonar/Artifactory/GitHub after a past order — or none yet |

From permissions panel he can add accounts / manage groups when allowed (Owner/Admin).

---

## Scene 3 — Create a workspace-local group

Path: `/my-page/workspaces/$id/new-group`

Wizard: information → properties (role code, tenant/realm if shown) → members → summary.

| | Example |
|--|---------|
| **Input** | Role code `READERS`, display name “Lunch readers”, members: intern “Sam” |
| **Naming** | Technical name built from tenant + acronym + role (SPEED naming rules) |
| **Output** | Group created; request may appear under **My requests → Groups**; Sam can be granted access patterns tied to that group |

This is a **NORMAL** group (workspace-scoped), not a global group.

---

## Scene 4 — Someone requests access to the workspace

Path: `/my-page/workspaces/request/$workspaceId` → `.../submitted`

A colleague **Nina** wants into Lunch workspace users/roles.

| | Example |
|--|---------|
| **Input** | Nina submits workspace access request with reason |
| **Output** | Submitted page; Marcus sees it under **My requests → Workspaces** / approval paths as designed |
| **Result** | Nina becomes Member/Admin per decision — still separate from Sonar group membership |

Workspace role ≠ Sonar group. Two locks on two doors.

---

## Scene 5 — My applications

Path: `/my-page/applications`

Marcus opens **My applications**.

| | Example |
|--|---------|
| **Input** | View applications tied to him / his orders |
| **Output** | Sees business application linkage (ServiceNow-oriented “official app” for Lunch Menu) |

Metaphor: the **legal business name** on the permit, not the mailbox code.

---

## Scene 6 — My global groups (user side)

Path: `/my-page/global-groups` (+ `/new` if allowed)

Anna browses global groups she owns/belongs to. Creating a new global group from My Page is the “user” twin of Admin create.

| | Example |
|--|---------|
| **Input** | Optional: create “Cafeteria Champions” global group with owners Marcus, members Anna |
| **Output** | `GLOBALGROUP` spanning workspaces; later used in permission requests |

---

## Takeaway

Workspace = address + ownership.  
Groups = keys for tools under that address.  
Applications = official business app label.  
Requests = paperwork to change ownership/membership.

Next: [06-ordering-a-kitchen-its.md](06-ordering-a-kitchen-its.md)
