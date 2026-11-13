# 09 — Bigger catalog: GHE, CodeNOW, clusters, JGenius, AI agents

**FE covered:** Marketplace OpenShift Cluster, AKS, OpenShift AppBox, JGenius (OpenShift + AKS), GHE Organization, CodeNOW; AI Agent Marketplace list/detail; My requests → ai-agents; Skills already in 02.

**People:** Marcus (ITS lead), Lea (curious), Anna (tries an AI agent).

---

## Metaphor

Stories 06–07 bought kitchens/apartments. This story walks the **rest of the mall food court** — rarer but real tiles. You don’t need all of them; you need to recognize what each booth sells.

---

## Scene 1 — “We need a whole Kubernetes building”

### ITS OpenShift Cluster — `/marketplace/request/openshiftCluster`

| Metaphor | Buy the whole apartment building (cluster) + kitchen kit (GitHub/Artifactory/Sonar) |
| Input | Cluster size/region-ish fields, acronym, owners, app linkage |
| Output | OpenShift cluster + DevSecOps tools wired; order under My requests → Orders |

### ITS OpenShift AppBox — `/marketplace/request/openshiftAppBox`

| Metaphor | Rent one apartment (namespace) in a shared building, not the whole tower |
| Output | AppBox namespace + same style tool integration |

### ITS Azure AKS — `/marketplace/request/aks`

| Metaphor | Same idea as OpenShift kitchen, but the building is Azure Kubernetes |
| Output | AKS cluster (± Postgres option per more-info) + GitHub/Artifactory/Sonar |

**Why clusters at all?** Containers need a place to run. GitHub stores code; Artifactory stores images; OpenShift/AKS **runs** them.

Example path after order:

1. CI builds image → Artifactory  
2. Deploy manifest points cluster at that image  
3. Service URL answers `GET /menus`

---

## Scene 2 — JGenius booths

Paths: `/marketplace/request/jgenius`, `/marketplace/request/jgenius-aks`

| Metaphor | Not only empty kitchen — also install a specific appliance brand (**JGenius** app) onto AppBox or AKS |
| Input | JGenius-specific parameters + infra choice |
| Output | Infra + JGenius deployment tasks in the order |

Use when the product is “give me JGenius running,” not “give me a blank cluster.”

---

## Scene 3 — GitHub (GHE) Organization only

Path: `/marketplace/request/ghe-org`

| Metaphor | Buy only the **company filing cabinet org**, not the full kitchen |
| Prerequisite | Owner accounts must **already exist** in GHE |
| Input | Org name, owners (Marcus, Anna) |
| Output | GHE organization; repos can be created under it later |

Business-unit allowlisting may apply (GBS/P&P style checks in code).

---

## Scene 4 — CodeNOW PaaS

Path: `/marketplace/request/codenow`

| Metaphor | Hire a **full-service hotel** for hybrid/multi-cloud DevSecOps instead of assembling IKEA parts |
| Input | CodeNOW form fields (team, env, …) |
| Output | CodeNOW project/onboarding; order/tasks tracked like others |

Note: SPEED microservices themselves often deploy *on* CodeNOW — platform eating its own cooking — but the Marketplace tile is for **teams ordering CodeNOW as a product**.

---

## Scene 5 — AI Agent Marketplace

Paths: `/ai-marketplace`, `/ai-marketplace/$id`

Anna browses agents (backed by `agentsUrl` / `speed-agents`, not in this folder).

| Input | Open an agent detail; submit access/order style request as UI defines |
| Output | Entry under **My requests → AI agents** (`/my-page/requests/ai-agents`) |

**Skills** nav (story 02) is the external AI site; **AI Agent Marketplace** is in-app catalog.

---

## Scene 6 — Components tab after fancy orders

When cluster/agent/component attach flows create pending work:

- **My requests → Components**  
- **Waiting for approval → Components** (if enabled)

Marcus opens a component request detail to see which tool URL is being attached to workspace `LUNCH`.

---

## Catalog cheat sheet

| Tile | Buys you |
|------|----------|
| ITS DevOps Templates | Kitchen without necessarily buying a whole cluster |
| CDaaS (P&P) | P&P turnkey golden stack |
| OpenShift Cluster / AppBox / AKS | Place to run containers (+ usually kitchen tools) |
| JGenius * | Cluster slice **and** JGenius app |
| GHE Org | GitHub Enterprise organization only |
| CodeNOW | PaaS onboarding |
| AI Agent Marketplace | AI agent products/access |

---

## Closing the series

You now have:

1. Map of districts (ITS/P&P) and utilities (LCM)  
2. Why each tool building exists  
3. Trivial login → Selfservice → permissions → workspace → ITS kitchen → CDaaS → Admin → exotic tiles  

SPEED’s benefit: **one permit office** so Anna doesn’t file five tickets in five dialects to get a standard, auditable toolkit and keys.

Back to [00-index.md](00-index.md) · Overview [`../SPEED-OVERVIEW.md`](../SPEED-OVERVIEW.md)
