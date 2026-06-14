# Reducing Waiting Time for Medical Tourists via Hybrid Agent-Based + Discrete-Event Simulation

Simulation model and supplementary materials for:

**Baghi, M. & Mosadegh, H.** *"Reducing Waiting Time for Medical Tourists Through Hybrid
Agent-Based and Discrete-Event Simulation: A Hospital Case Study."* Submitted to
*Health Care Management Science*.
Department of Industrial and Systems Engineering, Amirkabir University of Technology, Tehran, Iran.

## Contents
- `IPD27_hybrid.alp` — the **hybrid** ABS+DES model (AnyLogic 8.9.8).
- `IPD27_DES.alp` — the **DES** variant (compatible-section bed sharing disabled), used for the
  hybrid-vs-DES comparison.
- `designs/` — user-interface / dashboard designs.
- `data/` — run-output data is **not** included here (see `data/README.md`); the complete results
  accompany the archived release and are available from the authors on request.

## Requirements
Open the `.alp` files with **AnyLogic 8.9.8** (Personal Learning Edition is sufficient).

## How to run
Open a model -> select the **Simulation** experiment -> **Run**. Each completed run appends one row
of results to a CSV (path is set in the experiment's *After simulation run* action -- change it to
your own folder).

## Response variables (result columns)
| Column | Meaning |
|---|---|
| `TouristWaitHospQueue` | mean medical-tourist wait in hospital admission queue (days) -- headline |
| `WaitHospQueue`, `WaitSystem` | mean waits (days) |
| `EarlyLeave`, `EmergencyBeforeTurn`, `Recovered` | event counts |
| `Util_Spec1`..`Util_Spec5`, `Util_Practitioner` | specialist utilisation (%) |

## Citation
Baghi, M. & Mosadegh, H. (2026). *Reducing Waiting Time for Medical Tourists ...* (software).
DOI: _(added after archiving this release to Zenodo)_

## License
- Source code and simulation models: **MIT** (see `LICENSE`).
- Data, figures, and documentation: **CC-BY-4.0** (https://creativecommons.org/licenses/by/4.0/).
