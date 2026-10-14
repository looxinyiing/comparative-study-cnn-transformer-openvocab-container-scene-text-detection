# Container Text Detection Benchmark

A reproducible benchmark comparing CNN-based (YOLOv8), Transformer-based
(RT-DETR), and open-vocabulary (YOLO-World) detectors on cargo container
text and ICDAR 2015 scene text, with COCO 2017 as a reference check.

Companion code for the paper:

> X. Y. Loo, S. Yang, X. Dong and W. Huang,
> *A Comparative Study of CNN-Based, Transformer-Based, and Open-Vocabulary
> Detectors for Cargo Container and Scene Text Detection*,
> CCAT 2026, Fukuoka, Japan.

## What is here

- `notebooks/` — nine Jupyter notebooks that reproduce every number and
  figure in the paper. Numbered in the order they should be run.
- `results/` — all evaluation CSVs produced by the notebooks and a small
  set of prediction montages used for sanity checks.
- `paper_assets/` — the final figures and LaTeX tables used in the paper
  (same files, read-only).
- `data/README.md` — how to obtain the three datasets. The datasets
  themselves are not redistributed here.
- `docs/` — reproducibility notes and the full prompt sets used in the
  zero-shot sweeps.
- `configs/` — training and evaluation configuration.

## Quick start

The notebooks were developed on Kaggle Notebooks with one NVIDIA T4 (16 GB)
and are expected to be run there, because the storage and credential paths
assume `/kaggle/working` and `/kaggle/input`. See `docs/reproducibility.md`
for the exact environment and the small changes needed to run them locally.

1. Create a Kaggle notebook, enable GPU T4 x1, and set the following
   notebook secrets under *Add-ons -> Secrets*:
   - `ROBOFLOW_API_KEY` — a free Roboflow account key.
2. Attach the following Kaggle datasets as inputs when needed:
   - `jessicali9530/coco2017` (COCO 2017 val, reference only).
   - Your own Kaggle dataset holding ICDAR 2015 (`icdar2015-task41-raw`
     with the four official zips, see `data/README.md`).
3. Upload the notebooks under `notebooks/` and run them in order.

Local execution is possible but requires editing the Kaggle paths to
local paths. The notebooks skip the Kaggle dataset push step automatically
when the Kaggle CLI is not configured.

## Reproducibility summary

| Item                | Value                              |
|---------------------|------------------------------------|
| GPU                 | NVIDIA T4, 16 GB                   |
| Framework           | Ultralytics `ultralytics` 8.x      |
| Image size          | 640                                |
| Epochs              | 100                                |
| Batch size          | 16 (YOLOv8, YOLO-World) / 8 (RT-DETR) |
| Optimiser           | SGD, Ultralytics default schedule  |
| Seed                | 0                                  |
| Random split        | 70 / 20 / 10 (container), ICDAR 2015 official split |

The CSVs in `results/` are the authoritative numbers.
`paper_assets/table1_main_results.csv` is the paper's Table 1.

## Known limitation

The reported numbers come from a single random seed, which is one of the
limitations the paper acknowledges. The notebooks expose `SEED` as a
single configuration value, so re-running them with different seeds is a
one-line change.

## License

The code is released under the MIT License (see `LICENSE`).
Prediction images under `results/figures/` are derived from the public
datasets and inherit each dataset's own licence (see `data/README.md`).

## Citation

If you use this code, please cite the paper above. A machine-readable
citation is provided in `CITATION.cff`.
