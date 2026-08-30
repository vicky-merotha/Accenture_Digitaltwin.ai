# DigitalTwin.ai
### Predictive Digital Twin for Mixed-Model Assembly Lines
**Accenture Innovation Challenge 2026 — Round 2, Problem Track 4**

## Overview

DigitalTwin.ai is a predictive digital-twin prototype for a vehicle assembly line. It fuses uneven
sensor telemetry, manual inspection checklists, and historical quality data into one live model of
the line, and gives three different stakeholders — a floor supervisor, a plant manager, and plant
leadership — a view of that same model calibrated to what they each need to decide.

This repository contains the Round 2 working prototype referenced in the accompanying
**Business Proposal** (`DigitalTwin_ai_Business_Proposal.docx`).

## What the prototype demonstrates

The prototype is a self-contained, single-file web app (`index.html`) simulating a 42-station
mixed-model line (Body Construction → Paint → Final Assembly). It runs entirely on generated
sample data — no real plant connection or proprietary data is used, consistent with the challenge
guidance.

| Capability | Where to see it |
|---|---|
| Live station health scoring with SPC-style thresholds on sensor-equipped stations | Floor Supervisor → Live Station Map |
| Confidence-scored inference at simulated sensor-poor (manual-checklist) stations | Click any dashed-border station on the map |
| Bottleneck early-warning feed, with shadow-mode vs. validated alert status | Floor Supervisor → Real-Time Alert Feed |
| Role-specific views generated from one shared twin state | Nav tabs: Floor Supervisor / Plant Manager / Leadership |
| Low-cost sensor retrofit prioritization for the weakest-confidence stations | Plant Manager → Recommended Sensor Retrofits |
| Defect backward-tracing to candidate origin stations | Defect Backward-Trace tab — pick a defect, click "Trace Origin" |
| Investment case roll-up (downtime avoided, rework saved, ROI) | Leadership tab |

## Running it

No build step or dependencies are required.

```bash
git clone <this-repo-url>
cd digitaltwin-ai
open index.html   # or double-click the file / drag into a browser
```

The dashboard refreshes its simulated state every 5 seconds to mimic a live feed.

## Repository contents

```
.
├── index.html                                # working prototype (single-file, no build step)
├── DigitalTwin_ai_Business_Proposal.docx     # Round 2 business proposal
└── README.md
```

## Design notes / how it maps to the proposal

- **Uneven sensor coverage** — ~25% of stations are marked "manual" (dashed border on the line
  map). Their health is *inferred* rather than measured directly, and always shown with an explicit
  confidence percentage rather than a false-precision single number.
- **Validation before trust** — alerts are labeled either `Shadow-mode` (logged, not yet actionable)
  or `Active` (validated), reflecting the shadow-period gating described in the proposal's
  Phase 1 rollout.
- **Backward-tracing** — the trace view replays a selected defect's simulated path through six
  stations and ranks the most likely origin using a simple weighted score of anomaly severity and
  historical defect correlation, and flags other units that passed the same station in the same
  window for re-inspection.
- **Scalability** — the station-graph data model (`stations` array in `index.html`) is intentionally
  generic so the same code could represent a different line's layout, station count, or sensor mix
  by changing the generation parameters at the top of the script.

## Assumptions (illustrative, stated per challenge guidance)

- 42-station mixed-model line: 16 Body Construction, 10 Paint, 16 Final Assembly.
- ~25% of stations rely on manual checklists rather than live sensors.
- Baseline figures used in the Leadership/business-case view (downtime, escape rate, ROI) are
  directional placeholders for demonstration and would be recalibrated against a pilot line's real
  historical data during a Phase 0 discovery engagement.

## Demo video

_Add link to the recorded prototype walkthrough here before submission._

## License

Prototype built for the Accenture Innovation Challenge 2026. For challenge submission purposes only.
