# 07 — Parcel district: CDaaS (P&P) with approval

**FE covered:** Marketplace CDaaS (P&P) form; business-unit gating; order approval + reject path; contrast with ITS.

**People:** Lea (P&P developer), Omar (approver), Priya (admin if cleanup needed).

---

## Metaphor

Lea works in the **P&P (Post & Parcel) district**, not ITS municipal engineering.

Her district sells a **turnkey furnished apartment**: **CDaaS** — Cloud DevOps as a Service — golden stack on Managed Azure (T-Systems), not the ITS OpenShift-flavored kitchen.

Same SPEED mall, different aisle.

---

## Scene 1 — Why Lea doesn’t use ITS DevOps tile

Lea’s Entra business unit maps to **P&P** (`PeP` claim → `P&P` in SPEED). Some marketplace routes check allowed business units (e.g. GBS/P&P lists).

| | Example |
|--|---------|
| **Input** | Lea opens Marketplace |
| **Output** | CDaaS (P&P) is *her* golden path; ITS tiles may be irrelevant or restricted by policy/flags |

**CDaaS** = the package name. **P&P** = who it’s for. Don’t confuse CDaaS with “continuous delivery” in general.

---

## Scene 2 — Order CDaaS

Path: `/marketplace/request/pnp`  
UI title: **CDaaS (P&P) Request**

| Example inputs | |
|----------------|--|
| Product / app name | `Parcel Label Printer Service` |
| Acronym | `PLPS` |
| Owners | Lea + Omar |
| Azure / stack options | As form requires (golden stack defaults) |

Submit → order created, often **needs approval**.

---

## Scene 3 — Omar approves (and a reject branch)

Omar: **Waiting for approval → Orders**.

**Happy path**

| Input | Approve |
| Output | Order → `IN_PROGRESS` → connectors create CDaaS workspace resources → `COMPLETED` |

**Reject path (teaching moment)**

| Input | Omar **Rejects** with reason “wrong cost center” |
| Output | Order/tasks **Denied**; Lea sees denial under My requests → Orders; no kitchen built |

Playwright coverage even has “rejected by approver” and “inactive tool user validation failed” style cases — governance is real.

---

## Scene 4 — After completion

Lea’s **My Page**:

- Workspace / application entries for PLPS  
- Components pointing at the CDaaS-provisioned tools  
- She still may need **permission requests** for teammates (story 04)

Tenant on the workspace: **P&P**, not ITS.

---

## Side-by-side

| | ITS DevOps (story 06) | CDaaS (this story) |
|--|----------------------|---------------------|
| District | ITS / DHL IT Services | P&P Post & Parcel |
| Metaphor | Standard IKEA kitchen | Turnkey furnished apartment |
| Typical cloud flavor | Often OpenShift/AKS ITS paths | Managed Azure golden stack |
| Same SPEED? | Yes | Yes |

---

## Takeaway

Tenants/divisions explain **why two marketplace tiles exist**.  
CDaaS is P&P’s productized DevSecOps offering inside SPEED.  
Approvals are part of the value (control), not a bug.

Next: [08-admin-city-hall.md](08-admin-city-hall.md)
