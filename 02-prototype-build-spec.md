# Prototype Build Spec — Paste Into Lovable / v0.dev / Replit / AI Studio

## How to Use This

This is **ASPIRE** — Automated Services & Post-sales Intelligent Resolution
Engine, built for Meridian Security Professional Services & Pre-Sales
Engineering Delivery. Stack: **React 18, Vite, TypeScript, Tailwind CSS**
(Recharts for the Dashboard's charts). It covers the full product surface —
the plan is to carry the technical narrative in the **live demo**, with the
slide deck reduced to framing and transitions.

**Navigation (left sidebar, dark #201C1D theme, top to bottom):**
1. Dashboard — *Services Analytics & Delivery Metrics*
2. Pre-Sales Deals — *Guided Conversion Flow* (formerly "Deal Queue")
3. Design of Record — *Approved Pre-Sales Technical Baselines*
4. Execution Plan — *Post-Sales Task Dispatch to DeliveryOps*
5. Resources — *Resource Allocation & Capacity Matrix*
6. Reference Sets — *Architecture Guidelines & Standards*
7. Feedback Loop — *Post-Implementation CustomerPulse Feedback & Governance*
   **(new)**
8. Notification *(TBD)* — *In-App Threshold & Milestone Alerts* **(new,
   lighter spec — placeholder-level for now)**
9. Audit Log *(TBD)* — *Latest-First Immutable System Audit Stream*
   **(reinstated — an earlier round of this spec cut Audit Log entirely;
   it's back now, marked TBD, spec'd lighter than the core screens)**
10. Configuration — *DealCRM, DeliveryOps, CustomerPulse & LLM Token Settings*

**Top header rule:** a filter header (Product View: Sentinel XDR / Sentinel SOAR / Aegis SASE; Time Range: Weekly / Monthly / Yearly) appears **only
on the Dashboard**. Every other screen has **no header banner** — clean
negative space, not an empty bar repeated on every page.

**Important — Pre-Sales Deals is a single guided flow, not page-hopping.**
Clicking "Process Deal" does **not** navigate to separate "Design of
Record" and "Execution Plan" pages as independent destinations. It opens
one continuous flow: confirm the Design of Record → generate the
Execution Plan → assign a resource, all connected. Once that flow
completes, the deal becomes a new entry in the **Design of Record** and
**Execution Plan** sidebar items — which are **archive/list views** of
every deal that's completed the flow, not live editing destinations
themselves.

---

## Screens

1. **Dashboard** — top header with Product View + Time Range filters
   (Weekly default). KPI row: Active In-Progress Execution Plans,
   Completed & Synced Plans, Time to Deploy, **Conversion Speedup (3.2x)**,
   Reference Set Utilization (%). Two Recharts charts below: **Deployment
   Speedup by Product** and **Monthly Pre-Sales Conversions** (seed data
   below).
2. **Pre-Sales Deals** — list of 5 pending DealCRM opportunities (seed
   data below), standardized sync indicator (DealCRM only), a "Process
   Deal" button per row launches the Guided Flow. Status badge per row
   ("New Handover" / "Processing" / "Completed"), Pre-Sales Context quote
   preview inline, "Load More" at the bottom.
3. **Design of Record** (archive) — list of every "approved" baseline:
   deals that have completed the flow (5 pre-loaded + Northwind Bank once
   processed live), storing architecture baseline, BOM (bill of materials —
   the SKUs/products sold), and technical scope notes per deal.
   Standardized sync indicator (DealCRM only). Modal drawer to inspect
   read-only fields + Pre-Sales Context + assigned Reference Set.
4. **Execution Plan** (archive) — list of every generated plan, each row
   showing a progress bar, task completion counter, status toggle summary
   (In Progress vs. Completed), and a real-time DeliveryOps sync indicator
   badge. Standardized sync indicator (DeliveryOps only). Clicking a row
   opens a modal drawer with the full task breakdown **plus the embedded
   Resource Assignment section** (dropdown, expand, Assign/Reassign/Back —
   this is where resourcing actually happens, not a separate page).
5. **Resources** — read-only table (Name, Availability, capacity
   utilization visual bar with overbooking alert, Recent Product
   Experience, Last Engagement). No selection/assignment here — that only
   happens inside a specific Execution Plan. Standardized sync indicator
   (DeliveryOps).
6. **Reference Sets** — grouped by product, each an expandable group
   (Product + Version) with multiple named documents underneath.
7. **Feedback Loop** (CustomerPulse-integrated, new) — table of
   post-implementation customer feedback: Product SKU, Customer, Assigned
   Rep, feedback snippet, status (Pending Review / Accepted / Rejected).
   "Review & Decide" opens a **Governance Popup** with the full feedback
   payload in a formatted text box, plus two decision buttons: **"Accept &
   Sync DeliveryOps"** (triggers a simulated playbook/doc update) and
   **"Reject Feedback."** A summary card at the bottom of the screen
   diagrams the pipeline: **CustomerPulse API → Governance Review → DeliveryOps
   Sync.**
8. **Notification** *(TBD, lighter spec)* — a real-time hub for system
   events: LLM token threshold alerts (e.g., "Token usage at 85% of
   limit"), DeliveryOps sync triggers, pre-sales milestone updates. Filterable
   by category, read/unread toggle, clicking a notification deep-links to
   the relevant screen. Not a demo priority — build if time allows.
9. **Audit Log** *(TBD, lighter spec)* — immutable, **latest-first** event
   stream (reuses the same event-log concept as before — see seed data
   below), with search and a module filter (Guided Flow / DeliveryOps Sync /
   Feedback Loop / Token Engine / Configuration). Not a demo priority —
   build if time allows.
10. **Configuration** — DealCRM section, DeliveryOps section, **CustomerPulse
    section (new)** — Webhook URL, Secret/Passkey, Sync Enabled toggle,
    Direction — and LLM Picker (Gemini / Claude / GPT-4, token usage +
    limit).

### The Guided Flow (triggered from Pre-Sales Deals, not its own nav item)

**Step A — Design of Record Review:** pre-filled, editable structured
fields (Customer Name, Deal Tier, SKUs as multi-select toggle buttons, Use
Case, Environment: On-prem / Hybrid/Multi-cloud / Cloud-native). Read-only
"Pre-Sales Context" block. Optional "Additional Context" textarea (delivery
constraints). "Reference Set: [Product] v[X] — auto-selected" tag. A
"Generate Execution Plan" button moves to Step B within the same flow.

**Step B — Execution Plan + Resource Assignment:** the **AI
requirement-to-task parser** generates the task list (Because tags with
quoted context, Not Yet Covered box, tasks editable/addable/removable).
Each task shows an **estimated effort with a Planning View multiplier** —
a "Weekly / Monthly" toggle scales displayed task estimates by **1.0x
(Weekly baseline) / 1.25x (Monthly)**, mirroring the Dashboard's own
scaling convention but applied to task-level estimates, not just
dashboard aggregates. Push to DeliveryOps / Simulate Update / progress /
completion (Full Loop Simulation below), plus the Resource Assignment
section on the same screen. Reaching 100% surfaces a **"Complete
Processing & Save to Archives"** button — clicking it (not automatic
completion) is what adds the deal to the Design of Record and Execution
Plan archives, and updates the Dashboard's KPIs.

---

## Standardized Sync Indicator (use this exact component everywhere)

```
[Source]  ·  Last synced: [time]  ·  [Sync Now button]
```

- **Pre-Sales Deals** and **Design of Record** → Source = **DealCRM
  only**.
- **Execution Plan** and **Resources** → Source = **DeliveryOps only**.
- **Feedback Loop** → Source = **CustomerPulse only**.
- "Sync Now" resets "Last synced" to "just now" (simulated, no real API
  call). Same component, same three parts, everywhere it appears.

---

## Seed Data

### The unified deal dataset (Dashboard KPIs, Design of Record archive,
### Execution Plan archive — one dataset, three views)

**Already-completed deals** (pre-loaded so nothing is empty before you
demo anything):

| Deal | Product | Time to Deploy |
|---|---|---|
| Vantage Insurance Group | Sentinel XDR | 12 days |
| Coastal Retail Group | Aegis SASE | 9 days |
| Union Financial | Sentinel SOAR | 7 days |
| Briarwood Systems | Sentinel XDR | 8 days |
| Delta Manufacturing | Aegis SASE | 5 days |

**Northwind Bank** (the live demo path — pending in Pre-Sales Deals,
becomes the 6th completed entry once you finish the guided flow live):
Sentinel XDR, 3 days deploy — the fastest of all six, backing the
"Conversion Speedup 3.2x" KPI and demonstrating it growing in real time,
not as a pre-loaded number.

**Dashboard KPI values (default, before processing Northwind):**
- Active In-Progress Execution Plans: 1 (Northwind, once you start it)
- Completed & Synced Plans: 5
- Time to Deploy (average): 8.2 days
- Conversion Speedup: 3.2x (baseline manual process vs. ASPIRE)
- Reference Set Utilization: 78%

**Chart data:**
- *Deployment Speedup by Product* — Sentinel XDR: 3.5x, Sentinel SOAR: 2.8x,
  Aegis SASE: 3.0x.
- *Monthly Pre-Sales Conversions* — a 6-month trend, e.g. Jan 4, Feb 6,
  Mar 5, Apr 7, May 8, Jun 9 (rising) — deals converted from Pre-Sales to
  a completed Execution Plan per month.

### Pre-Sales Deals rows (pending)

**Row 1 — Northwind Bank** (the live demo path)
- Deal Tier: Enterprise · SKUs: Sentinel XDR, Sentinel SOAR
- Use Case: Ransomware Response · Environment: Hybrid/Multi-cloud

**Row 2 — Alpine Retail Co.**
- Deal Tier: Mid-Market · SKUs: Aegis SASE
- Use Case: Branch Office Connectivity · Environment: Cloud-native

**Row 3 — Meridian Health Systems** *(queue bulk only)*
- Deal Tier: Enterprise · SKUs: Sentinel XDR, Aegis SASE
- Use Case: Ransomware Response · Environment: Hybrid/Multi-cloud

**Row 4 — Fenwick Logistics** *(queue bulk only)*
- Deal Tier: Mid-Market · SKUs: Sentinel SOAR
- Use Case: Branch Office Connectivity · Environment: Cloud-native

**Row 5 — Cascade Manufacturing** *(queue bulk only)*
- Deal Tier: SMB · SKUs: Aegis SASE
- Use Case: Ransomware Response · Environment: On-prem

Only Northwind Bank needs full Pre-Sales Context / Not Yet Covered — Rows
2–5 just need pre-filled fields if clicked.

### Pre-Sales Context (Northwind Bank, raw text)

> "Northwind Bank is consolidating three regional SOC teams following a
> ransomware incident at a peer institution. They need endpoint detection
> with automated containment, plus a way to accelerate their currently
> manual SOC playbooks. Running hybrid — some workloads still on-prem, core
> banking moving to AWS over the next two quarters. Their CISO specifically
> asked about audit trail requirements for their next regulatory exam, and
> mentioned SOC analysts are drowning in alert volume."

### "Not Yet Covered" box (Northwind Bank)

- "CISO's audit trail requirement for the regulatory exam" — no matching
  rule; a genuinely unaddressed gap, named honestly rather than hidden.
  *(Now that Audit Log exists as a TBD screen, this can stay an honest gap
  regardless — don't retrofit a payoff that isn't built yet.)*
- "SOC analyst alert-fatigue concern" — no current rule maps this to a
  task.

### Reference Sets (grouped)

**Sentinel XDR — v3.2:** Admin Guide, API Reference, Release Notes
**Sentinel SOAR — v2.1:** Admin Guide, Playbook Reference
**Aegis SASE — v4.0:** Admin Guide, API Reference, Release Notes,
Migration Guide

### Resources (roster — powers both the read-only table and the Execution
### Plan's assignment dropdown)

| Name | Availability | Capacity | Recent Product Experience | Last Engagement |
|---|---|---|---|---|
| Maya Chen | Available in 2 days | 70% | Sentinel XDR, Sentinel SOAR — Ransomware Response | 2 months ago |
| Priya Nair | Available in 3 days | 65% | Sentinel XDR, Aegis SASE | 8 months ago |
| Alex Vance | Available in 1 day | 55% | Sentinel XDR (general) | 5 months ago |
| Devon Marsh | Available in 4 days | 90% (overbooked) | Sentinel XDR, Aegis SASE, Sentinel SOAR | 1 month ago |
| Jordan Wu | Available today | 40% | None relevant | — |
| Sam Okafor | Available today | 10% | None | — |

**Execution Plan's assignment dropdown (Northwind context, deal-specific
fit, Maya Chen pre-selected):**

| Name | Fit Category | Supporting Facts |
|---|---|---|
| Maya Chen | Best Fit | Delivered 3 prior Sentinel XDR + Ransomware Response engagements; last closed 2 months ago; CSAT 9/10 |
| Priya Nair | Strong Fit | Delivered this exact SKU + use-case combo once, 8 months ago |
| Alex Vance | Partial Match | Delivered Sentinel XDR before, but not Ransomware Response specifically |
| Devon Marsh | Partial Match (overbooked) | Delivered 5 prior similar engagements, currently overbooked |
| Jordan Wu | First Available | No prior exposure to this SKU/use case; 40% capacity |
| Sam Okafor | Fully Available | No relevant experience; fully available |

### Feedback Loop (CustomerPulse, new — seed entries)

| Product SKU | Customer | Assigned Rep | Feedback Snippet | Status |
|---|---|---|---|---|
| Sentinel XDR | Vantage Insurance Group | Maya Chen | "Endpoint isolation policy triggered a false positive during a scheduled backup window — needs a maintenance-mode exception." | Pending Review |
| Aegis SASE | Coastal Retail Group | Priya Nair | "SD-WAN failover worked as expected during a regional outage — customer specifically called this out as a win." | Pending Review |
| Sentinel SOAR | Union Financial | Alex Vance | "Requesting an additional playbook for a use case not in the original scope." | Accepted |

**Governance Popup:** shows the full feedback text, Product/Customer/Rep
metadata, and two buttons — "Accept & Sync DeliveryOps" (simulated: shows a
toast "Synced to DeliveryOps — playbook update queued") and "Reject
Feedback" (simulated: status flips to "Rejected," nothing synced).

### Audit Log (TBD — seed entries, reusing the Northwind timeline)

```
Day 3, 10:01 AM — Deal marked 100% complete — Time to Deploy: 3 days
Day 3, 10:00 AM — Remaining 6 tasks marked complete (synced from DeliveryOps)
Day 2, 4:20 PM  — Task "Configure behavioral analytics profile" marked
                   complete (synced from DeliveryOps)
Day 2, 11:40 AM — Task "Deploy Sentinel agents across endpoint fleet" marked
                   complete (synced from DeliveryOps)
Day 1, 2:15 PM  — Maya Chen assigned (synced to DeliveryOps)
Day 1, 9:05 AM  — Plan pushed to DeliveryOps (Project #CZ-4821)
Day 1, 9:03 AM  — Execution Plan generated (10 tasks)
Day 1, 9:02 AM  — Design of Record pulled from DealCRM
```
(Latest-first — top entry is the most recent.)

---

## Mapping Rules (the actual "Technical Agency" logic)

| If Input Field = | Generate This Task | Context Snippet Cited |
|---|---|---|
| SKU includes "Sentinel XDR" | "Deploy Sentinel agents across endpoint fleet"; "Configure behavioral analytics profile" | "they need endpoint detection with automated containment" |
| SKU includes "Sentinel SOAR" | "Integrate Sentinel alerts with Sentinel SOAR for automated response playbooks" | "accelerate their currently manual SOC playbooks" |
| Use Case = "Ransomware Response" | "Configure endpoint isolation policy"; "Define incident-response runbook thresholds" | "following a ransomware incident at a peer institution" |
| SKU includes "Aegis SASE" | "Provision Aegis Access connectors"; "Configure Zero Trust Network Access policies" | "secure, consistent connectivity across all sites" |
| Use Case = "Branch Office Connectivity" | "Onboard branch sites to SASE fabric"; "Validate SD-WAN failover per site" | "opening 12 new store locations... no SD-WAN" |
| Environment includes "hybrid" or "multi-cloud" | "Validate cross-environment IAM roles for telemetry ingestion" (prerequisite, top of list) | "core banking moving to AWS over the next two quarters" |
| Deal Tier = "Enterprise" | "Assign dedicated TAM"; "Schedule executive business review cadence" | (deal-tier driven) |

Anything in the Pre-Sales Context that doesn't match a rule goes into the
"Not Yet Covered" box.

---

## Full Loop Simulation (Execution Plan step — Push, Simulate, Progress, Complete)

0. **Task list editing:** edit a task's title inline, add a custom task
   ("+ Add Task"), or remove a task (delete icon per row).
1. **"Push to DeliveryOps"** → toast "Pushed to DeliveryOps — Project #CZ-4821
   created." Every task gets a status pill (default "Not Started"). A
   persistent "✓ Synced to DeliveryOps — [timestamp]" badge appears.
2. **"Simulate DeliveryOps Update"** (demo-only) → each click flips 1–3 tasks
   to "✓ Completed" with "Completed [date/time] — synced from DeliveryOps."
   Progress line updates live: "3/8 tasks complete" → "6/8" → etc.
3. **At 100%**, the progress line reads "100% complete — took 3 days" plus
   a completion timestamp, and a **"Complete Processing & Save to
   Archives"** button appears. Clicking it (not automatic) adds the deal
   to the Design of Record and Execution Plan archives and updates the
   Dashboard's KPIs (Completed & Synced Plans, Conversion Speedup, Time to
   Deploy average).

