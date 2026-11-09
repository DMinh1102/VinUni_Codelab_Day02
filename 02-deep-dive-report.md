# 02 - Deep-Dive Report: Xanh SM Charging Co-pilot

## Decision context

**Selected scope:** Help a Xanh SM dispatcher turn a driver low-battery report plus a trusted operational snapshot into a structured, human-reviewed next-step draft. The larger member brief describes live station guidance using battery state, trip demand, and charging availability. This prototype does not connect to those systems and must not imply it has real-time data.

**Evidence status:** The workflow and time estimates are working hypotheses for a lab exercise. No Xanh SM operator interviews, production logs, station feed, or measured baseline were provided. Validate before any production commitment.

## 3.1 Current-state workflow

```text
Driver reports low battery / charging concern
  -> [Handoff] Dispatcher opens vehicle and location view (assumed 2 min)
  -> Dispatcher checks battery, vehicle compatibility, and trip urgency (assumed 3 min)
  -> [Bottleneck] Dispatcher checks station availability, compatibility, and queue across tools (assumed 5 min)
  -> [Handoff] Dispatcher drafts and confirms guidance with driver (assumed 3 min)
  -> Dispatcher records outcome / escalates to charging support if needed (assumed 2 min)

Estimated touch time: 15 minutes per case (assumption; measure during discovery).
Bottleneck hypothesis: fragmented, potentially stale station and vehicle information.
```

These durations are estimates to help design discovery, not company-reported statistics. A shadowing study should record active handling time, waiting time, rework, station-data freshness, and outcome for a representative sample.

## 3.2 Problem statement (6 fields)

| Field | Statement |
|---|---|
| **1. Actor / Operator** | Xanh SM fleet dispatcher handling driver-reported charging concerns; the driver is the direct recipient of guidance. |
| **2. Current Workflow** | The dispatcher reviews a report, checks vehicle/battery/location and trip context, looks up a compatible station and its current status, then communicates a next step and records the case. The tools and sequence above are hypotheses to validate. |
| **3. Bottleneck** | Comparing several changing facts (battery, vehicle compatibility, distance, station availability/queue, and trip urgency) and communicating a clear recommendation. A stale or missing station snapshot makes recommendation unsafe. |
| **4. Business Impact** | Delayed decisions can keep a vehicle unavailable, increase driver and passenger waiting, or cause a missed trip. Impact is currently unquantified. Establish a baseline with case volume, median handling time, vehicle downtime, and rework; do not infer savings until measured. |
| **5. Success Metric** | Proposed pilot gates: (a) median time from complete report to reviewed guidance is at most 3 minutes and improves against the measured baseline; (b) at least 95% exact extraction of required fields on a dispatcher-labeled evaluation set; (c) zero recommendations that violate the critical-battery rule in adversarial tests; (d) 100% of outgoing actions have recorded human approval. Targets are hypotheses, not current performance. |
| **6. Operational Boundary** | The model may extract facts and draft one of `recommend_station`, `dispatch_mobile_charger`, or `request_human_review` from the supplied data. If battery is below 5%, it must select mobile-charger escalation and must not recommend a station. A station recommendation requires verified compatibility, availability, distance, and freshness in the input. Missing, stale, contradictory, or out-of-scope information means human review. The model cannot access live systems, send messages, dispatch resources, change trips, diagnose a vehicle, or override a dispatcher. A dispatcher approves every action. |

## 3.3 Future-state flow and AI fit

**AI fit:** A bounded LLM feature for understanding free-text driver reports and drafting an explanation, paired with deterministic rules for thresholds, required fields, and output validation. An autonomous agent is not justified: the task depends on live operational data and a mistaken action has real-world cost.

```text
1. Driver report + trusted structured snapshot
   -> 2. Deterministic input checks: required fields, data freshness, units
   -> 3. [AI] Extract report and draft a schema-constrained action/reason
   -> 4. Deterministic safety gate: battery < 5% => mobile charger;
         missing/stale/contradictory data => human review
   -> 5. [HUMAN] Dispatcher checks source data and approves/edits/rejects
   -> 6. Existing authorized workflow executes the action and records outcome

Fallback: model timeout, invalid JSON, low confidence, or failed safety gate
   -> no recommendation/action -> dispatcher uses the current manual process.
```

The prototype implements only steps 3-4 against text inputs and local adversarial cases. It does not implement data access or step 6. Structured output is a convenience for review, not proof that the content is correct.

## Phase 5 - Readiness and decision

| Readiness question | Status | Evidence / next action |
|---|---|---|
| Representative, approved sample reports and station snapshots available? | **No / unknown** | Request de-identified examples and confirm data owner, permitted use, and coverage. |
| Risk controlled through HITL and fallback? | **Partially** | Prototype boundary requires human approval and manual fallback; validate with an integration threat/safety review and dispatcher scenarios. |
| Operators ready to change workflow? | **Unknown** | Interview dispatchers, observe current handling, and test whether drafts reduce work without adding review burden. |

**Decision: NOT YET for production; proceed only with a bounded offline prototype and discovery.** The problem is plausible and the prompt boundary is testable, but no operational baseline, representative data, live station feed, or operator validation is available. Revisit the production decision after those prerequisites are met and the pilot gates are tested against labeled cases. A deterministic rule-based baseline should be measured alongside the LLM feature.
