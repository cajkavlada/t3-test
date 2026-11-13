# 02 — Trivial story: Anna’s first day in SPEED

**FE covered:** Login, auth callback, About SPEED, Profile, My Page landing, Skills external link, forbidden/unauthorized awareness.

**People:** Anna (new developer).

---

## Metaphor

Anna gets a **keycard** to the city permit office (SPEED). On day one she doesn’t build anything. She learns where the lobby, info desk, and her locker are.

---

## Scene 1 — Login

1. Anna opens SPEED in the browser.
2. She signs in with **Entra ID** (company Microsoft account).
3. Browser returns via `/auth/callback` with a token.
4. SPEED stores the session; idle timeout may later show session-expired UI.

**Input:** company email + password / SSO.  
**Output:** authenticated SPA; nav shows Selfservice, Marketplace, AI Agent Marketplace, My Page (Admin hidden — she is not `lcm-admin`).

If she had no access at all she might see **unauthorized**. If she tried Admin without role → **forbidden**.

---

## Scene 2 — About SPEED

Anna opens the drawer **About SPEED** (bottom nav / menu).

She reads: SPEED automates provisioning across GitHub, Artifactory, SonarQube, Jira, Confluence, DefectDojo; benefits = self-service, standardization, governance, integration, audit trail.

She also sees links: DevSecOps Portal, Helpdesk, privacy, terms — and service versions (tools/rbac/…).

**Input:** click About.  
**Output:** mental model + where to get help. No resources created.

---

## Scene 3 — Profile

Anna opens **Profile**.

**Input:** view profile.  
**Output:** sees her identity as SPEED knows it (from Entra / directory). Confirms she’s “Anna,” not a shared account.

---

## Scene 4 — My Page (almost empty)

Anna opens **My Page**.

Depending on flags she sees tabs like My workspaces / applications / global groups, My requests, Request waiting for my approval, My permissions.

Today:

- Workspaces list empty or only things someone else already shared
- Requests empty
- Permissions empty or thin

**Input:** browse tabs.  
**Output:** she understands “this is my locker wall” — later stories fill it.

---

## Scene 5 — Skills link

Anna taps **Skills** in the nav.

**Input:** click.  
**Output:** leaves SPEED to `https://speed.dhl.com/ai/` (external). Separate from ordering tools inside SPEED.

---

## What she did *not* do yet

No Jira, no marketplace order, no groups. That’s intentional — trivial story.

**Takeaway:** SPEED is a gated portal. First day = identity + orientation. Value starts when she creates or requests something (stories 03+).

Next: [03-wiki-and-tickets.md](03-wiki-and-tickets.md)