**Why simulated, not real:** no actual DeliveryOps instance exists —
simulating the state transitions proves the loop is understood without
pretending a real integration exists.

---

## Assign/Override Flow (embedded in the Execution Plan screen)

1. Dropdown lists all 6 engineers, sorted Best Fit first for this deal,
   Maya Chen pre-selected.
2. Selecting an entry expands a panel with 2–3 supporting facts plus
   "Assign [Name]" and "Back."
3. **Assign** → confirmation banner: "✓ [Name] assigned — synced to
   DeliveryOps Project #CZ-4821" (same project number as Push-to-DeliveryOps). A
   "Reassign" option appears.
4. **Reassign** → re-opens the dropdown; picking someone new updates the
   *same* DeliveryOps project record.
5. **Back** (before assigning) → collapses the panel, nothing assigned.

---

## Dashboard (detail)

**Top header (Dashboard only):** Product View filter (Sentinel XDR / Sentinel SOAR / Aegis SASE) and Time Range filter (Weekly / Monthly / Yearly,
Weekly default).

**KPI row:** Active In-Progress Execution Plans, Completed & Synced Plans,
Time to Deploy (average), **Conversion Speedup (3.2x)**, Reference Set
Utilization (%) — values in Seed Data above.

**Two Recharts charts:** Deployment Speedup by Product (bar chart, 3
products), Monthly Pre-Sales Conversions (line/bar trend, 6 months) — seed
data above. Time Range filter scales displayed values using the same
convention used elsewhere: Weekly = 1.0x baseline, Monthly = 1.25x.

