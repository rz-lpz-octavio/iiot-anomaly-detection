# Dataset Exploration Notes - SKAB

**Date:** 2025-01-15
**Dataset:** SKAB (Skoltech Anomaly Benchmark)
**Source:** https://github.com/waico/SKAB

---

## Exploration Log

### Step 1: Understanding what we downloaded

**Action:** List SKAB directory structure

**Main directory contents:**
```
- README.md (10.7 KB)
- LICENSE (35.1 KB)
- core/ (Python source code directory)
- data/ (dataset files)
- docs/ (documentation)
- notebooks/ (example notebooks)
- results/ (benchmark results)
- pyproject.toml (Python project config)
- poetry.lock (dependency lock file)
```

**Data directory structure:**
```
data/
├── README.md
├── anomaly-free/
│   └── anomaly-free.csv (1 file)
├── valve1/
│   └── 0.csv through 15.csv (16 files)
├── valve2/
│   └── 0.csv through 3.csv (4 files)
└── other/
    └── 1.csv through 14.csv (14 files)
```

**Total data files:** 1 + 16 + 4 + 14 = 35 CSV files

**Initial observations:**
- Data is organized by scenario (anomaly-free, valve1, valve2, other)
- valve1 and valve2 likely represent specific anomaly types
- "other" might be additional anomaly scenarios
- Each scenario has multiple CSV files (experiments/runs?)

---

### Step 2: Verify data integrity & record version

**Purpose:** Document EXACTLY which version of SKAB we're using for reproducibility.

**Git repository information:**
```
Remote URL: https://github.com/waico/SKAB.git
Branch: master
```

**Version we downloaded:**
```
Commit Hash: b2c0d46c2971dcbfe71e26087b6d231998bb91c2
Commit Date: 2024-08-11 23:53:38 +0300
Commit Message: "Misprints and links in README.md fixed"
```

**Official releases:**
```
Latest tagged release: v0.9.0
  Tag commit: 80bac4a00d9cd2a277a6fda8f6a6d5936b892bd2
  Tag date: 2023-08-09 20:17:08 +0300
  Tag message: "Annual update, a lot of information added and updated"

Our position: 9 commits AFTER v0.9.0 release
```

**What this means:**
- We are NOT using the official v0.9.0 release
- We are using a development version (master branch, post-v0.9.0)
- The 9 commits after v0.9.0 include minor updates and fixes
- For our research, we should cite: "SKAB dataset (commit b2c0d46, post-v0.9.0)"

**Reproducibility note:**
To get the EXACT same data we're using, someone would run:
```bash
git clone https://github.com/waico/SKAB.git
cd SKAB
git checkout b2c0d46c2971dcbfe71e26087b6d231998bb91c2
```

**Download date:** 2025-01-15

---

### Step 3: Understanding SKAB documentation

**Purpose:** Read official documentation to understand dataset structure, sensors, anomaly types, and citation requirements.

**Dataset Overview:**
- Name: Skoltech Anomaly Benchmark (SKAB)
- Version: v0.9 (35 datasets)
- Created by: Skoltech (Skolkovo Institute of Science and Technology)
- Authors: Katser, Iurii D. and Kozitsin, Vyacheslav O.
- Year: 2020
- DOI: 10.34740/KAGGLE/DSV/1693952
- Kaggle: https://www.kaggle.com/dsv/1693952

**Important notes:**
- Current version (v0.9): 34 datasets with collective anomalies (plus 1 anomaly-free)
- Future v1.0 planned: 300+ additional files
- Testbed currently under repair (as of last update)
- Each dataset represents ONE experiment with ONE anomaly

**Sensor Columns:**
Each CSV file contains the following columns:
1. `datetime` - Timestamp (YYYY-MM-DD hh:mm:ss)
2. `Accelerometer1RMS` - Vibration acceleration (g units)
3. `Accelerometer2RMS` - Vibration acceleration (g units)
4. `Current` - Electric motor amperage (Ampere)
5. `Pressure` - Pressure after water pump (Bar)
6. `Temperature` - Engine body temperature (Celsius)
7. `Thermocouple` - Fluid temperature in circulation loop (Celsius)
8. `Voltage` - Electric motor voltage (Volt)
9. `RateRMS` - Circulation flow rate (Liter per minute)
10. `anomaly` - Binary label for outlier detection (0=normal, 1=anomalous)
11. `changepoint` - Binary label for changepoint detection (0=normal, 1=changepoint)

**Testbed Description:**
Industrial water circulation system with:
- Water pump with electric motor
- Valves (inlet and outlet)
- Sensors monitoring vibration, temperature, pressure, flow, electrical parameters

**Anomaly Scenarios:**

1. **anomaly-free/** (1 file)
   - Normal operation mode
   - No anomalies

2. **valve1/** (16 files)
   - Valve closing at flow INLET to pump
   - Simulates restricted water supply to pump

3. **valve2/** (4 files)
   - Valve closing at flow OUTLET from pump
   - Simulates blocked discharge from pump

4. **other/** (14 files)
   - Files 1-4: Fluid leaks and fluid additions
   - Files 5-9: Various rotor imbalance behaviors (sharp, linear, step, delta, exponential)
   - File 10: Slow water increase in circuit
   - File 11: Sudden water increase in circuit
   - File 12: Water draining until cavitation
   - File 13: Two-phase flow (cavitation)
   - File 14: Increased temperature water supply

**Two Types of Anomaly Detection Problems:**
1. Outlier detection - Single-point anomalies (using `anomaly` column)
2. Changepoint detection - Collective anomalies (using `changepoint` column)

**Benchmark Leaderboard Context:**
SKAB includes leaderboards for both problems. Key baseline algorithms:
- Isolation Forest: F1=0.29 (outlier), NAB=26.16 (changepoint)
- Conv-AE: F1=0.78 (outlier), NAB=23.61 (changepoint)
- LSTM-AE: F1=0.74 (outlier), NAB=23.51 (changepoint)
- PCA-based methods, MSET, etc.

Note: Our research focus is lightweight models (<1MB), so Isolation Forest is relevant baseline.

**Citation Format (BibTeX):**
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

**License:** GPL v3.0

**For our paper, we should cite as:**
"SKAB dataset (Katser & Kozitsin, 2020) commit b2c0d46, post-v0.9"

