# Chile MoE-XGB event-stratified dataset

This repository provides the final training, validation, and test datasets used to develop and evaluate a ground-motion prediction model for Chile. The records originate from the publicly accessible SIBER-RISK strong-motion database described by Castro et al. (2022).

## Event-level split

The data were split **by complete earthquake event**, rather than by individual ground-motion record. `Earthquake Name` was used as the event identifier. All records associated with one earthquake were assigned to exactly one subset.

This design prevents records from the same earthquake from appearing in both model development and evaluation data. It therefore reduces event leakage and gives a more realistic estimate of generalization to previously unseen earthquakes.

The requested allocation was approximately 80% training, 10% validation, and 10% testing. Stratification considered event type and moment-magnitude interval. Candidate splits were generated with fixed random seeds, and the selected split balanced event metadata without using ground-motion response targets.

## Released datasets

| File | Purpose | Records | Unique events | Record share | Event share |
| --- | --- | ---: | ---: | ---: | ---: |
| `train.csv` | Model fitting | 3,808 | 563 | 79.98% | 79.86% |
| `val.csv` | Model selection and validation | 475 | 71 | 9.98% | 10.07% |
| `test.csv` | Final independent evaluation | 478 | 71 | 10.04% | 10.07% |
| **Total** |  | **4,761** | **705** | **100%** | **100%** |

Event-overlap checks for the released files:

- train-validation overlap: 0 events
- train-test overlap: 0 events
- validation-test overlap: 0 events

The initial split audit covered 4,796 source records and 708 events. The three analysis-ready CSV files released here contain 4,761 records and 705 events after dataset preparation. The event-level separation remains intact in the released files.

## Data structure

Each CSV contains 128 columns:

- Event metadata: earthquake identifier, date, origin/record time, moment magnitude, hypocenter coordinates, depth, and event type.
- Station and path metadata: station name/code and coordinates, sampling interval, hypocentral, epicentral, rupture, and Joyner-Boore distances, Vs30, azimuth, HVSR, processing status, and update information.
- Ground-motion response columns: `0` represents PGA, while the remaining numeric column names represent spectral periods in seconds from 0.01 to 10 s. The source dataset is identified as the geometric-mean response dataset with damping ratio `xi = 0.02`.

The files preserve the original column names and values used in the modeling workflow.

## Integrity checks

SHA-256 checksums:

```text
train.csv  aca5e9cb255bebb24c86c26c838cab217fa4e536aec446c144a88d635ea8fe33
val.csv    70a086e68dbc00b149e8ce7270343898790a771d3a413a41c4294abf1942feb4
test.csv   c049cb63ff4d3a4bb29a8091371a630f2ef312c4a29c7d77d1f58fee736c64e8
```

## Data source

Castro, S., Benavente, R., Crempien, J. G. F., Candia, G., & de la Llera, J. C. (2022). A consistently processed strong-motion database for Chilean earthquakes. *Seismological Research Letters, 93*(5), 2700-2718. https://doi.org/10.1785/0220200336

SIBER-RISK Strong Motion Database: https://siberrisk.ing.puc.cl/StrongMotionDatabase

Users should also follow the original database's terms and citation requirements.

## Citing this dataset

Until an archived DOI is assigned, please cite the repository as:

> Dai, J. (2026). *Chile MoE-XGB event-stratified dataset* [Data set]. GitHub. https://github.com/djf18130297878-cyber/Chile-MoE-XGB-dataset

Suggested manuscript wording:

> The final analysis-ready strong-motion datasets were divided at the earthquake-event level into training, validation, and independent test subsets and are publicly available at https://github.com/djf18130297878-cyber/Chile-MoE-XGB-dataset.
