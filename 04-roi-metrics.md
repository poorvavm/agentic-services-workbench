# Success & ROI Metrics — Written Answer

*Framed as business KPIs a GTM/exec audience cares about, not loss functions.*

## First Available → Best Fit: Is the Shift Actually Happening?

**Metric:** % of assignments where the delivery manager accepts the "Best
Fit" recommendation vs. overrides back to "First Available."

Track this against a secondary metric — **rework hours per project** (time
spent redoing or correcting delivery work after initial assignment). If
Best-Fit acceptance rises and rework hours fall together, the shift is real
and paying off, not just a UI nudge nobody follows.

## Time to Deploy

**Definition:** elapsed time from *deal closed* (DealCRM stage change) to
*solution live in the customer's environment* (DeliveryOps task marked
complete for final deployment step).

**Instrumentation:** ASPIRE logs a timestamp the moment a Design of
Record is received, and DeliveryOps already logs deployment completion — Time
to Deploy is just the delta between those two, computed automatically per
project rather than self-reported.

## Time to Value

**Definition:** elapsed time from *deployment complete* to the customer
*actually realizing the outcome they bought* — e.g., first successful use of
the deployed capability, or crossing an adoption/usage threshold (already
tracked in CustomerPulse for CS health scoring).

This is deliberately a further downstream metric than Time to Deploy — a
project can be "deployed" and still not be delivering value if adoption
lags, and that gap is exactly what CS teams currently can't see early enough.

## Internal Delivery Friction

**Definition:** proxy metrics for how much back-and-forth a handoff still
requires, tracked per project:

- Number of clarification round-trips between pre-sales and delivery teams
  (e.g., Slack threads or emails asking "what did the customer actually mean
  by X") — today invisible, could be tagged/logged through ASPIRE's
  intake flow.
- Engineer hours spent on rediscovery (re-reading notes, recreating an HLD
  that already existed) vs. hours spent on net-new delivery work — estimated
  via a simple time-tracking tag at project kickoff, compared before/after
  ASPIRE rolls out to a team.

**Why this framing, not accuracy/precision:** the panel explicitly asked to
move beyond loss functions to business KPIs. Every metric above answers "did
delivery get faster and cleaner for the business," not "how good is the
model" — the model quality only matters insofar as it moves these numbers.

## How This Maps to the Dashboard You'll See Live

The prototype's actual Dashboard surfaces a slightly different-looking set
of numbers — Conversion Speedup (3.2x), Reference Set Utilization,
Completed & Synced Plans, Active In-Progress Plans. These aren't a
replacement for the four metrics above; they're the **operational,
daily-use view** a delivery team would actually watch, derived from the
same underlying data:

- **Conversion Speedup (3.2x)** is Time to Deploy expressed as a ratio
  against the pre-ASPIRE manual baseline, not a new metric — easier for a
  delivery lead to act on at a glance than a raw day count.
- **Reference Set Utilization** is a leading indicator for the
  Configuration Copilot's grounding quality (`03-architecture-strategy.md`
  — "The AI Loop"): if engineers aren't actually using the auto-selected
  reference docs, that's an early signal the RAG grounding isn't earning
  trust, well before it shows up as rework or a friction complaint.
- **Completed & Synced Plans / Active In-Progress Plans** are the simplest
  possible leading counters for the same Time to Deploy pipeline — how
  many deals are in flight vs. done, before you even look at duration.

If asked "why does your dashboard show different metrics than your ROI
framework," the honest answer is that one is the **defensible measurement
strategy** (this doc, answering exactly what the assignment asked for),
and the other is the **at-a-glance operational view** built on top of it —
not two competing definitions of success.
