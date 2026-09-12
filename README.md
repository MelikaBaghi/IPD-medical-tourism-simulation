# Medical-Tourist Hospital Flow: a Hybrid Agent-Based and Discrete-Event Simulation

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22646799.svg)](https://doi.org/10.5281/zenodo.22646799)

A behaviour-explicit hybrid (ABS + DES) simulation, built in AnyLogic, of a multi-specialty
international-patient hospital department that serves **medical tourists and local patients
from the same beds, specialists and appointment slots**.

**Melika Baghi** and Hadi Mosadegh
Department of Industrial and Systems Engineering, Amirkabir University of Technology, Tehran, Iran

## What makes it hybrid

- **Agent-based patient behaviour.** Medication adherence, doctor switching, online versus
  in-person channel choice, and early abandonment are part of the operational logic rather
  than post-hoc discussion.
- **Compatible-section bed sharing.** Wards borrow each other's idle beds through
  inter-agent message passing.
- **Discrete-event patient flow.** Visits, hospitalisation, recovery and re-presentation.

## Headline result

Across 30 randomized-seed replications, compatible-section bed sharing reduces the mean
inpatient admission queue by **43 percent** (25.9 to 14.8 days, *p* < 0.001) against an
otherwise identical discrete-event-only model. The agent layer also reproduces patient
abandonment, emergency escalation and realistic throughput that a pure discrete-event model
suppresses by construction.

## Run it

1. Open `IPD27_hybrid.alp` in **AnyLogic 8.9.8**. The Personal Learning Edition is enough.
2. Select the **Simulation** experiment and press **Run**.
3. Ward configuration (beds, specialists, slots) is read from the bundled `database/`
   folder, in the `HOSPITAL` table. The run-log database rebuilds itself on first run.
4. Optionally, results append to a CSV. The path is set in the experiment's *After
   simulation run* action; change it to a folder on your machine.

### Run it in a browser instead

An interactive web build runs on AnyLogic Cloud, so you can press play and watch the
dashboard without installing anything:

**https://cloud.anylogic.com/model/ddca6c4e-7a3b-4015-bd9f-fb8d02cb30be**

The `.alp` file here is the editable source.

## Contents

| Path | What |
|---|---|
| `IPD27_hybrid.alp` | the hybrid ABS+DES model |
| `database/` | the model's configuration database, required to run |
| `docs/` | project landing page |

## Citing this model

If you use, adapt, teach with, or build on this model, please cite it. The authorship and
licence notice is embedded in the header of the `.alp` file itself.

> Baghi, M. and Mosadegh, H. (2026). *Compatible-Section Bed Sharing and Behavioural Risk
> in a Shared Medical-Tourism Hospital Department: A Hybrid Agent-Based and Discrete-Event
> Simulation* (software). https://doi.org/10.5281/zenodo.22646799

A machine-readable version is in [`CITATION.cff`](CITATION.cff), and GitHub renders it as a
"Cite this repository" button in the sidebar.

This model is archived in Zenodo under the DOI above. That DOI always resolves to the
newest version and gives the model a permanent, dated citation even if this repository
moves or is renamed. See [`RELEASING.md`](RELEASING.md) for how new versions are published.

## Licence

Model and code: **MIT** (see [`LICENSE`](LICENSE)).
Documentation and figures: **CC BY 4.0**.

MIT is permissive: you may use this commercially, modify it, and redistribute it. The one
condition is that the copyright and licence notice stays with it. That notice names the
authors, which is the point.

## Requirements

AnyLogic 8.9.8, Personal Learning Edition or higher. No other dependencies.