---

## Feedback Loop Page (detail)

Table of CustomerPulse-sourced feedback (seed data above). "Review & Decide"
per row opens the Governance Popup. Bottom-of-screen summary card
diagrams: **CustomerPulse API → Governance Review → DeliveryOps Sync.** Accepting
feedback is a simulated DeliveryOps sync (toast only); rejecting just updates
status locally.

---

## Reference Sets Page (detail)

Grouped view: each product is a collapsible group (name + version) with
its documents listed underneath. "Add Document" / "Add Link" scoped
per-group. "Create New Reference Set" opens a form that becomes a new
group.

---

## Resources Page (detail)

Flat, read-only table — Name, Availability, capacity utilization visual
bar (with overbooking alert badge), Recent Product Experience, Last
Engagement. No click-to-assign; assignment only happens inside a specific
Execution Plan.

---

## Configuration Page (detail)

**DealCRM section:** Instance URL, Passkey (masked), Sync Duration
(15 min / 30 min / 1 hr), Direction (Inbound / Outbound / Bidirectional /
Paused — default Bidirectional).

**DeliveryOps section:** same four fields as DealCRM.

**CustomerPulse section (new):** Webhook URL, Secret/Passkey (masked), Sync
Enabled (toggle), Direction (Inbound / Outbound / Bidirectional / Paused).

