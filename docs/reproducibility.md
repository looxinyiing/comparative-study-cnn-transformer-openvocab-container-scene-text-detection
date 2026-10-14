# Reproducibility notes

## Environment

The paper's numbers were produced on Kaggle Notebooks with the following
runtime:

- GPU: 1 x NVIDIA T4 (16 GB)
- CUDA: 12.1
- Python: 3.11
- `ultralytics`: 8.3.0
- `torch`: 2.4.0
- Random seed: 0 (single run per model)

For a local re-run, install `requirements.txt` into a fresh Python 3.11
environment and edit the `KAGGLE_WORKING` and dataset-mount paths in the
first configuration cell of each notebook to point to local directories.

## Notebook order

The notebooks are numbered in dependency order:

1. `00_setup_and_smoke_test.ipynb` — downloads the Roboflow container
   dataset, converts the ICDAR 2015 polygon annotations to axis-aligned
   boxes, prepares the YOLO data YAMLs, and runs a one-epoch smoke test
   on all three models to confirm the training loop is wired up.
2. `01_container_supervised.ipynb` — trains YOLOv8-s and RT-DETR-l on
   the container dataset, 100 epochs each.
3. `02_container_openvocab.ipynb` — zero-shot YOLO-World across eight
   container prompts, then fine-tunes YOLO-World on the container data.
4. `03_icdar2015_yolov8_world.ipynb` — YOLOv8-s and YOLO-World on
   ICDAR 2015, both zero-shot (four prompts) and fine-tuned.
5. `04_coco_reference.ipynb` — evaluates the pretrained YOLOv8-s,
   RT-DETR-l and YOLO-World checkpoints on COCO 2017 val, as a pipeline
   sanity check.
6. `05_aggregation.ipynb` — collects per-notebook CSVs into the paper's
   master tables.
7. `06_icdar2015_rtdetr.ipynb` — trains RT-DETR-l on ICDAR 2015; split
   from notebook 03 because of its longer runtime.
8. `07_latency_memory.ipynb` — measures inference latency and GPU memory
   for each architecture at image size 640, batch size 1 on T4.
9. `99_repush_helper.ipynb` — convenience helper for re-pushing a Kaggle
   dataset from a prior notebook output. Not required for a fresh run.

A full fresh run on a T4 takes roughly 7 to 9 hours of GPU time, dominated
by RT-DETR on ICDAR 2015 (around 1.8 hours).

## Known caveats

- All results are from a single random seed. The notebooks expose `SEED`
  as a top-cell constant.
- ICDAR 2015 polygon annotations are converted to axis-aligned bounding
  boxes before training. The axis-aligned box enclosing an oriented
  polygon contains background, so IoU-based metrics on ICDAR are
  depressed relative to polygon-based evaluation. The ranking among
  models is unaffected.
- The container dataset has limited appearance diversity (bodies mostly
  red or brown, text mostly white). Results demonstrate robustness to
  varying capture conditions, not to varying container appearance.
