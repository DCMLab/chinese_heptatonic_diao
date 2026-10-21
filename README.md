# *Tong Yun San Gong*: data and code

Data and analysis for **“Revisiting *Tong Yun San Gong* Theory: Corpus Evidence for the Distinctions among Three Chinese Heptatonic *Diao*”**, by Shuxin Meng, Fabian C. Moss and Martin A. Rohrmeier.

## Contents

| File | Purpose |
|---|---|
| `analysis.ipynb` | Corpus summaries, Bayesian mode inference, resampling, and evaluation. |
| `data/corpus.csv` | Metadata and pitch-class profiles for 2,240 Chinese Essen melodies. |
| `data/heptatonic.csv` | Manual annotations and model profiles for 219 heptatonic melodies. |
| [data/README.md](data/README.md) | Field definitions, units, and provenance. |
| `requirements.txt` | Python dependencies. |

The data tables join on the source filename, `name`. Corpus profiles express each score’s declared tonic as C; `source_tonic_pitch_class` records that source tonic. Heptatonic model profiles use a common diatonic reference, C–D–E–F–G–A–B.

The notebook fits three modes to the original annotated corpus, a balanced bootstrap sample, and a balanced Dirichlet sample. It also calculates silhouette scores for 2–21 modes. Calculations begin with the supplied processed tables.

## Annotated heptatonic dataset

**Diao Annotations for Heptatonic Pieces in the Chinese Collection of the Essen Folksong Database** is available on Zenodo: https://zenodo.org/records/14607710.

The dataset is included in this repository as [data/heptatonic.csv](data/heptatonic.csv).

## Run

Use Python 3.9–3.11. From this repository’s folder:

```sh
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
jupyter lab analysis.ipynb
```

Select **Run → Run All Cells**. Results appear in the notebook, with progress messages during model fitting.

The analysis was run with Python 3.9.6, NumPy 1.26.4, pandas 2.2.3,
SciPy 1.10.1, Numba 0.60.0, scikit-learn 1.5.2, and JupyterLab 4.2.5.

## Model attribution

The Bayesian mode implementation adapts
[DCMLab/HistoryModes_DataCode](https://github.com/DCMLab/HistoryModes_DataCode/).
Please cite:

Harasim, D., Moss, F. C., Ramirez, M., & Rohrmeier, M. (2021).
Exploring the foundations of tonality: Statistical cognitive modeling of modes in the history of Western classical music. *Humanities and Social Sciences Communications, 8*, Article 5.
[doi:10.1057/s41599-020-00678-6](https://doi.org/10.1057/s41599-020-00678-6).

## Funding

This project has received funding from the European Research Council (ERC) under the European Union’s Horizon 2020 research and innovation programme under grant agreement No 760081 – PMSB. The authors also thank Claude Latour for supporting this research through the Latour Chair in Digital Musicology at EPFL.

## Licenses

Code, including the adapted mode implementation, is licensed under
[GPLv3](LICENSE_GPL.txt). The manuscript, documentation, and original data
contributions are licensed under [CC BY-NC 4.0](LICENSE_CC.md).
Third-party source-data rights remain with their respective owners.
