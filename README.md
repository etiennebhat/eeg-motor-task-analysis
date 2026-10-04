# EEG Motor-Task Spectral Analysis

An exploratory computational neuroscience project analyzing EEG activity during left- and right-hand motor execution using Python and MNE-Python.

## Research Question

**How does EEG spectral activity differ between left- and right-hand motor execution, and where on the scalp are these differences most pronounced?**

## Dataset

This project uses the **PhysioNet EEG Motor Movement/Imagery Dataset**, accessed through MNE-Python.

For this analysis:

* Subject: 1
* Runs: 3, 7, and 11
* Conditions: rest, left-hand movement, right-hand movement
* Sampling frequency: 160 Hz

The data contain real human EEG recordings collected during a motor task.

## Analysis Pipeline

The analysis follows these main steps:

1. Load and combine repeated motor-task runs.
2. Standardize EEG channel names and assign standard electrode locations.
3. Inspect the experimental event markers.
4. Apply an average EEG reference.
5. Band-pass filter the data from 1–40 Hz.
6. Extract event-based epochs from 1.0–3.9 seconds after each experimental event.
7. Screen epochs for large peak-to-peak amplitudes as a basic artifact-quality check.
8. Estimate power spectral density (PSD) using Welch's method.
9. Calculate theta, alpha, and beta band power.
10. Calculate relative band power.
11. Examine activity over a sensorimotor region of interest.
12. Compare spectral features between left- and right-hand conditions.
13. Visualize left-versus-right beta-power differences using scalp topography.
14. Perform exploratory statistical comparisons.

## Frequency Bands

The analysis uses commonly studied EEG frequency ranges:

| Band  | Frequency range |
| ----- | --------------: |
| Theta |          4–8 Hz |
| Alpha |         8–13 Hz |
| Beta  |        13–30 Hz |

These frequency boundaries are methodological choices and are not universal definitions.

## Sensorimotor Region of Interest

The primary regional analysis uses the following EEG channels when available:

`C3, C1, Cz, C2, C4, CP3, CP4`

These electrodes provide coverage around the central and centro-parietal scalp regions associated with sensorimotor processing.

## Spectral Measures

Power spectral density is used to examine how signal power is distributed across frequencies.

For each epoch and EEG channel, the project calculates:

* Theta power
* Alpha power
* Beta power
* Relative theta power
* Relative alpha power
* Relative beta power
* Theta/alpha power ratio

Band power is estimated by integrating the PSD across each frequency band.

## Visualizations

The project produces:

* Sensorimotor PSD curves for each experimental condition
* Relative theta, alpha, and beta power comparisons
* Theta/alpha ratio comparisons
* A scalp topography showing left-versus-right beta-power differences

Figures are saved in the `figures/` directory.

## Statistical Analysis

The left- and right-hand conditions are compared using exploratory Mann–Whitney U tests for selected spectral features.

Bonferroni correction is applied across the tested features.

These statistical results are treated as exploratory because the current analysis uses recordings from a single participant rather than a multi-subject sample.

## Important Limitations

This is a **single-subject exploratory analysis** and should not be interpreted as evidence of a population-level effect.

The project is intended primarily as a learning and reproducible-analysis exercise. It does not claim to establish a general neural signature of left- or right-hand movement.

The artifact screening is also intentionally simple. More advanced EEG preprocessing could include methods such as ICA-based artifact correction and more detailed inspection of ocular and muscular artifacts.

## Future Directions

Possible extensions include:

* Repeating the analysis across multiple participants
* Examining event-related desynchronization/synchronization (ERD/ERS)
* Comparing contralateral and ipsilateral sensorimotor activity
* Performing time-frequency analysis
* Using common spatial patterns (CSP) for motor-condition decoding
* Training a classifier to distinguish left- versus right-hand movement
* Evaluating whether a model trained on one participant generalizes to others
* Using statistical models that explicitly account for repeated trials and multiple participants

## Tools

* Python
* MNE-Python
* NumPy
* Pandas
* SciPy
* Matplotlib

## Repository Structure

```text
comp neuro practice/
├── eeg_motor_task_analysis_rehearse.ipynb
├── README.md
├── figures/
└── results/
```

## Reproducibility

The raw EEG recordings are not included in this repository.

The notebook retrieves the public dataset through MNE-Python. The analysis outputs are saved locally in the `figures/` and `results/` directories.

## Disclaimer

This is an independent educational and exploratory computational neuroscience project, done as a rehearsal for actual research. The results should not be interpreted as a validated diagnostic, fatigue-detection, or brain-computer-interface system.
