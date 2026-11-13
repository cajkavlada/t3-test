# 04 — Getting access: permission requests and approvals

**FE covered:** `/new-permission-request`; My permissions; My requests → permissions / groups; Waiting for approval → permissions / groups / components; decide approve/reject.

**People:** Anna (needs access), Marcus (approver), Tom (already in a global group).

---

## Metaphor

Tools are buildings. **Groups are key rings.**  
A permission request is Anna filling a **key request form** at the permit office. Marcus stamps it. Connectors cut the physical key in the real building (Sonar/Jira/…).

---

## Setup (assume already exists)

Workspace **Lunch Menu** acronym `LUNCH` has component groups:

- `LUNCH-SONAR-USERS`
- `LUNCH-SONAR-ADMINS`

Global group:

- `LCM-SONAR-USERS` (platform-wide read-ish Sonar club — Tom is in it)

Anna has **no** `LUNCH-SONAR-USERS` yet. She cannot open the Sonar project dashboard meaningfully.

---

## Scene 1 — Anna looks at My permissions

Path: `/my-page/permissions`

She opens **Workspaces** subtab and **Global groups** subtab.

| | Example |
|--|---------|
| **Input** | Browse trees |
| **Output** | Sees she lacks Lunch Sonar groups; maybe sees nothing under Lunch |

This is the **inventory of keys she already holds**.

---

## Scene 2 — New permission request

Path: `/new-permission-request`

Anna:

1. Selects **herself** as affected user (could also request for a colleague).
2. Searches workspace Lunch → expands components → selects **Grant** on `LUNCH-SONAR-USERS`.
3. Optionally searches global groups — she does **not** take `LCM-SONAR-ADMINS` (that would be overkill / maybe not requestable the same way).
4. Submits.

| | Example |
|--|---------|
| **Input body (conceptually)** | `groupsToGrant`: ACCESS → [`LUNCH-SONAR-USERS`] |
| **SPEED** | RBAC creates Task type `PERMISSION_REQUEST` |
| **Output** | Request id; appears under **My requests → Permissions** as pending |

Groups containing `WS_ADMIN_STD` stay disabled — those keys are not self-serve.

---

## Scene 3 — Marcus approves

Marcus opens **Request waiting for my approval → Permissions**  
(`/my-page/requests-waiting-approval/permissions`).

| | Example |
|--|---------|
| **Input** | Open request; **Approve** (decide API) |
| **Output** | Task progresses; Kafka/connectors sync Anna into Sonar group |
| **Reject path** | He could Deny → Anna sees denied under My requests |

Same area has tabs for **Groups** and **Components** waiting approval (component tab depends on feature flag).

---

## Scene 4 — Anna verifies

1. **My requests → Permissions** → status Done.  
2. **My permissions** → Lunch → Sonar users group visible.  
3. Outside SPEED: Sonar project allows her in.

**Revoke example:** Marcus later requests revoke of a contractor’s `LUNCH-SONAR-USERS` via same wizard (`groupsToRevoke`).

---

## Scene 5 — Group request flavor

If Anna instead asked “create/join a managed group workflow,” she might land under **My requests → Groups** / waiting-approval **Groups** (`GROUP_REQUEST`). Same building, different form type.

---

## Takeaway

Permissions in SPEED ≈ **membership in groups**, not a separate ACL UI per file.  
Approvals protect the key cabinet.  
Global groups (Tom) vs workspace groups (Anna’s Lunch Sonar) = master city keys vs apartment keys.

Next: [05-workspace-home.md](05-workspace-home.md)
