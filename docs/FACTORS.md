# Screening factors and where they live in the model

The paper's screening experiment varies 16 factors, coded A to P. This table maps each
factor to the element of `IPD27_hybrid.alp` (or its `database/` folder) that implements it.
Section numbering follows the case study's specialist list: 1 = cardiology, 2 = internal
medicine, 3 = cosmetic surgery, 4 = pediatrics, 5 = breast oncology. The `Disease` enum labels
in the code (`BreastCancer`, `LungCancer`, `HeartDisease`, `CosmeticSurgery`, `ColonCancer`, in
that section order) are placeholders kept from an early build and do not describe the sections;
the per-section clinic schedules (`Specialist1WorkingTime` to `Specialist5WorkingTime`) match the
specialists' documented timetables in the order above. Sections 1, 2, and 5 form the
bed-sharing group (`BorrowFromSections`); sections 3 and 4 keep their beds. As implemented, the
sharing routine never adds beds (README, *Known issue: bed-sharing routine*).

| Factor | Meaning | Where it is set | Value in the released model |
|---|---|---|---|
| A to E | Beds in sections 1 to 5 | `database/` table `HOSPITAL`, column `BEDS` (row `SECTION` 1 to 5) | 30, 16, 22, 2, 16 |
| F to J | Specialists in sections 1 to 5 | `HOSPITAL`, column `SPEC` | 3, 5, 3, 3, 5 |
| K | Share of medical tourists routed to online consultation | Patient agent, channel decision in the `OnlineOrNot` branch (tourist probability) | model default |
| L | Share of local patients routed to online consultation | Same branch, local probability | model default |
| M | Online bed-scheduling rule | `Main` function `schedulingToHospitalizationOnline`: with the rule on (high level), a referral is deferred by `DaysAfter` days when the section's `WaitForEmptyBed` queue is longer than `noEmpty`; with the rule off (low level), the referral takes the next available position | Deferred (high): `DaysAfter = 10`, `noEmpty = 10` |
| N | In-person bed-scheduling rule | `Main` functions `schedulingToHospitalization` (direct placement in the section's `Bed` list) and `schedulingToHospitalizationInPerson` (placement deferred by `DaysAfter`), selected at the `StayOrNot` branch: direct when `randomTrue(0.7) || stayOrNot(agent)` holds, where `stayOrNot` is true while the section's `WaitForEmptyBed` queue is shorter than `noEmpty`; deferred otherwise | mixed rule as described (`noEmpty = 10`, `DaysAfter = 10`) |
| O | Admission-queue priority rule | Priority assigned to a patient at the admission branch (`agent.priority`): tourists first (`4`), locals next (`3`), online-referred patients behind both (`2`); served through `waitForEmptyBed_priority`. The high level of O replaces this with service in order of referral | Tourists first (low level) |
| P | Clinic appointment-slot interval | `Main` parameter `slot` (minutes), the recurrence of the `WorkingTimes` slot event | 2 minutes |

Other `Main` parameters that stay fixed in the paper: `dailyPatient` (16 in the released
model; 24 in the screening experiment and the robustness checks), `nPractitioners` (3),
`Ratio` (0.1, the tourist share of arrivals).

In the original screening experiment the two levels of the rule factors M, N and O were
applied by switching between the code paths named above; the released model ships with
one setting of each, listed in the last column. The arrival rate and the bed and specialist
counts used for each reported experiment are stated in the paper.
