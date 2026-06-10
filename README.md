# MEDS Pooling System

**Math Education Digital Shadows (MEDS)** — Data Pooling Dashboard.  
CogNosco Lab, University of Trento.

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](TODO_COLAB_NOTEBOOK_URL)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/)
[![Dataset](https://img.shields.io/badge/dataset-MEDS-blue.svg)](TODO_DATA_RELEASE_URL)
[![Manuscript](https://img.shields.io/badge/manuscript-MEDS-orange.svg)](TODO_PREPRINT_OR_DOI_URL)

<p align="center">
  <img src="assets/logofis.png" alt="FIS logo" height="180">
  <img src="assets/MEDS_Logo.png" alt="MEDS logo" height="180">
</p>

**MEDS Pooling System** is an interactive dashboard for the *Math Education Digital Shadows (MEDS)* dataset. MEDS contains 28,000 LLM-generated digital shadows produced across 14 large language models under two prompting conditions: human-simulated personas and baseline AI-assistant responses. Each digital shadow links mathematical problem solving to confidence, psychometric scales, persona metadata, free-text explanations, and graph-based semantic association data.

The dashboard lets researchers filter personas by model, mode, demographic profile, educational background, psychological attributes, and task-specific outputs. Users can then inspect each selected persona's topic answers, math-anxiety and self-efficacy scales, behavioral forma mentis networks, quiz answers, confidence scores, and reasoning traces. Filtered subsets can be exported for downstream statistical, linguistic, psychological, and network-science analyses.

The MEDS Pooling System was created by **Navid Aghazadeh Ardebili**, **Anthony Tricarico**, **Luisa Porzio** and **Naomi Esposito**, based on code developed together with **Rodolfo Rizzi**. Scientific supervision and dataset coordination were provided by *prof. Massimo Stella* within **CogNosco Lab**.

<p align="center">
  <img src="assets/MEDS-pooling-system.png" alt="MEDS Pooling System dashboard" width="900">
</p>

<p align="center"><em>Filters on the left; matching personas, selected persona metadata, and task answers on the right.</em></p>

## What the dashboard provides

The pooling system is designed for researchers from multiple disciplinary backgrounds.

- **Social scientists** can retrieve persona-level profiles stratified by age, gender, education, employment, migration status, religious beliefs, hobbies, and subject preferences.
- **Psychologists and education researchers** can compare math anxiety, math self-efficacy, confidence, and problem-solving performance across simulated humans and AI assistants.
- **Linguists and NLP researchers** can access open-ended explanations, reasoning summaries, and generated justifications.
- **Network scientists and AI researchers** can extract behavioral forma mentis networks built from cue-word associations and valence labels.

The goal is not to replace the raw MEDS files, but to make them easier to explore, subset, visualise, and reuse.

## Quick start (Colab)

Click the **Open in Colab** badge above, then run the two cells in order. The first run downloads the MEDS dashboard data file; subsequent runs in the same session use the local cache.

```python
# Cell 1
!pip install --upgrade pandas panel git+TODO_GITHUB_REPOSITORY_URL --quiet

# Cell 2
import meds_pooling as meds
meds.launch_dashboard()
```

## Quick start (local installation)

Run the dashboard on your machine inside an isolated virtual environment.

**1. Create the virtual environment**  
Requires a Python ≥3.11 interpreter.

```bash
python -m venv .venv_meds
```

**2. Activate the environment**

Windows PowerShell:

```powershell
.venv_meds\Scripts\Activate.ps1
```

macOS / Linux:

```bash
source .venv_meds/bin/activate
```

**3. Install the package**

```bash
pip install git+TODO_GITHUB_REPOSITORY_URL
```

**4. Launch the dashboard**

```bash
python -c "import meds_pooling as meds; meds.launch_dashboard()"
```

A browser tab will open automatically. On first launch, the data file is downloaded and cached locally.

## Persistent caching on Colab (optional)

By default, Colab caches the data file only for the current runtime. To persist the cache across sessions, mount Google Drive and point the dashboard to a Drive folder:

```python
from google.colab import drive
drive.mount('/content/drive')

import meds_pooling as meds
meds.launch_dashboard(cache_dir='/content/drive/MyDrive/MEDS-pooling/')
```

## Programmatic API

```python
import meds_pooling as meds

df = meds.load_pool()                             # merged MEDS dashboard table
hits = meds.search_personas(
    df,
    model="Qwen3.5 9B",
    mode="human",
    city="Chicago",
    sexual_orientation="asexual"
)

meds.launch_dashboard(df=hits)                   # dashboard over filtered subset
```

Typical exported functions include:

```text
launch_dashboard
load_pool
search_personas
DATA_VERSION
SOCIO_COLS
TASK_OPTIONS
TOPIC_QUESTIONS
SCALE_ITEMS
FORMA_MENTIS_CUES
QUIZ_ITEMS
FILTER_GROUPS
VIEW_MODES
__version__
```

Function names may vary slightly across releases; inspect the package with `dir(meds_pooling)` if needed.

## Data

The dashboard uses a merged persona-level table derived from the MEDS task files.

- **Dataset:** Math Education Digital Shadows (MEDS).
- **Size:** 28,000 digital shadows.
- **Models:** 14 large language models.
- **Modes:** human-simulated personas and baseline LLM/AI-assistant responses.
- **Core tasks:** topic answers, psychometric scales, behavioral forma mentis networks, and math problem solving.
- **Psychometric instruments:** MSES, AMAS, MSEAQ, and MSES-R problem-solving items.
- **Graph data:** cue-word associations and valence labels for behavioral forma mentis network construction.
- **Primary identifiers:** release-dependent, typically including `run_id`, `model`, and `mode`.
- **Data file:** not stored directly in git; distributed through the repository release page or the official MEDS data archive.
- **Recommended use:** academic, non-commercial research and reproducible analysis.

The raw MEDS release contains task-level JSON records. The pooling system provides a pre-merged table for interactive exploration and export. Always cite the MEDS manuscript and the dashboard repository when using the data.

## Repository structure

```text
MEDS-pooling-system/
├── assets/
│   ├── MEDS-pooling-system.png
│   ├── MEDS_Logo.png
│   └── logofis.png
├── notebooks/
│   └── colab_MEDS_pooling_system_dashboard.ipynb
├── src/
│   └── meds_pooling/
├── LICENSE
└── README.md
```

## License

- **Code:** MIT License — see [`LICENSE`](LICENSE).
- **Data:** MEDS is shared for academic, non-commercial research under the terms specified in the corresponding data release. Please cite the MEDS manuscript if you use the data, the dashboard, or any exported subset.

## Citation

If you use the MEDS dataset or this pooling system in academic work, please cite the accompanying manuscript:

> Esposito, N., Tricarico, A., Porzio, L., Aghazadeh Ardebili, A., & Stella, M. (2026).  
> *Math Education Digital Shadows for facilitating learning with LLMs: Math performance, anxiety and confidence in simulated students and AIs.*  
> Manuscript submitted for publication.

If you use the dashboard code, please also cite or acknowledge:

> Aghazadeh Ardebili, N., Rizzi, R., & Stella, M. (2026).  
> *MEDS Pooling System: An interactive dashboard for Math Education Digital Shadows.*  
> CogNosco Lab, University of Trento.

## Credits

The MEDS Pooling System was created by **Navid Aghazadeh Ardebili** based on code developed together with **Rodolfo Rizzi**.

MEDS was developed within **CogNosco Lab**, Department of Psychology and Cognitive Science, University of Trento.

## Contact

Corresponding author: **Massimo Stella** — [massimo.stella-1@unitn.it](mailto:massimo.stella-1@unitn.it)  
CogNosco Lab, Department of Psychology and Cognitive Science, University of Trento, Italy.

For technical questions about the pooling system, please contact the dashboard maintainers or open an issue in the repository.

---
