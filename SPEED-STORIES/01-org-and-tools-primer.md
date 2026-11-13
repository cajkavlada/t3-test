# 01 — World map: tenants, ITS, LCM, CDaaS, and every tool

Metaphor for the whole company: **DHL is a huge city**. SPEED is the **city permit office + hardware store combo** where neighborhoods order standard toolkits and get keys cut for the right people.

---

## Tenant (which neighborhood’s building code?)

A **tenant** is not a “customer login.” It is a **partition / neighborhood** inside SPEED.

Imagine the city has districts. Each district has its own fire code and preferred contractors:

| Tenant (from FE realms) | Display name | Metaphor |
|-------------------------|--------------|----------|
| `ITS` | DHL IT Services | The big “internal IT construction” district |
| `PNP` | P&P (Post & Parcel) | The “parcel delivery product” district |

When you create a workspace you pick a tenant. Same word “workspace,” but:

- naming rules and available templates can differ
- acronym uniqueness is **per tenant** (two districts can both have a shop called `INV` in theory; SPEED tracks them separately)
- which marketplace tiles you care about often follows your business unit

**Analogy:** Choosing tenant = choosing which district office stamps your building permit.

---

## ITS (DHL IT Services)

**ITS** = one large internal IT organization that builds and runs software for DHL.

In SPEED, “ITS” shows up as:

- a **tenant** (`DHL IT Services`)
- marketplace products like **ITS DevOps Templates**, **ITS OpenShift Cluster**, **ITS Azure AKS**, **ITS OpenShift AppBox**

**Analogy:** ITS is the municipal engineering corps. Their “standard house kit” is the ITS DevOps template: GitHub + Artifactory + SonarQube + reusable pipelines (± somewhere to deploy).

If Anna works on an internal IT product, she usually lives in the ITS neighborhood.

---

## P&P (Post & Parcel)

**P&P** = the Post & Parcel division (parcels, delivery products). In Entra claims it may appear as `PeP`; in SPEED UI as **P&P**.

They have their own preferred “golden” stack.

**Analogy:** A different district with its own preferred contractors and cloud landlord (Managed Azure by T-Systems in CDaaS copy).

---

## CDaaS (Cloud DevOps as a Service) — for P&P

**CDaaS** is **not** a random acronym for “CD.” In SPEED Marketplace it is the tile **“CDaaS (P&P)”**:

> Golden Stack turn-key DevSecOps workspace for P&P … CI/CD and Infrastructure as Code on Managed Azure by T-Systems.

So:

- **CDaaS** = the *product/package* P&P teams order
- **P&P** = the *division / tenant neighborhood* that package is for

**Analogy:**

- ITS DevOps Templates = IKEA kitchen for the ITS district  
- CDaaS = turnkey furnished apartment package sold only in the P&P district (golden stack)

Lea (P&P developer) orders CDaaS, not because she loves the letters, but because that is her division’s approved full toolkit.

---

## LCM (Lifecycle Management)

**LCM** historically = **Lifecycle Management** — the platform/org that managed tool identity and access (Crowd, Atlassian directories, group sync). SPEED’s RBAC service still comes from that “platform-service” world.

You will see LCM as:

- **`lcm-admin`** Entra role → can open SPEED **Admin** (city hall keys)
- Group name prefixes like **`LCM-SONAR-ADMINS`** → platform-wide Sonar admin club, not “Anna’s one project”
- Test data like workspace “Lifecycle Management Platform | LCM”

**Analogy:** LCM is the **utilities & keys department**. They don’t write Invoice Portal features. They run the master key cabinet and the wiring rules for the city’s tool buildings. Priya with `lcm-admin` is a clerk with master keys.

LCM is **not** a marketplace tile like CDaaS. It is heritage + admin/power naming.

---

## Big picture diagram

```text
DHL city
├── District ITS  ── tenant "DHL IT Services"
│     └── standard kit: ITS DevOps / OpenShift / AKS templates
├── District P&P  ── tenant "P&P"
│     └── standard kit: CDaaS (P&P)
└── Utilities LCM ── identity, groups, Admin, many LCM-* global groups
      └── SPEED is the permit desk that talks to all tool buildings
```

---

## Why each tool exists (with toy examples)

Think of building a small app **“Lunch Menu API”** for cafeteria displays.

### GitHub / GitHub Enterprise (GHE)

**Why:** Where source code lives; pull requests; CI (GitHub Actions) often starts here.

| | Example |
|--|---------|
| **Input** | Anna pushes branch `feat/soup-endpoint` with Java code |
| **What happens** | PR review, Actions workflow runs tests |
| **Output** | Merged `main`, green/red CI check, link to commit |

Without GitHub you have code on laptops and USB sticks. Chaos.

GHE = GitHub Enterprise (company-controlled / data-resident instance). Marketplace “GHE Organization Creation” = create a company org folder for a team’s repos.

### Artifactory

**Why:** After CI builds, the **binary** (jar, Docker image, npm package) must live somewhere versioned so servers install *exactly* `lunch-menu-api:1.4.2`, not “whatever was on Anna’s laptop.”

