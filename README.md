# PERCEIV Dataset

**P**ER**C**eption of Visual **E**ncodings **I**n Info**V**is: A Multimodal Physiological Dataset for Adaptive InfoVis Interfaces

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Dataset](https://img.shields.io/badge/Dataset-PERCEIV-blue.svg)]()
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)

---

## Overview

PERCEIV is a large-scale multimodal physiological dataset designed to support studies of user responses to visual encoding variants as a foundation for adaptive information visualization interfaces. The dataset contains synchronized recordings from **120 participants** who completed tasks of varying difficulty across three visualization types (graphs, timelines, and distribution charts), resulting in **14,400 feature-rich trials**.

This dataset captures the intersection of cognitive load, visual attention, and physiological responses during information visualization tasks, providing empirical evidence for developing user-model-driven adaptive InfoVis systems.

### Key Features

- **Multi-Modal Data Collection**: Synchronized EEG, Eye Tracking (ET), and Electrodermal Activity (EDA) recordings
- **Large-Scale Coverage**: 120 participants × 120 trials = 14,400 total trials
- **Three Visualization Types**: Network graphs, timelines, and distribution charts
- **Systematic Task Manipulation**: Question difficulty × Stimulus complexity × Visual adaptations
- **Rich Annotations**: Behavioral performance (accuracy, reaction time), trial-level metadata, and participant demographics
- **Preprocessed Data**: Epoched recordings and fully processed event-aligned derivatives (raw continuous files >100 MB available upon request)
- **Baseline ML Models**: Pre-trained classifiers and feature extraction pipelines for cognitive load estimation
- **Reproducible Research**: Complete preprocessing code, standardized data splits, and comprehensive documentation

> **📦 Repository Note**: Files exceeding 100 MB have been omitted from this repository. For access to full raw continuous recordings, please contact the authors at sebastian.idesis@gmail.com

---

## Dataset Description

### Experimental Design

Participants were randomly assigned to one of three visualization types and completed 120 trials, each consisting of:

1. **Fixation cross** (1 second)
2. **Question screen** (self-paced)
3. **Visualization screen** (up to 10 seconds for response)
4. **Rest period** (self-paced)

#### Independent Variables

1. **Question Difficulty** (Low/High)
   - Low: Simple feature detection (e.g., "How many females are shown?")
   - High: Multi-attribute integration (e.g., "How many females have been arrested more than 10 times?")

2. **Stimulus Complexity** (Low/High)
   - Graph: 3 nodes (low) vs. 6 nodes (high)
   - Timeline: 2 callers over 5 hours (low) vs. 4 callers over 12 hours (high)
   - Distribution: 5 hours (low) vs. 24 hours (high)

3. **Visual Adaptation** (Baseline/Adapted)
   - Adapted stimuli: Enhanced node size, color encoding, edge thickness for task-relevant information
   - 40 of 120 trials per participant included visual adaptations

#### Dependent Variables

- **Behavioral**: Accuracy, reaction time
- **EEG**: Theta power, frontal alpha asymmetry, spectral/amplitude entropy, phase-locking value
- **Eye Tracking**: Pupil dilation, fixation amount/duration, saliency coverage/entropy
- **EDA**: Area under curve, number of peaks, time to peak, recovery time, peak amplitude

---

## Repository Structure

```
perceiv/
├── 📁 Graph/                        # Network graph visualization data
│   ├── Graph EDA/                   # Electrodermal activity recordings
│   ├── Graph EEG/                   # EEG recordings
│   └── Graph ET/                    # Eye tracking recordings
├── 📁 Timeline/                     # Timeline visualization data
│   ├── Timeline EDA/                # Electrodermal activity recordings
│   ├── Timeline EEG/                # EEG recordings
│   └── Timeline ET/                 # Eye tracking recordings
├── 📁 Distribution/                 # Distribution chart visualization data
│   ├── Distribution EDA/            # Electrodermal activity recordings
│   ├── Distribution EEG/            # EEG recordings
│   └── Distribution ET/             # Eye tracking recordings
├── 📄 .gitignore                    # Git ignore configuration
├── 📄 README.md                     # This file
└── 📄 LICENSE                       # License information
```

### Data Organization

Each visualization type folder contains three modality subfolders:

#### EEG Data
- **Site 1**: 32-channel gel-based actiCHamp system (Brain Products, 256 Hz)
- **Site 2**: 12-channel dry-electrode Bitbrain Diadem system (256 Hz)
- **Features**: Theta power, frontal alpha asymmetry, spectral entropy, amplitude entropy, theta-band phase-locking value

#### Eye Tracking (ET) Data
- **Device**: GP3 HD Eye Tracker (150 Hz) at both sites
- **Features**: Pupil dilation, fixation amount, fixation duration, saliency coverage, saliency entropy
- **Calibration**: 5-point calibration with quality control

