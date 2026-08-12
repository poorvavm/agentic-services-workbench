# Problem Statement

## Context

Meridian Security's post-sales motion — everything that happens after a
deal closes — runs across three disconnected systems: **DealCRM** (the
CRM, owns the account and deal record), **DeliveryOps** (a PSA tool for
services delivery, task tracking, and resourcing), and **CustomerPulse**
(the customer-success platform tracking adoption, health, and renewal
risk). None of them talk to each other.

## The Problem

**Context gets lost at every handoff.** When a deal closes, the pre-sales
team's notes — the customer's use case, which product SKUs they bought,
their environment, what "success" looks like to them — live in a single
document: the **Design of Record**. Today, a Professional Services
engineer or CS Technical Account Manager reads that document once, then
manually rebuilds a High-Level Design and project plan from it, from
scratch, in a separate tool. That rebuild is where the context degrades
and delivery slows down.

**Planning is manual, so activation is delayed.** There's no system that
turns a pre-sales artifact into a scoped, assigned, trackable execution
plan on its own — someone has to do that translation by hand, every time,
which means deals sit before delivery actually starts.

**Resourcing defaults to "First Available," not "Best Fit."** Whoever's
free gets assigned to a delivery engagement today, regardless of whether
they've ever touched this product-and-use-case combination before. That
drives rework and slower time-to-value, especially on complex or
high-risk engagements where familiarity with the customer's specific
setup actually matters.

**None of this is visible until it's already a problem.** Internal
delivery friction — clarification round-trips between pre-sales and
delivery, engineer hours spent rediscovering context that already existed
somewhere — is invisible today. It only shows up downstream, as a slow
deployment or a frustrated customer.

## Why It Matters

Every one of these gaps compounds into the same outcome: **the time
between "deal closed" and "customer actually realizing the value they
bought" is longer than it needs to be**, and the business has no clean
way to measure or shrink that gap because the data needed to do so is
scattered across three tools that don't share a model of the customer.

## The Opportunity

A single system of engagement — spanning deal close → deployment →
adoption → renewal — that:

- Reads a Design of Record and **auto-generates** a Technical
  Requirements Document and Execution Plan, instead of a person rebuilding
  one by hand.
- Recommends the **best-fit** delivery engineer for the job, not just the
  first available one, while keeping a human making the final call.
- Grounds any AI-assisted configuration guidance in **current, versioned
  product documentation**, so it's never confidently wrong about a config
  that changed last release.
- Stays a **living spec** — an execution plan that updates as inputs
  change, rather than a static document that goes stale the moment it's
  written.
- Makes the friction it eliminates **measurable**: time to deploy, time
  to value, and delivery friction, tracked automatically rather than
  self-reported.

This is the problem the rest of this case study — concept, prototype,
architecture, and ROI framework — is solving for.