| | Example |
|--|---------|
| **Input** | CI uploads `lunch-menu-api-1.4.2.jar` |
| **What happens** | Stored under team’s Artifactory project/repo with permissions |
| **Output** | Deploy job downloads that jar/image by version |

Warehouse for build products. Not the source code; the **packaged result**.

### SonarQube

**Why:** Automatic code quality / security review so bad patterns don’t silently ship.

| | Example |
|--|---------|
| **Input** | CI sends analysis of Anna’s PR |
| **What happens** | Sonar scans for bugs, smells, vulnerabilities, coverage |
| **Output** | Dashboard: “3 bugs, quality gate failed” or “passed” |

Like a building inspector’s report before you get the occupancy certificate.

### Jira

**Why:** Track **work**: bugs, stories, sprints — not the code itself.

| | Example |
|--|---------|
| **Input** | Marcus creates ticket `LUNCH-12: Add allergy flags` |
| **What happens** | Team assigns, moves across board columns |
| **Output** | Done ticket linked to PR; audit of who decided what |

Selfservice “create Jira” = create the project/board for the team. SPEED does not replace writing tickets inside Jira.

### Confluence

**Why:** Team **wiki** — how to run the service, architecture decisions, onboarding. Not tickets; documents.

| | Example |
|--|---------|
| **Input** | Anna writes page “How to restart Lunch Menu API” |
| **What happens** | Page lives in Confluence space with edit/view permissions |
| **Output** | New teammate finds runbook without Slack archaeology |

Yes, it is “documentation of sorts.” It is a proper shared wiki with permissions, search, and history — not a Google Doc floating privately.

**Jira ≠ Confluence.** Tickets vs docs. Often used together; SPEED can create either without forcing the other.

### DefectDojo

**Why:** Collect and manage **security findings** from scanners over time (what’s open, what’s risk-accepted).

| | Example |
|--|---------|
| **Input** | Scanner finds “outdated dependency CVE-2024-…” |
| **What happens** | Finding tracked in Dojo with status |
| **Output** | Security/devs see backlog of vulns to fix |

### Checkmarx

**Why:** Another security scanning product (SAST). Connector exists so SPEED can talk to it when provisioning/syncing that part of the stack.

### Terraform / Terraform Cloud

**Why:** Describe cloud infrastructure as code (“create this cluster/network”) and apply it repeatedly.

| | Example |
|--|---------|
| **Input** | Terraform config “AKS cluster size 3” |
| **What happens** | Terraform apply via connected cloud |
| **Output** | Real Kubernetes cluster exists |

### OpenShift / AKS (Azure Kubernetes Service)

**Why:** Places where containers **run** in production/test.

| | Example |
|--|---------|
| **Input** | Deploy image `lunch-menu-api:1.4.2` |
| **What happens** | Cluster schedules pods, exposes service |
| **Output** | API reachable at an internal URL |

- **OpenShift** = Red Hat Kubernetes platform (common in ITS templates)  
- **AKS** = Azure’s managed Kubernetes  
- **AppBox** = lighter “namespace/slice” of a shared OpenShift (apartment in a building vs owning the whole building)

### CodeNOW

**Why:** A **PaaS** (platform as a service) that wraps a lot of cloud/DevSecOps complexity so teams develop faster. Also the platform SPEED itself is often deployed on. Marketplace tile = order CodeNOW for a team.

### ServiceNow

**Why:** Enterprise ITSM / CMDB — catalog of business applications and services. SPEED orders/workspaces often link to a **business application ID** so finance/ops know which “official app” owns the tools.

| | Example |
|--|---------|
| **Input** | Business app “Lunch Menu Display” ID from ServiceNow |
| **What happens** | Attached to workspace/order |
| **Output** | Audit: these GitHub/Sonar resources belong to that business app |

### Crowd / AD / Entra

**Why:** Know **who humans are** and sometimes which directory groups they belong to.

- **Entra (Azure AD)** — how you log into SPEED  
- **AD / LDAP** — corporate directory lookups when picking users  
- **Crowd** — Atlassian-oriented directory used in LCM heritage for tool access sync  

---

## How SPEED uses these tools (one sentence each)

| Tool | SPEED’s job |
|------|-------------|
| GitHub/GHE | Create orgs/repos/pipelines wiring as part of templates |
| Artifactory | Create projects + permission groups for artifacts |
| SonarQube | Create projects + permission templates/groups |
| Jira / Confluence | Selfservice create spaces/projects + managed groups |
| OpenShift / AKS / Terraform | Provision runtimes/infra from marketplace |
| DefectDojo / Checkmarx | Security tooling in the connector landscape |
| ServiceNow | Tie workspaces/orders to official business apps |
| Entra/AD/Crowd | Login + user pickers + sync memberships into tools |

SPEED is the **permit desk**. The tools are the **actual buildings** where work happens.

Next: [02-trivial-first-day.md](02-trivial-first-day.md)
