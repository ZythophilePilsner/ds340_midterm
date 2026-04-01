# DS340 Midterm Project

This repository contains the code for a DS340 midterm project on music genre classification. The main workflow trains a paper-style CNN on GTZAN MFCC features and optionally evaluates the same model on locally stored AI-generated music.

## Repository Contents

- `demo_3.ipynb`: end-to-end notebook covering preprocessing, MFCC extraction, CNN training, GTZAN evaluation, and optional AI music evaluation
- `midterm_progress.py`: script version of the core GTZAN plus AI-evaluation workflow
- `load_data.ipynb`: notebook for loading or organizing the local Suno dataset batches
- `demo_1.ipynb`, `demo_2.ipynb`, `trial_1.ipynb`: earlier exploratory notebooks
- `requirements.txt`: Python dependencies for the notebooks and scripts

## Public Upload Note

`demo_3.ipynb` is included in a public-safe form:

- stored without cell outputs or execution counts
- cleaned of hardcoded personal filesystem paths
- configured to use repository-local `data/` and `artifacts/` folders
- trimmed to avoid keeping unnecessary AI metadata fields such as prompts and track titles in notebook-generated artifacts

## Project Workflow

1. Load one GTZAN example track and walk through waveform, rectification, smoothing, FFT, STFT, spectrogram, and MFCC views.
2. Build MFCC segment datasets from the local GTZAN audio folders.
3. Train the CNN used in the paper replication.
4. Evaluate the trained model on a GTZAN test split.
5. Optionally map local Suno tags into the GTZAN label space and evaluate the same model on AI-generated tracks.

## Expected Local Data

Large datasets are not included in the repository.

The code expects:

- `data/genres_original`
- `data/suno-audio` for the optional AI-evaluation section

Generated outputs are written to `artifacts/demo_3` and are ignored by git.

## Setup

Create and activate a virtual environment, then install dependencies:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Working With `demo_3.ipynb`

Launch Jupyter and open the notebook:

```bash
jupyter notebook demo_3.ipynb
```

The notebook assumes the local dataset folders above already exist. If `data/suno-audio` is missing, the AI-evaluation section is skipped automatically.

## Running The Script

GTZAN-only run:

```bash
python midterm_progress.py --skip-ai-eval
```

Full GTZAN plus AI evaluation:

```bash
python midterm_progress.py --rebuild-gtzan-json --rebuild-ai-features --retrain-model
```

## Notes

- The GTZAN model uses MFCC segments as inputs to a CNN that follows the paper replication structure.
- The AI-evaluation extension uses heuristic tag mapping because the Suno dataset does not ship with GTZAN-style labels.