#### Electrodermal Activity (EDA) Data
- **Site 1**: actiCHamp integrated sensor (250 Hz, finger electrodes)
- **Site 2**: Bitbrain Ring sensor (32 Hz, ring-type sensor)
- **Features**: Area under curve, number of peaks, time to peak, recovery time, peak amplitude

---

## Dataset Statistics

### Participants
- **Total**: 120 participants (75 male, 45 female)
- **Age**: Mean = 28 years (SD = 7.5)
- **Distribution**: 60 participants per site, 40 per visualization type

### Trials
- **Total Trials**: 14,400 (120 participants × 120 trials)
- **Per Visualization**: 4,800 trials each (Graph, Timeline, Distribution)
- **Condition Distribution**: Balanced 2×2×2 design (Question × Stimulus × Adaptation)

### Data Quality
- **EEG**: Impedances < 10 kΩ (gel-based), quality-checked (dry-electrode)
- **Eye Tracking**: Calibration error minimized, continuous quality monitoring
- **EDA**: Cleaned and artifact-corrected

---

## Getting Started

### Prerequisites

- **Python 3.8 or higher**
- **Required Libraries**:
  ```bash
  pip install numpy pandas scipy matplotlib seaborn
  pip install mne scikit-learn
  pip install h5py pyedflib
  ```

### Data Access

> **Important**: This repository contains processed data and features that are under 100 MB. Raw continuous recordings and large unprocessed files (>100 MB) have been **omitted from this repository** due to GitHub file size limitations.

**Available in this repository**:
- Epoched/preprocessed EEG data
- Extracted features from all modalities (EEG, ET, EDA)
- Behavioral data and trial annotations
- Baseline model code and analysis scripts
- Participant metadata

**Files omitted (>100 MB)**:
- Full continuous raw EEG recordings
- Complete unprocessed eye tracking streams
- Large HDF5/archive files

**Need access to omitted files?** Please contact the authors directly:
- Email: sebastian.idesis@gmail.com
- Provide details about which files you need and your intended use case

1. **Clone this repository**:
   ```bash
   git clone https://github.com/[your-username]/perceiv.git
   cd perceiv
   ```

2. **Verify data integrity**:
   ```bash
   # Check file structure
   python scripts/verify_dataset.py
   ```

### Quick Start Example

```python
import pandas as pd
import numpy as np
import mne

# Load behavioral data
behavior_df = pd.read_csv('Graph/behavioral_data.csv')

# Load preprocessed EEG epochs
epochs = mne.read_epochs('Graph/Graph_EEG/participant_001_epo.fif')

# Load eye tracking features
et_features = pd.read_csv('Graph/Graph_ET/features/participant_001_features.csv')

# Load EDA features
eda_features = pd.read_csv('Graph/Graph_EDA/features/participant_001_features.csv')

# Analyze by condition
easy_trials = behavior_df[behavior_df['condition'] == 'Easy']
hard_trials = behavior_df[behavior_df['condition'] == 'Hard']

print(f"Easy trials accuracy: {easy_trials['accuracy'].mean():.2%}")
print(f"Hard trials accuracy: {hard_trials['accuracy'].mean():.2%}")
```

---

## Data Formats

### Behavioral Data
- **Format**: CSV files with trial-level annotations
- **Columns**: participant_id, trial_number, visualization_type, question_difficulty, stimulus_complexity, adaptation, accuracy, reaction_time, timestamp

### EEG Data
- **Raw Format**: `.fif` (MNE-Python) or `.edf` (European Data Format)
- **Epoched Format**: `.fif` epochs (-0.5 to 3.0 s around stimulus onset)
- **Features**: CSV files with extracted features per trial

### Eye Tracking Data
- **Raw Format**: CSV files with timestamp, gaze_x, gaze_y, pupil_size, validity
- **Processed Format**: CSV files with fixation events and saccade events
- **Features**: CSV files with trial-level aggregated metrics

### EDA Data
- **Raw Format**: CSV files with timestamp and conductance values
- **Processed Format**: CSV files with peak-detected events
- **Features**: CSV files with trial-level summary statistics

---

## Baseline Analysis & Models

### Classification Performance

Using subject-grouped cross-validation (5-fold):

| Modality | Best Classifier | Accuracy | Features |
|----------|----------------|----------|----------|
| **Behavior (RT + Accuracy)** | Linear SVM | 80-85% | 2 |
| **All Physiological (EEG+ET+EDA)** | Random Forest | 75-85% | ~20 |
| **Eye Tracking** | Linear SVM | ~80% | 5 |
| **EEG** | Gradient Boosting | 60-66% | 6 |
| **EDA** | Linear SVM | 60-70% | 5 |

### Feature Importance

**Top EEG Features**:
1. Spectral entropy (frontal)
2. Theta power (frontal ROI)
3. Amplitude entropy

**Top Eye Tracking Features**:
1. Fixation amount
2. Fixation duration
3. Saliency entropy

