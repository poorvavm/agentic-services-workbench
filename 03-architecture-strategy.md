# Agent-Native Architecture (Strategy) — Written Answer

*This document explains the mechanism; ASPIRE (the prototype) now makes
most of it visible on screen rather than leaving it purely written. The
Configuration screen exposes the sync-direction and LLM settings described
below as actual UI controls; the Reference Sets screen is a working
version of the RAG retrieval index described in "The AI Loop"; the
Resource Assignment section embedded in the Execution Plan screen
demonstrates the scoring logic below with a real Assign/Reassign flow.
This doc is still the deeper "why," not duplicated by the build spec.*

## Reference Stack (name this if asked "what would you actually build this on")

Naming concrete technology choices, not just concepts, signals this was
thought through as a real system:

- **Frontend:** React/TypeScript — same stack as the prototype, so the
  Proof of Value and the production version share a component layer.
- **Backend:** a thin API proxy service — DealCRM/DeliveryOps credentials
  and any LLM API keys live server-side only, never in the browser client.
- **AI infrastructure:** a hosted LLM API (e.g., Claude or Gemini) for two
  distinct jobs, neither of which is generating the TRD tasks themselves —
  that mapping logic stays rules-based, deliberately, for traceability (see
  Retrospective in `05-presentation-outline.md`). The two AI jobs are: (1) a
  stronger model for the *structured-extraction* step proposed in the
  Retrospective — parsing messy real-world Design of Record notes into the
  clean fields the rules engine already trusts — where accuracy matters more
  than speed; and (2) a faster/cheaper model for the Configuration Copilot's
  live chat, where a user is waiting and expects a quick reply.
- **Data grounding:** the RAG retrieval layer sits in front of *both* models
  — this is what prevents hallucinated product configs, not model choice
  alone.

## Integration: Bidirectional Sync Without Data Loops

The failure mode to design against: System A pushes an update to System B,
B's webhook pushes back to A, A reacts again — an infinite (or at minimum
duplicating, conflicting) write loop.

**Approach — single ownership per field, one-directional writes:**

- **DealCRM owns** account and deal-stage fields (the commercial record).
- **DeliveryOps owns** project/task and delivery-status fields (the execution
  record).
- **CustomerPulse owns** post-implementation customer health and feedback data
  — a fourth system, not just the two originally scoped.
- **ASPIRE owns** the generated TRD/Execution Plan and the resourcing
  decision — data that doesn't exist anywhere else yet.

Writes only ever flow *from* the owning system *outward*. ASPIRE reads
from DealCRM and DeliveryOps to build context, but only ever writes back to
the field it itself owns, plus a status flag ("Execution Plan generated") —
never a field DealCRM or DeliveryOps already owns.

Every sync event carries an origin tag (which system produced it). If a
system receives an event tagged with its own origin, it drops it instead of
reprocessing — this is what actually kills the loop, not just "good field
ownership" in principle.

**Now visible in the prototype:** the Configuration screen's "Direction"
control (Inbound / Outbound / Bidirectional / Paused) per system is the
literal UI surface for this policy — it's what an admin would actually set
to enforce the ownership model above, not just a decorative dropdown.

## The AI Loop: RAG for the Configuration Copilot

The risk with an LLM answering configuration questions from trained memory
alone: it can confidently describe a product config that's outdated the
moment our docs change, or worse, describe a config for the wrong product
version.

**Approach:**

- Ingest product documentation (config guides, API references, release
  notes) into a retrieval index, chunked and versioned by product release.
- Every time the Copilot answers, it first retrieves the doc chunks matching
  *this specific customer's* deployed version (from the Design of Record's
  environment data) — not "latest" by default — then grounds its answer in
  those chunks.
- Re-index on every doc release, not on a schedule, so the index is never
  more stale than the docs themselves.
- Every answer surfaces its source doc/section inline, so the engineer can
  verify before acting on it rather than trusting it as ground truth. This is
  the same "human never blindsided by what the automation is doing" principle
  I've built before (PatientPoint's observability layer around AI/ML
  compliance automation) — applied here as source citations instead of
  execution traces.

**Now visible in the prototype:** the Reference Sets screen is a working
version of this retrieval index — one entry per product version, each with
its attached docs. The Review screen's "Reference Set: [Product] v[X] —
auto-selected" tag is the version-matching behavior described above, shown
live instead of only described.

## Resource Logic: Best Fit vs. First Available

Today's default is "First Available" — whoever's free gets assigned,
regardless of whether they've ever touched this product/use-case combination.

**Approach — a weighted recommendation, not an auto-assign black box:**

Score each candidate engineer on two axes: **availability** (calendar) and
**familiarity** (has this engineer delivered this specific SKU + use-case
combination before — pulled from their project history, same rules-based
tagging the prototype uses to generate the Execution Plan in the first
place).

- For high-complexity or high-risk engagements (e.g., security incident
  response use cases), weight familiarity heavier — a 2-day wait for the
  right engineer beats a same-day assignment that risks rework.
- For simple, well-documented use cases, default to availability — the
  familiarity gap matters less when the task itself is low-risk.
- The engine always shows *both* the Best Fit and First Available options
  side by side with its rationale — a delivery manager makes the final call.
  This keeps a human in the loop on every resourcing decision rather than
  auto-assigning silently, the same principle the Configuration Copilot
  applies to technical answers.

**Now visible in the prototype:** the Resource Assignment section, embedded
directly in the Execution Plan screen rather than a separate page,
demonstrates this live — Assign writes back to the same DeliveryOps project as
the plan, and Reassign updates that same record rather than creating a
disconnected one, so the loop this section describes is
something you can click through, not just something you say.

## The Feedback Loop: CustomerPulse Without Breaking the Ownership Model

Adding CustomerPulse as a fourth system creates the same risk the Integration
section above already solved for two systems — a naive bidirectional sync
between CustomerPulse and DeliveryOps could create exactly the write-loop problem
named earlier. The fix is the same principle, applied a third time:

**Approach — CustomerPulse feedback never writes to DeliveryOps directly.** It
routes through a **Governance Review** step first: a human sees the full
feedback payload and makes an explicit Accept-or-Reject call. Only "Accept"
triggers a write to DeliveryOps (a playbook/doc update), and that write
carries the same origin-tagging as every other sync event in this
architecture — so even an accepted piece of feedback can't loop back and
re-trigger itself as a "new" event.

This is the third instance of the same underlying pattern in this
document: the Configuration Copilot cites its source rather than asserting
ground truth; the Resource engine recommends rather than auto-assigns; and
now CustomerPulse feedback proposes rather than auto-syncs. One principle,
applied consistently across every AI-touched decision point in ASPIRE, not
three unrelated features that happen to look similar.

**Now visible in the prototype:** the Feedback Loop screen's Governance
Popup and its "Accept & Sync DeliveryOps" / "Reject Feedback" buttons are
exactly this — a human decision gate, shown live, not just described.
