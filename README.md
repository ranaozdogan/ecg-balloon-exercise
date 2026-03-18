# ECG Analysis: Pre- vs Post-Exercise (Balloon Inflation)

This project had been conducted within the scope of the BENG306-BIOINSTRUMENTATION course. This project analyses ECG signals recorded before and after a 2-minute balloon inflation exercise from **31 anonymised subjects**, using Neurobridge3 ECG sensors.

## Study Design

Each subject has two 30-second ECG recordings:

| File pattern          | Description                                            |
| --------------------- | ------------------------------------------------------ |
| `ECG_SUBxxx_PRE.csv`  | Baseline — recorded before exercise                    |
| `ECG_SUBxxx_POST.csv` | Post-exercise — recorded after 2-min balloon inflation |

Subject identities are anonymised. The mapping key (`PRIVATE_subject_mapping.csv`) is stored separately and **not included** in this repository.

## Analysis Pipeline

The notebook `ecg_analysis.ipynb` covers the full pipeline:

1. **Signal preprocessing** — Butterworth low-pass filter (40 Hz cutoff) + Savitzky-Golay smoothing
2. **R-peak detection** — `scipy.signal.find_peaks` with adaptive threshold
3. **Feature extraction** — BPM, mean RR interval, SDNN (HRV proxy)
4. **Per-subject visualisation** — dual-panel ECG plots for PRE and POST
5. **Statistical analysis** — Shapiro-Wilk normality check + paired t-test (PRE vs POST BPM)
6. **Group-level visualisation** — bar charts, paired slope plot, delta histogram, SDNN scatter

## Repository Structure

```
ecg_project/
├── ecg_analysis.ipynb       # Main analysis notebook
├── ecg_results.csv          # Output: per-subject feature table (generated)
├── ecg_group_summary.png    # Output: summary figure (generated)
├── requirements.txt         # Python dependencies
├── data/                    # Place anonymised CSV files here (not tracked by git)
│   ├── ECG_SUB001_PRE.csv
│   ├── ECG_SUB001_POST.csv
│   └── ...
└── README.md
```

## Getting Started

```bash
# 1. Clone the repository
git clone https://github.com/ranaozdogan/ecg-balloon-exercise.git
cd ecg-balloon-exercise

# 2. Install dependencies
pip install -r requirements.txt

# 3. Place the anonymised CSV files in the data/ folder

# 4. Open and run the notebook
jupyter notebook ecg_analysis.ipynb
```

## Dependencies

See `requirements.txt`. Key packages:

- `pandas`, `numpy` — data loading and manipulation
- `scipy` — signal filtering, peak detection, statistical tests
- `matplotlib` — visualisation

## Results

The notebook produces:

- A summary table (`ecg_results.csv`) with BPM, RR interval, and SDNN for each subject pre/post
- A paired t-test result comparing heart rate before and after balloon inflation exercise
- A group summary figure (`ecg_group_summary.png`)

## Ethics & Privacy

All participants were informed prior to data collection that their health data and ECG measurements would be shared exclusively in anonymised form. Informed consent was obtained from each participant before their involvement in the study, covering the collection, processing, and anonymous publication of their physiological data. 
All subject identifiers have been removed from the dataset before inclusion in this repository. The private name-to-ID mapping is stored securely offline and is not accessible through this repository.
