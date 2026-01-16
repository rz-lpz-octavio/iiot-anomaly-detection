# Dataset Documentation

## SKAB - Skoltech Anomaly Benchmark

### Overview

**Dataset:** Skoltech Anomaly Benchmark (SKAB)
**Version:** v0.9 (post-release, commit b2c0d46)
**Source:** https://github.com/waico/SKAB
**Authors:** Katser, Iurii D. and Kozitsin, Vyacheslav O.
**Institution:** Skolkovo Institute of Science and Technology
**Year:** 2020
**DOI:** 10.34740/KAGGLE/DSV/1693952
**License:** GPL-3.0

### Dataset Description

SKAB is a benchmark dataset for evaluating anomaly detection algorithms in industrial systems. The data was collected from a water circulation testbed equipped with sensors monitoring an electric motor-driven pump system.

**Total files:** 35 CSV files
**Data collection:** Multivariate time series from industrial testbed
**Anomaly types:** Mechanical faults, valve malfunctions, fluid anomalies, cavitation, temperature variations

### Reproduction Instructions

To obtain the exact version used in this research:

```bash
cd data/raw/
git clone https://github.com/waico/SKAB.git
cd SKAB
git checkout b2c0d46c2971dcbfe71e26087b6d231998bb91c2
```

**Download date:** 2025-01-15

### Data Structure

```
data/raw/SKAB/data/
├── anomaly-free/        # Normal operation (1 file)
├── valve1/              # Inlet valve closure experiments (16 files)
├── valve2/              # Outlet valve closure experiments (4 files)
└── other/               # Other anomaly types (14 files)
```

Each CSV file represents one experiment containing one anomaly.

### Sensor Measurements

Each dataset contains 11 columns:

| Column | Description | Units |
|--------|-------------|-------|
| `datetime` | Timestamp | YYYY-MM-DD hh:mm:ss |
| `Accelerometer1RMS` | Vibration acceleration | g units |
| `Accelerometer2RMS` | Vibration acceleration | g units |
| `Current` | Electric motor current | Ampere |
| `Pressure` | Pump outlet pressure | Bar |
| `Temperature` | Engine body temperature | Celsius |
| `Thermocouple` | Fluid temperature | Celsius |
| `Voltage` | Electric motor voltage | Volt |
| `RateRMS` | Flow rate | L/min |
| `anomaly` | Outlier detection label | 0 or 1 |
| `changepoint` | Changepoint detection label | 0 or 1 |

### Anomaly Scenarios

**anomaly-free/** (1 file)
- Normal system operation

**valve1/** (16 files)
- Valve closure at pump inlet
- Simulates restricted water supply

**valve2/** (4 files)
- Valve closure at pump outlet
- Simulates discharge obstruction

**other/** (14 files)
- Fluid leaks and additions (files 1-4)
- Rotor imbalance variations (files 5-9)
- Water volume changes (files 10-11)
- Cavitation scenarios (files 12-13)
- Temperature anomaly (file 14)

### Citation

If using this dataset, cite:

```bibtex
@misc{skab,
  author = {Katser, Iurii D. and Kozitsin, Vyacheslav O.},
  title = {Skoltech Anomaly Benchmark (SKAB)},
  year = {2020},
  publisher = {Kaggle},
  howpublished = {\url{https://www.kaggle.com/dsv/1693952}},
  DOI = {10.34740/KAGGLE/DSV/1693952}
}
```

### Notes

- Version used: post-v0.9 development version (9 commits after v0.9.0 release)
- Each experiment contains exactly one anomaly
- Dataset supports two problem formulations: outlier detection and changepoint detection
- Original benchmark leaderboard available at: https://paperswithcode.com/sota/change-point-detection-on-skab
