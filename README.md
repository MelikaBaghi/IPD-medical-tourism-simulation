# Medical-Tourist Hospital Flow — Hybrid Agent-Based + Discrete-Event Simulation

A behaviour-explicit **hybrid (ABS + DES)** simulation, built in AnyLogic, of a multi-specialty
international-patient hospital department that serves **medical tourists and local patients** from
the *same* beds, specialists, and appointment slots.

> **Baghi, M. & Mosadegh, H.** — Department of Industrial and Systems Engineering,
> Amirkabir University of Technology, Tehran, Iran. Submitted to *Health Care Management Science*.

## What makes it a *hybrid* model
- **Agent-based patient behaviour** — medication adherence, doctor switching, online vs. in-person
  channel choice, and early abandonment are part of the operational logic, not post-hoc discussion.
- **Compatible-section bed sharing** — wards borrow each other's idle beds through inter-agent
  message passing.
- **Discrete-event patient flow** — visits, hospitalisation, recovery, and re-presentation.

## Headline result
Across 30 randomized-seed replications, compatible-section bed sharing **reduces the mean inpatient
admission queue by 43%** (25.9 -> 14.8 days; *p* < 0.001) versus an otherwise-identical
discrete-event-only model. The agent layer additionally reproduces patient abandonment, emergency
escalation, and realistic throughput that a pure discrete-event model suppresses by construction.

## Run it
1. Open **`IPD27_hybrid.alp`** in **AnyLogic 8.9.8** (Personal Learning Edition is sufficient).
2. Select the **Simulation** experiment -> **Run**.
3. Ward configuration (beds, specialists, slots) is read from the bundled **`database/`**
   (the `HOSPITAL` table). The run-log database is rebuilt automatically on first run.
4. *(Optional)* results are appended to a CSV — the path is set in the experiment's
   *After simulation run* action; change it to a folder on your machine.

## Contents
| Path | What |
|---|---|
| `IPD27_hybrid.alp` | the hybrid ABS+DES model |
| `database/` | the model's configuration database (`HOSPITAL` ward table) |
| `designs/` | user-interface / dashboard designs |

## Requirements
AnyLogic 8.9.8 (PLE or higher). No other dependencies.

## Citation
Baghi, M. & Mosadegh, H. (2026). *Reducing Waiting Time for Medical Tourists Through Hybrid
Agent-Based and Discrete-Event Simulation: A Hospital Case Study* (software).
DOI: _added on archival to Zenodo._

## License
- Code & model: **MIT** (see `LICENSE`).
- Data, figures, documentation: **CC-BY-4.0** (https://creativecommons.org/licenses/by/4.0/).
