# 08 — City hall: Admin workspaces, groups, users, blacklist

**FE covered:** Admin nav (lcm-admin); Admin workspaces list/create/detail; blacklist; Admin groups + create; Admin global groups + create; Admin users; My requests → components; waiting approval components/groups as admin-ish ops.

**People:** Priya (`lcm-admin`), Marcus (owner), Tom (security).

---

## Metaphor

Priya works at **city hall** (LCM utilities). She has the **master keycard** (`lcm-admin`). Normal developers never see the Admin menu.

---

## Scene 1 — Admin gate

Priya logs in → **Admin** appears in nav. Anna still doesn’t see it.

Path: `/admin` → tabs Workspaces | Groups | Global groups | Users.

---

## Scene 2 — Create workspace from Admin

Path: `/admin/workspaces/new`

Priya creates a workspace that didn’t come from Marketplace (or pre-creates the folder).

| Example inputs | |
|----------------|--|
| Name | `Lifecycle Demo Lab` |
| Acronym | `LDLAB` |
| Tenant | DHL IT Services |
| Approver workflow | `OneApprover` |
| Owners | Marcus |
| Admins | Anna |
| Category | SOFTWARE |

| Output | Workspace in DB; Kafka may trigger default group creation; appears in Admin list + Marcus’s My workspaces |

Detail: `/admin/workspaces/$id` — Priya inspects users/components.

---

## Scene 3 — Blacklist (blocked acronyms)

Path: `/admin/workspaces/blacklist`

Someone tries acronym `DHL` or a reserved brand code — policy says no.

| Input | Priya adds acronym `DHL` to blacklist (or CSV upload) |
| Output | State stored as **BlockedAcronym**; create workspace with `DHL` fails |
| Remove | Priya deletes entry when policy changes |

**UI says Blacklist; API says blocked-acronyms.** Same thing: forbidden mailbox codes.

---

## Scene 4 — Admin create group

Path: `/admin/groups`, `/admin/groups/new`

Priya creates a NORMAL group for LDLAB when owners can’t / shouldn’t.

| Input | Tenant, workspace/component context, role code, members |
| Output | Group in RBAC; sync toward end tools |

Search/filter Admin Groups grid; open drawer; add account actions.

---

## Scene 5 — Admin global groups

Path: `/admin/global-groups`, `/admin/global-groups/new`

Tom needs cross-city Sonar powers.

| Input | Create global group `LCM-SONAR-ADMINS` (or add Tom as member/owner to existing) |
| Output | `GLOBALGROUP`; owners managed; used in permission trees city-wide |

Priya adds Tom as **Owner** of a security global group; later Anna’s permission UI can surface it when searching globals.

---

## Scene 6 — Admin users

Path: `/admin/users`

Priya searches Anna.

| Input | Search email/name |
| Output | Drawer: user info, permissions tab, global groups tab; richer fields if IDP admin attributes exist |

This is the **phone book + key inventory** for a person.

---

## Scene 7 — Component requests (ops view)

When teams request attaching/changing components, items show under **My requests → Components** and **Waiting for approval → Components** (flag `approvalComponentRequestsEnabled`).

| Input | Approver decides component request |
| Output | Workspace gains/updates a component link (e.g. register existing Sonar URL) |

Even if the flag is off in some envs, the routes exist — know they mean “change the appliances listed on the folder.”

---

## Takeaway

Admin = LCM city hall.  
Blacklist = forbidden acronyms.  
Global groups = city-wide key rings.  
Users screen = inspect anyone’s keys.  
Developers use My Page; Priya uses Admin when standards or cleanup need a master key.

Next: [09-bigger-catalog.md](09-bigger-catalog.md)
