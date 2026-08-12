# Concept Brief: The Unified Post-Sales "Outcome Engine"

## What It Is

A single system of engagement — **ASPIRE** (*Automated Services & Post-sales
Intelligent Resolution Engine*) — that replaces three disconnected tools
(DeliveryOps for PS project delivery, CustomerPulse for CS health/renewals,
DealCRM for the account record) with one workbench spanning the full
post-sales lifecycle: deal closes → deployment → adoption → renewal.
CustomerPulse is now an active integration, not just conceptual — the
"adoption" stage of that lifecycle is concretely represented by ASPIRE's
Feedback Loop, which routes post-implementation customer feedback through
a human Governance Review before anything syncs back to DeliveryOps.

## The User & The Job

**Primary user:** a Professional Services engineer or CS Technical Account
Manager, the moment a deal closes. Today they open a "Design of Record" (the
pre-sales solution architect's notes — use case, product SKUs sold, customer
environment, success criteria) and manually rebuild a High-Level Design and
project plan from it, in a separate tool, from scratch. That rebuild is where
context gets lost and delivery slows down.

**Job to be done:** turn a pre-sales artifact into a scoped, assigned,
trackable execution plan in minutes, not days — without re-interviewing the
account team.

## The Core Flow (what the prototype must prove)

```
Design of Record (pre-sales input)
        │
        ▼
AI reads it → auto-generates a Technical Requirements Document (TRD)
        │        or Execution Plan (scoped tasks, milestones, required skills)
        ▼
Engineer reviews/edits → assigns via Resource Assignment (same screen)
        │
        ▼
Execution Plan becomes the tracked record of delivery
```

The thing being tested is not "can you build a nice UI" — it's **"Technical
Agency"**: can you show, in working logic, that specific fields in a Design of
Record (e.g., product SKU, use case, customer environment) deterministically
map to specific sections/tasks in the generated TRD. That mapping *is* the
prototype's core IP.

## Why It Matters (the business problem)

- Fragmented tools (DeliveryOps + CustomerPulse + DealCRM) → no single source of
  truth across the post-sales lifecycle.
- Manual planning → delayed activation; deals sit before delivery starts.
- Context loss at the pre-sales → deployment handoff → engineers waste time
  recreating HLDs the account team already effectively wrote.
- Resourcing today is "First Available" (whoever's free), not "Best Fit"
  (whoever knows this customer's use case) — driving rework and slower
  time-to-value.

## Design Philosophy — "Living Specs, Not Static Docs"

The core idea behind ASPIRE's output: an AI-generated spec should stay
**executable and live**, not go stale the moment it's written like a static
PDF or Word doc. The auto-generated TRD/Execution Plan *is* the living
spec — it updates as inputs change, rather than needing to be manually
rewritten every time something upstream shifts.

## Scope Note

ASPIRE **builds** most of what could have stayed "strategy only":
Configuration, Reference Sets, the Resource Assignment flow, and the
CustomerPulse Feedback Loop are all real, working screens, not just
described. `03-architecture-strategy.md` is still the deeper "why" behind
each of them; it's no longer the only place they exist. The one thing
that hasn't changed: the core mapping logic
(`02-prototype-build-spec.md`'s Mapping Rules) is still the single most
important piece of this system — everything else is in service of
proving that, not a substitute for it.
