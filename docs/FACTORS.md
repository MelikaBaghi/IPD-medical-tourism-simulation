# Screening factors and where they live in the model

The paper's screening experiment varies 16 factors, coded A to P. This table maps each
factor to the element of `IPD27_hybrid.alp` (or its `database/` folder) that implements it.
Section numbering: 1 = breast oncology (`BreastCancer`), 2 = internal medicine
(`LungCancer`), 3 = cardiology (`HeartDisease`), 4 = cosmetic surgery (`CosmeticSurgery`),
5 = pediatrics (`ColonCancer`); the names in code are the enum labels kept from the original
build and do not change the model logic.

| Factor | Meaning | Where it is set | Value in the released model |
|---|---|---|---|
| A to E | Beds in sections 1 to 5 | `database/` table `HOSPITAL`, column `BEDS` (row `SECTION` 1 to 5) | 30, 16, 22, 2, 16 |
| F to J | Specialists in sections 1 to 5 | `HOSPITAL`, column `SPEC` | 3, 5, 3, 3, 5 |
| K | Share of medical tourists routed to online consultation | Patient agent, channel decision in the `OnlineOrNot` branch (tourist probability) | model default |
| L | Share of local patients routed to online consultation | Same branch, local probability | model default |
| M | Online bed-scheduling rule | `Main` function `schedulingToHospitalizationOnline`: with the rule on (high level), a referral is deferred by `DaysAfter` days when the section's `WaitForEmptyBed` queue is longer than `noEmpty`; with the rule off (low level), the referral takes the next available position | Deferred (high): `DaysAfter = 10`, `noEmpty = 10` |
| N | In-person bed-scheduling rule | `Main` functions `schedulingToHospitalization` (direct placement in the section's `Bed` list) and `schedulingToHospitalizationInPerson` (placement deferred by `DaysAfter`), selected at the in-person admission branch | branch controlled by the `decision` parameter (0.8) |
| O | Admission-queue priority rule | Priority assigned to a patient at the admission branch (`agent.priority`): tourists first (`4`), locals next (`3`), online-referred patients behind both (`2`); served through `waitForEmptyBed_priority`. The high level of O replaces this with service in order of referral | Tourists first (low level) |
| P | Clinic appointment-slot interval | `Main` parameter `slot` (minutes), the recurrence of the `WorkingTimes` slot event | 2 minutes |

Other `Main` parameters that stay fixed in the paper: `dailyPatient` (16 in the released
model; 24 in the screening experiment and the robustness checks), `nPractitioners` (3),
`Ratio` (0.1, the tourist share of arrivals).

In the original screening experiment the two levels of the rule factors M, N and O were
applied by switching between the code paths named above; the released model ships with
one setting of each, listed in the last column. The arrival rate and the bed and specialist
counts used for each reported experiment are stated in the paper.