**LLM Picker section:** Provider (Gemini / Claude / GPT-4, Gemini first),
Access Key (masked), Token Usage (progress bar, "12,400 / 50,000 tokens
this month"), Token Limit (numeric, default 50,000).

"Save Configuration" → toast "Settings saved." No real persistence needed.

---

## Visual Style

- **Sidebar:** dark #201C1D background, #E8590C (Meridian Security's
  actual brand orange, "Outrageous Orange") for the active nav item
  accent. Fixed/locked, sticky full-height.
- **Canvas:** warm off-white/light gray — #EBEBEB and #FAF9F9 — panels/
  cards white (#FFFFFF) with crisp #D1D1D1 hairline borders, subtle
  shadows (shadow-xs).
- **Dark neutrals:** #201C1D and #332E2F for headers, sidebars, and
  high-contrast tables.
- **Accent:** #E8590C consistently for buttons, active states, badges,
  accent borders — never a generic blue or purple.
- **Typography:** clean sans-serif body; bold **uppercase Arial Narrow**
  for headers/section titles; **font-mono** for IDs, tokens, timestamps,
  and metrics.
- **Zero unrequested hero fluff** — no marketing-style landing treatment,
  this is an internal enterprise tool.

---

## Prompt to Paste

Try the full prompt first; split into two passes only if the builder
struggles — **Phase 1** = Dashboard, Pre-Sales Deals, and the Guided Flow
(Design of Record → Execution Plan + Resource Assignment). **Phase 2** =
Resources, Reference Sets, Feedback Loop, Configuration (and Notification
/ Audit Log if time allows — they're marked TBD for a reason).

```
Build a high-performance, single-page enterprise web application for
ASPIRE Platform (Meridian Security Professional Services & Pre-Sales
Engineering Delivery) using React 18, Vite, TypeScript, and Tailwind CSS.

VISUAL DESIGN:
- Canvas/Background: warm off-white/light gray (#EBEBEB and #FAF9F9).
- Primary Accent: Brand Orange (#E8590C).
- Dark Neutrals: Onyx Dark Charcoal (#201C1D and #332E2F) for headers,
  sidebars, and high-contrast tables.
- Typography: clean sans-serif body, bold uppercase 'Arial Narrow'
  headers, font-mono for IDs/tokens/metrics.
- Crisp 1px hairline borders (#D1D1D1), subtle shadows (shadow-xs), clean
  card padding, zero unrequested hero fluff.

NAVIGATION: left sidebar (dark #201C1D theme), in this exact order:
"Dashboard," "Pre-Sales Deals," "Design of Record," "Execution Plan,"
"Resources," "Reference Sets," "Feedback Loop," "Notification (TBD),"
"Audit Log (TBD)," "Configuration."

TOP HEADER RULE: a filter header (Product View: Sentinel XDR / Sentinel SOAR
/ Aegis SASE; Time Range: Weekly / Monthly / Yearly, Weekly default)
appears ONLY on the Dashboard page. Every other page has no header
banner — clean negative space, not an empty bar repeated everywhere.

FLOW NOTE: "Design of Record" and "Execution Plan" are ARCHIVE/LIST views
of deals that have completed processing — NOT where a new deal is
processed. Processing happens entirely from "Pre-Sales Deals": clicking
"Process Deal" launches one continuous Guided Flow (confirm Design of
Record → generate Execution Plan → assign a resource, no separate page
navigation). Completing the flow adds the deal to both archive lists and
updates the Dashboard's KPIs.

SYNC INDICATOR (identical reusable component everywhere): "[Source]  ·
Last synced: [time]  ·  [Sync Now button]." Pre-Sales Deals and Design of
Record show "DealCRM" only. Execution Plan and Resources show
"DeliveryOps" only. Feedback Loop shows "CustomerPulse" only. "Sync Now" resets
"Last synced" to "just now" (simulated, no real API call).

=== SCREEN 1: DASHBOARD ===
Top header with Product View and Time Range filters (Weekly default). KPI
row: Active In-Progress Execution Plans, Completed & Synced Plans, Time to
Deploy, Conversion Speedup (3.2x), Reference Set Utilization (%) — values
below. Two Recharts charts: "Deployment Speedup by Product" (bar chart)
and "Monthly Pre-Sales Conversions" (trend chart) — data below. Time Range
filter scales values: Weekly = 1.0x baseline, Monthly = 1.25x.

=== SCREEN 2: PRE-SALES DEALS ===
Table of 5 pending DealCRM opportunities (rows below), each showing a
status badge ("New Handover" / "Processing" / "Completed"), Customer Name,
Product SKUs, Deal Tier, Primary Use Case, Environment, a Pre-Sales
Context quote preview inline, and a "Process Deal" button. Standardized
sync indicator (DealCRM only) at top. "Load More" button at bottom
(visual only).

=== GUIDED FLOW (triggered by "Process Deal," not a nav destination) ===
STEP A — "Design of Record Review": every field pre-filled from the
clicked row: Customer Name (text), Deal Tier (dropdown: SMB / Mid-Market /
Enterprise), Product SKUs (multi-select toggle buttons: Sentinel XDR, Sentinel SOAR, Aegis SASE), Use Case (dropdown: Ransomware Response, Branch
Office Connectivity), Customer Environment (dropdown: On-prem, Hybrid/
Multi-cloud, Cloud-native) — all editable. Standardized sync indicator
(DealCRM only). Read-only "Pre-Sales Context" block (data below).
Optional "Additional Context" textarea. "Reference Set: [Product] v[X] —
auto-selected" tag. "Generate Execution Plan" button moves to Step B
within the same flow.

STEP B — "Execution Plan": AI-generated task list using the CONDITIONAL
TASK-GENERATION RULES below, each task showing "Because: [field] —
context: '[quoted snippet]'" and an estimated effort value. A "Planning
View" toggle (Weekly / Monthly) scales displayed task estimates by 1.0x
(Weekly) / 1.25x (Monthly). A "Not Yet Covered" box lists uncovered
context items (data below). Tasks are editable, addable ("+ Add Task"),
and removable (delete icon). "Push to DeliveryOps" button — toast "Pushed to
DeliveryOps — Project #CZ-4821 created," status pill per task (default "Not
Started"), persistent badge "✓ Synced to DeliveryOps — [timestamp]."
"Simulate DeliveryOps Update" button (demo-only) — each click flips 1-3 tasks
to "✓ Completed" with "Completed [date/time] — synced from DeliveryOps,"
updating a live progress line. At 100%, show "100% complete — took 3
days" plus a "Complete Processing & Save to Archives" button — clicking
it (not automatic) archives the deal and updates Dashboard KPIs.

BELOW THE TASK LIST, SAME SCREEN — "Resource Assignment": dropdown of 6
engineers labeled "[Name] — [Fit Category] — Available [X]" (data below),
sorted Best Fit first, pre-selected on load. Selecting expands a panel
with supporting facts plus "Assign [Name]" and "Back." Assign shows "✓
[Name] assigned — synced to DeliveryOps Project #CZ-4821" and a "Reassign"
button reopening the dropdown, updating the same project record.

=== SCREEN 3: DESIGN OF RECORD (archive) ===
List of every completed deal (5 pre-loaded + any processed live), showing
Customer Name, Product, Deal Tier, completion date. Standardized sync
indicator (DealCRM only). Clicking a row opens a modal drawer with
structured fields, Pre-Sales Context, and assigned Reference Set,
read-only.

=== SCREEN 4: EXECUTION PLAN (archive) ===
List of every generated plan, each row showing a progress bar, task
completion counter, and assigned-resource badge. Standardized sync
indicator (DeliveryOps only). Clicking a row opens a modal drawer with the
full task breakdown plus the resource assignment that was made.

=== SCREEN 5: RESOURCES ===
Read-only table — Name, Availability, capacity utilization visual bar with
overbooking alert badge, Recent Product Experience, Last Engagement (data
below). Standardized sync indicator (DeliveryOps only). No click-to-assign.

=== SCREEN 6: REFERENCE SETS ===
Grouped view: each product is a collapsible group (name + version) with
named documents underneath (data below). "Add Document"/"Add Link" scoped
per-group. "Create New Reference Set" opens a form for a new group.

=== SCREEN 7: FEEDBACK LOOP (CustomerPulse) ===
Table of customer feedback: Product SKU, Customer, Assigned Rep, feedback
snippet, status (Pending Review / Accepted / Rejected) — data below.
"Review & Decide" opens a Governance Popup with the full feedback text and
two buttons: "Accept & Sync DeliveryOps" (toast: "Synced to DeliveryOps —
playbook update queued") and "Reject Feedback" (status flips to
"Rejected"). A summary card at the bottom diagrams: CustomerPulse API →
Governance Review → DeliveryOps Sync. Standardized sync indicator (CustomerPulse
only).

=== SCREEN 8: NOTIFICATION (TBD — build if time allows) ===
Real-time hub: LLM token threshold alerts, DeliveryOps sync triggers,
pre-sales milestone updates. Filterable by category, read/unread toggle,
clicking deep-links to the relevant screen.

=== SCREEN 9: AUDIT LOG (TBD — build if time allows) ===
Immutable, latest-first event stream (data below), with search and a
module filter (Guided Flow / DeliveryOps Sync / Feedback Loop / Token Engine
/ Configuration).

=== SCREEN 10: CONFIGURATION ===
Sections: "DealCRM" (Instance URL, Passkey masked, Sync Duration 15min/
30min/1hr, Direction Inbound/Outbound/Bidirectional/Paused default
Bidirectional), "DeliveryOps" (same four fields), "CustomerPulse" (Webhook URL,
Secret/Passkey masked, Sync Enabled toggle, Direction), "LLM Picker"
(Provider dropdown Gemini/Claude/GPT-4 Gemini first, Access Key masked,
Token Usage progress bar "12,400 / 50,000 tokens this month", Token Limit
numeric default 50000). "Save Configuration" button shows toast "Settings
saved."

=== DASHBOARD DATA ===
KPIs: Active In-Progress Execution Plans = 1, Completed & Synced Plans =
5, Time to Deploy average = 8.2 days, Conversion Speedup = 3.2x, Reference
Set Utilization = 78%.
Deployment Speedup by Product: Sentinel XDR 3.5x, Sentinel SOAR 2.8x, Aegis SASE 3.0x.
Monthly Pre-Sales Conversions (6 months): Jan 4, Feb 6, Mar 5, Apr 7, May
8, Jun 9.

=== ALREADY-COMPLETED DEALS ===
Vantage Insurance Group: Sentinel XDR, Time to Deploy 12 days
Coastal Retail Group: Aegis SASE, Time to Deploy 9 days
Union Financial: Sentinel SOAR, Time to Deploy 7 days
Briarwood Systems: Sentinel XDR, Time to Deploy 8 days
Delta Manufacturing: Aegis SASE, Time to Deploy 5 days

=== PRE-SALES DEALS ROWS (pending) ===
Row 1: Northwind Bank, Enterprise, Closed Won, SKUs=[Sentinel XDR, Sentinel SOAR], Use Case=Ransomware Response, Environment=Hybrid/Multi-cloud
Row 2: Alpine Retail Co., Mid-Market, Closed Won, SKUs=[Aegis SASE], Use
Case=Branch Office Connectivity, Environment=Cloud-native
Row 3: Meridian Health Systems, Enterprise, Closed Won, SKUs=[Sentinel XDR,
Aegis SASE], Use Case=Ransomware Response, Environment=Hybrid/Multi-cloud
Row 4: Fenwick Logistics, Mid-Market, Closed Won, SKUs=[Sentinel SOAR], Use
Case=Branch Office Connectivity, Environment=Cloud-native
Row 5: Cascade Manufacturing, SMB, Closed Won, SKUs=[Aegis SASE], Use
Case=Ransomware Response, Environment=On-prem
(Only Row 1, Northwind Bank, needs Pre-Sales Context / Not Yet Covered.)

=== PRE-SALES CONTEXT (Northwind Bank) ===
"Northwind Bank is consolidating three regional SOC teams following a
ransomware incident at a peer institution. They need endpoint detection
with automated containment, plus a way to accelerate their currently
manual SOC playbooks. Running hybrid — some workloads still on-prem, core
banking moving to AWS over the next two quarters. Their CISO specifically
asked about audit trail requirements for their next regulatory exam, and
mentioned SOC analysts are drowning in alert volume."

=== NOT YET COVERED (Northwind Bank) ===
"CISO's audit trail requirement for the regulatory exam" (no matching
rule), "SOC analyst alert-fatigue concern" (no current rule maps this to
a task).

=== CONDITIONAL TASK-GENERATION RULES ===
- Sentinel XDR selected → "Deploy Sentinel agents across endpoint fleet" (context:
  "they need endpoint detection with automated containment") and "Configure
  behavioral analytics profile"
- Sentinel SOAR selected → "Integrate Sentinel alerts with Sentinel SOAR for automated
  response playbooks" (context: "accelerate their currently manual SOC
  playbooks")
- Use Case = Ransomware Response → "Configure endpoint isolation policy"
  (context: "following a ransomware incident at a peer institution") and
  "Define incident-response runbook thresholds"
- Aegis SASE selected → "Provision Aegis Access connectors" (context:
  "secure, consistent connectivity across all sites") and "Configure Zero
  Trust Network Access policies"
- Use Case = Branch Office Connectivity → "Onboard branch sites to SASE
  fabric" (context: "opening 12 new store locations... no SD-WAN") and
  "Validate SD-WAN failover per site"
- Environment = Hybrid/Multi-cloud or Cloud-native → add a prerequisite
  task at the TOP of the list: "Validate cross-environment IAM roles for
  telemetry ingestion" (context: "core banking moving to AWS over the next
  two quarters")
- Deal Tier = Enterprise → add "Assign dedicated TAM" and "Schedule
  executive business review cadence" at the end of the list

=== RESOURCES TABLE ===
Maya Chen: Available in 2 days, 70% capacity, Sentinel XDR/Sentinel SOAR/Ransomware
Response experience, last engagement 2 months ago
Priya Nair: Available in 3 days, 65% capacity, Sentinel XDR/Aegis SASE
experience, last engagement 8 months ago
Alex Vance: Available in 1 day, 55% capacity, Sentinel XDR (general)
experience, last engagement 5 months ago
Devon Marsh: Available in 4 days, 90% capacity (overbooked), Sentinel XDR/Aegis SASE/Sentinel SOAR experience, last engagement 1 month ago
Jordan Wu: Available today, 40% capacity, no relevant experience
Sam Okafor: Available today, 10% capacity, no relevant experience

=== RESOURCE DROPDOWN (Execution Plan screen, Northwind Bank context) ===
Maya Chen — Best Fit — Available in 2 days — "Delivered 3 prior Sentinel XDR
+ Ransomware Response engagements," "Last engagement closed 2 months ago,"
"Customer satisfaction 9/10"
Priya Nair — Strong Fit — Available in 3 days — "Delivered this exact SKU
+ use-case combo once, 8 months ago"
Alex Vance — Partial Match — Available in 1 day — "Delivered Sentinel XDR
before, but not Ransomware Response specifically"
Devon Marsh — Partial Match (overbooked) — Available in 4 days —
"Delivered 5 prior similar engagements, currently overbooked"
Jordan Wu — First Available — Available today — "No prior exposure to
this SKU/use case combination," "Currently at 40% capacity"
Sam Okafor — Fully Available — Available today — "No relevant experience,"
"Fully available"
Dropdown order matches this list; Maya Chen pre-selected.

=== REFERENCE SETS ===
Group "Sentinel XDR v3.2" contains documents: Admin Guide, API Reference,
Release Notes
Group "Sentinel SOAR v2.1" contains documents: Admin Guide, Playbook
Reference
Group "Aegis SASE v4.0" contains documents: Admin Guide, API Reference,
Release Notes, Migration Guide

=== FEEDBACK LOOP DATA ===
Sentinel XDR | Vantage Insurance Group | Maya Chen | "Endpoint isolation
policy triggered a false positive during a scheduled backup window —
needs a maintenance-mode exception." | Pending Review
Aegis SASE | Coastal Retail Group | Priya Nair | "SD-WAN failover worked
as expected during a regional outage — customer specifically called this
out as a win." | Pending Review
Sentinel SOAR | Union Financial | Alex Vance | "Requesting an additional
playbook for a use case not in the original scope." | Accepted

=== AUDIT LOG DATA (latest-first) ===
Day 3, 10:01 AM — Deal marked 100% complete — Time to Deploy: 3 days
Day 3, 10:00 AM — Remaining 6 tasks marked complete (synced from DeliveryOps)
Day 2, 4:20 PM — Task "Configure behavioral analytics profile" marked
complete (synced from DeliveryOps)
Day 2, 11:40 AM — Task "Deploy Sentinel agents across endpoint fleet" marked
complete (synced from DeliveryOps)
Day 1, 2:15 PM — Maya Chen assigned (synced to DeliveryOps)
Day 1, 9:05 AM — Plan pushed to DeliveryOps (Project #CZ-4821)
Day 1, 9:03 AM — Execution Plan generated (10 tasks)
Day 1, 9:02 AM — Design of Record pulled from DealCRM
```

---

## Demo Script (click-by-click)

**Step 1 — Dashboard (before processing anything)**
- *Click:* Show the KPI row and both charts.
- *Say:* "Five deals already synced and completed — watch these numbers
  move once I process a sixth live."

**Step 2 — Pre-Sales Deals**
- *Click:* Point at the DealCRM sync indicator, click "Sync Now."
  Point at Northwind's "New Handover" badge and its Pre-Sales Context
  quote preview. Click "Process Deal."
- *Say:* "One continuous flow starts here, not three separate pages."

**Step 3 — Design of Record Review (Step A)**
- *Click:* Point at pre-filled fields, Pre-Sales Context block, and the
  auto-selected Reference Set tag.
- *Say:* "Here's the actual pre-sales note this came from, and the system
  already knows which product docs apply." Click "Generate Execution
  Plan."

**Step 4 — Execution Plan (Step B, same flow)**
- *Click:* Point at a "Because" tag with its context quote, then "Not Yet
  Covered." Add one custom task, then delete it. Toggle Planning View
  Weekly → Monthly, watch estimates scale 1.25x.
- *Say:* "Every task cites its source, I can adjust the plan, and here's
  what wasn't covered — I didn't hide that gap." Click "Push to
  DeliveryOps," then "Simulate DeliveryOps Update" until 100%.
- *Say:* "Took 3 days — and this isn't archived yet, that's a deliberate
  next click."

**Step 5 — Resource Assignment (same screen)**
- *Click:* Open the dropdown, select Maya Chen, click "Assign." Click
  "Reassign," re-select Maya Chen, then click "Complete Processing & Save
  to Archives."
- *Say:* "Assigning writes to the same DeliveryOps project as the plan — and
  completing is explicit, not automatic."

**Step 6 — Design of Record & Execution Plan archives**
- *Click:* Navigate to both — Northwind Bank is now listed in each, with
  its progress bar and assigned-resource badge.
- *Say:* "These are the historical record of what I just did."

**Step 7 — Dashboard, revisited**
- *Click:* Return to Dashboard — KPIs and charts now reflect 6 deals.
- *Say:* "That moved because I processed a real deal, not because I
  clicked a demo button."

**Step 8 — Resources, Reference Sets**
- *Click:* Show the roster's capacity bars, then the Sentinel XDR reference
  group.
- *Say:* "Same roster DeliveryOps has — browsable, not assignable from here.
  And this is what auto-selected earlier."

**Step 9 — Feedback Loop**
- *Click:* Open "Review & Decide" on the Vantage Insurance feedback item,
  show the Governance Popup, click "Accept & Sync DeliveryOps."
- *Say:* "Post-implementation feedback from CustomerPulse routes through a
  human decision before anything reaches DeliveryOps — same principle as
  resourcing."

**Step 10 — Configuration**
- *Click:* Show DealCRM/DeliveryOps/CustomerPulse sync fields and the LLM
  Picker (Gemini, Claude, GPT-4).
- *Say:* "The knob-level control a real admin would need across every
  integration, including CustomerPulse now."

**Timing note:** this is the primary content of the Technical Deep Dive —
lean on this walkthrough over slide narration. Notification and Audit Log
are TBD/lower priority — skip them in the live demo unless there's time
left over.

---

## What to Say If Asked "Why Build the Full Surface?"

"I wanted to show I understand the whole operating surface a real admin
and delivery team would need, not just the demo-friendly slice. Everything
here is either real conditional logic (the task mapping) or an
honestly-labeled simulation (the DeliveryOps/CustomerPulse sync) — nothing
pretends to be a real integration that isn't."

**If asked "why aren't Design of Record and Execution Plan where you
process a new deal?":** "Processing a deal is one continuous decision, not
three destinations to navigate between. Those sidebar items are the
historical record of what's already been processed."

**If asked "why is Audit Log marked TBD when it was in scope before?":**
"I cut it early to stay focused on the core proof point, then reinstated
it once the rest of the surface was solid — it's genuinely useful, just
not load-bearing for what's being graded here, so it's honestly labeled as
not-yet-built rather than rushed."
