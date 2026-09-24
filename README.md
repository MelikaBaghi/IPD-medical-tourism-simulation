# Managing Shared Hospital Capacity for Medical Tourism: a Hybrid Agent-Based and Discrete-Event Simulation

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22646799.svg)](https://doi.org/10.5281/zenodo.22646799)

A behavior-explicit hybrid (ABS + DES) simulation, built in AnyLogic, of a multi-specialty
international-patient hospital department that serves **medical tourists and local patients
from the same beds, specialists and appointment slots**.

**Melika Baghi** and Hadi Mosadegh
Department of Industrial and Systems Engineering, Amirkabir University of Technology, Tehran, Iran

## What makes it hybrid

- **Agent-based patient behavior.** Medication adherence, physician switching, online versus
  in-person channel choice, and early abandonment are part of the operational logic rather
  than post-hoc discussion.
- **Bed-sharing routine (known issue).** A daily routine among the compatible sections
  (cardiology, internal medicine, breast oncology) is meant to let a congested ward borrow idle
  beds; as implemented it never adds beds. See *Known issue: bed-sharing routine* below.
- **Discrete-event patient flow.** Visits, hospitalization, recovery and re-presentation.

## Headline result

Across 30 hybrid and 36 discrete-event-only randomized-seed replications at a bed-constrained configuration, the hybrid model's
mean inpatient admission waiting time is **14.8 days against 25.8 days** in an otherwise
identical discrete-event-only model (about 42 percent lower, *p* < 0.001), and the gap
persists (25 to 64 percent) at higher demand and at larger bed counts. The difference is the
combined effect of the patient-behavior mechanisms, which the discrete-event-only version
removes. The bed-sharing routine runs in both versions and adds no beds (see below), so the
comparison does not evaluate bed sharing. The behavior mechanisms also make patient
abandonment and adherence-driven emergency escalation visible, which a pure discrete-event
model omits by construction.

## Known issue: bed-sharing routine

Beds are transferred by two daily events of `Main`, `BorrowFromSections` and
`TakeBackeFromSections`, over sections 1, 2 and 5. A section is flagged as short of beds when
more than three patients wait for a bed, and as able to lend when `occupied / Beds >= 0.5`;
both operands are integers, so this holds only when every bed is occupied. Flags are cleared
only by a transfer. The borrower adds `floor((occupied - Beds) * 0.5)` of the lender to its
`TotalBeds`, which is zero for a full lender and negative when the lender's flag is stale.
Every section starts with `TotalBeds = Beds`, so no transfer is ever positive: a negative
transfer lowers the borrower's `TotalBeds` for the rest of the run, and the give-back event,
which acts only on positive transfers, never runs (its lines for sections 2 and 5 also
subtract section 1's transfer instead of their own). The discrete-event-only version used in
the paper runs the same two events. The model is kept exactly as it was run for the paper's
results; the rule described in the documentation, lending half of a section's free beds when
more than half of them are free, would replace the lender test with
`(Beds - occupied) * 2 > Beds` and the transfer with `floor((Beds - occupied) * 0.5)`.

## Run it

1. Open `IPD27_hybrid.alp` in **AnyLogic 8.9.8**. The Personal Learning Edition is enough.
2. Select the **Simulation** experiment and press **Run**.
3. Ward configuration (beds, specialists, slots) is read from the bundled `database/`
   folder, in the `HOSPITAL` table. As shipped it holds the bed-constrained configuration
   used for the paper's hybrid-versus-DES comparison (beds 30, 16, 22, 2, 16 and
   specialists 3, 5, 3, 3, 5 for sections 1 to 5); edit that table to try other
   configurations. Database logging is off, so runs are fast and the folder stays small.
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
| `docs/` | project landing page and `FACTORS.md`, the mapping of the paper's 16 screening factors to model elements |

## Citing this model

If you use, adapt, teach with, or build on this model, please cite it. The authorship and
license notice is embedded in the header of the `.alp` file itself.

> Baghi, M. and Mosadegh, H. (2026). *Managing Shared Hospital Capacity for Medical Tourism:
> Patient Behavior, Bed Sharing, and Hybrid Simulation* (software).
> https://doi.org/10.5281/zenodo.22646799

A machine-readable version is in [`CITATION.cff`](CITATION.cff), and GitHub renders it as a
"Cite this repository" button in the sidebar.

This model is archived in Zenodo under the DOI above. That DOI always resolves to the
newest version and gives the model a permanent, dated citation even if this repository
moves or is renamed. See [`RELEASING.md`](RELEASING.md) for how new versions are published.

## License

Model and code: **MIT** (see [`LICENSE`](LICENSE)).
Documentation and figures: **CC BY 4.0**.

MIT is permissive: you may use this commercially, modify it, and redistribute it. The one
condition is that the copyright and license notice stays with it. That notice names the
authors, which is the point.

## Requirements

AnyLogic 8.9.8, Personal Learning Edition or higher. No other dependencies.