**Top EDA Features**:
1. Peak amplitude
2. Time to peak
3. Area under curve

---

## Use Cases & Applications

### 1. Adaptive Visualization Systems
Use the dataset to train models that predict cognitive load in real-time and trigger adaptive interface changes (e.g., simplifying visualizations, adjusting encoding strategies).

### 2. Visual Attention Modeling
Develop computational models of goal-directed attention in InfoVis tasks using synchronized gaze and task data.

### 3. Cognitive Fit Theory Validation
Test hypotheses about alignment between visualization formats and task demands using multimodal cognitive indicators.

### 4. Cross-Modal Fusion Research
Investigate optimal strategies for combining EEG, eye tracking, and EDA signals for cognitive state estimation.

### 5. Benchmarking ML Models
Establish baseline performance for new cognitive load classification algorithms using standardized data splits.

---

## Citation

If you use the PERCEIV dataset in your research, please cite:

```bibtex
@article{idesis2026perceiv,
  title={PERCEIV: A Multimodal Physiological Dataset of Visual Encodings for Adaptive InfoVis Interfaces},
  author={Idesis, Sebastian and Bruns, Mireia Masias and Cardona, Angela Lopez and Emami, Parvin and Duraisamy, Saravanakumar and Leiva, Luis A and Arapakis, Ioannis},
  journal={IEEE Transactions on Visualization and Computer Graphics},
  year={2026},
  publisher={IEEE}
}
```

### Related Publications

**Context-Aware Adaptive Visualizations** (ECAI 2025):
```bibtex
@inproceedings{LopezCardona2025ContextAware,
  author    = {Angela Lopez-Cardona and Mireia Masias Bruns and Nuwan T. Attygalle and
               Sebastian Idesis and Matteo Salvatori and Konstantinos Raftopoulos and
               Konstantinos Oikonomou and Saravanakumar Duraisamy and Parvin Emami and
               Nacera Latreche and Alaa Eddine Anis Sahraoui and Michalis Vakalellis and
               Jean Vanderdonckt and Ioannis Arapakis and Luis A. Leiva},
  title     = {Context-aware Adaptive Visualizations for Critical Decision Making},
  booktitle = {Proceedings of the 27th European Conference on Artificial Intelligence},
  year      = {2025},
  note      = {Demo paper}
}
```

---

## Ethical Considerations

### Data Collection
- **Ethical Approval**: Study protocol approved by institutional review board
- **Informed Consent**: All participants provided written informed consent
- **Compensation**: Participants received $30 for ~1 hour of participation

### Privacy & Anonymization
- **De-identification**: All personally identifiable information removed
- **Participant IDs**: Anonymous numeric identifiers only
- **Storage**: Secure storage with access controls during collection
- **Sharing**: Only anonymized data released publicly

### Inclusion Criteria
- Normal or corrected-to-normal vision
- No history of neurological or psychiatric disorders
- No medication affecting cognitive performance

---

## License

This dataset is released under the **MIT License**.

```
MIT License

Copyright (c) 2026 PERCEIV Dataset Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## Contributors

### Core Team
- **Sebastian Idesis** - Telefonica Research, Barcelona, Spain (sebastian.idesis@gmail.com)
- **Mireia Masias Bruns** - Telefonica Research, Barcelona, Spain
- **Angela Lopez Cardona** - Telefonica Research, Barcelona, Spain
- **Parvin Emami** - University of Luxembourg, Luxembourg
- **Saravanakumar Duraisamy** - University of Luxembourg, Luxembourg
- **Luis A. Leiva** - University of Luxembourg, Luxembourg
- **Ioannis Arapakis** - Telefonica Research, Barcelona, Spain

### Institutions
- **Telefonica Research** - Barcelona, Spain
- **University of Luxembourg** - Esch-sur-Alzette, Luxembourg

---

## Acknowledgments

This work is part of the SYMBIOTIK project, exploring symbiosis-inspired Human-AI frameworks for adaptive information visualization. We thank all participants who contributed their time and data to this research.

---

## Contact

For questions, issues, or collaborations:

- **Email**: sebastian.idesis@gmail.com
- **Issues**: [GitHub Issues](https://github.com/[your-username]/perceiv/issues)
- **Discussions**: [GitHub Discussions](https://github.com/[your-username]/perceiv/discussions)

---

## Changelog

### Version 1.0.0 (2026-08-24)
- Initial public release
- 120 participants across 3 visualization types
- 14,400 total trials with multimodal recordings
- Preprocessed derivatives and baseline models included
- Complete documentation and code examples

---

## Roadmap

- [ ] Add deep learning baseline models (CNN, RNN, Transformers)
- [ ] Include scanpath analysis tools
- [ ] Provide Jupyter notebook tutorials
- [ ] Add visualization of cognitive load dynamics
- [ ] Create interactive dataset explorer
- [ ] Expand to additional visualization types

---

**Last Updated**: August 24, 2026
