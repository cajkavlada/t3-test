# 06 — Ordering a kitchen: ITS DevOps Marketplace

**FE covered:** Marketplace catalog; More info dialog; ITS DevOps Templates form; My requests → Orders; Waiting for approval → Orders (happy path with little/no friction).

**People:** Marcus (orders), Anna (uses resulting tools), Omar (approver if required).

**District:** **ITS** (DHL IT Services) — see [01](01-org-and-tools-primer.md).

---

## Metaphor

Selfservice gave them a whiteboard (Jira) and binder (Confluence).  
Now they want the **full IKEA kitchen**: counters (GitHub), pantry (Artifactory), inspector (Sonar), and plumbing for pipelines.

Marketplace tile **ITS DevOps Templates** is that kitchen box for the ITS district.

---

## Scene 1 — Browse Marketplace

Path: `/marketplace`

Marcus sees tiles (feature-flagged): ITS DevOps, CDaaS, OpenShift, AKS, GHE, CodeNOW, …

He opens **More info** on ITS DevOps.

| | Example |
|--|---------|
| **Input** | Click More info |
| **Output** | Explains GitHub + Artifactory + Sonar + reusable pipelines; links to DevSecOps resources |

He does **not** pick CDaaS — that’s the P&P district package (story 07).

---

## Scene 2 — Fill ITS request

Path: `/marketplace/request/its`

Form fields (conceptually): application/business service, acronym, owners, environments, classification, template options…

| | Example inputs |
|--|----------------|
| Acronym | `LUNCH` |
| Tenant / BU | ITS / GBS world |
| Business application | ServiceNow id for “Lunch Menu Display” |
| Owners | Marcus (+ maybe Anna) |
| Template choices | Java template / pipeline defaults |

**Submit** → tools `POST /api/v2/order/template/create` (or related).

| | Output |
|--|--------|
| SPEED | Order id, tasks (create GitHub bits, Artifactory project, Sonar project, …) |
| State | May go `APPROVAL_NEEDED` or auto toward `IN_PROGRESS` |

---

## Scene 3 — Track the order

Marcus opens **My requests → Orders** (`/my-page/requests/orders`).

| Order state (examples) | Meaning |
|------------------------|---------|
| `APPROVAL_NEEDED` | Omar must approve |
| `IN_PROGRESS` | Connectors working via Kafka |
| `COMPLETED` | Kitchen built |
| `VALIDATION_FAILED` / `FAILED` | Something wrong — open task details |
| `DENIED` / `CANCELLED` | Stopped |

If approval needed: Omar uses **Waiting for approval → Orders**, Approves → execution continues.

**Example task outputs (outside SPEED):**

- GitHub: repos `lunch-menu-api`, `lunch-menu-infra` + Actions enabled  
- Artifactory: project ready for `lunch-menu-api` artifacts  
- Sonar: project key `LUNCH...` with quality gate  
- SPEED workspace `LUNCH` components now list those URLs  

Anna clones the GitHub repo, pushes code → CI builds → jar to Artifactory → Sonar analysis on the PR.

---

## Scene 4 — Why this bundle?

| Tool in the kitchen | Role in Lunch Menu |
|---------------------|--------------------|
| GitHub | Store code + run pipelines |
| Artifactory | Store built jar/image versions |
| SonarQube | Fail PR if quality gate fails |

Ordering them separately via tickets = three queues, three naming schemes. One ITS template = one standard.

---

## Takeaway

Marketplace **order** ≠ permission request.  
Order = build the rooms. Permission request = cut keys (story 04).  
ITS template = ITS district’s standard kitchen.

Next: [07-parcel-division-cdaas.md](07-parcel-division-cdaas.md)
