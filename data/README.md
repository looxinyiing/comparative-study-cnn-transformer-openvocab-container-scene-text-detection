# Datasets

Three datasets are used. None is redistributed in this repository. The
licence and origin of each is given below so that a third party can
reproduce the experiments.

## 1. Container number detection (Roboflow Universe)

- **Source:** <https://universe.roboflow.com/dissertation-t3buk/container-number-detection>
- **Version used:** v3
- **Size:** 1001 images, single class `container-number`
- **Licence:** CC BY 4.0
- **How to obtain:** notebook `00_setup_and_smoke_test.ipynb` downloads it
  with the Roboflow Python SDK. You need a free Roboflow account and must
  set `ROBOFLOW_API_KEY` as a Kaggle notebook secret (or an environment
  variable when running locally).

The repository split is 70 / 20 / 10 (train / val / test), produced from
the Roboflow download by `_split_container` in notebook 00.

## 2. ICDAR 2015 Robust Reading Competition, Task 4.1

- **Source:** <https://rrc.cvc.uab.es/?ch=4&com=downloads>
- **Files used:**
  - `ch4_training_images.zip`
  - `ch4_training_localization_transcription_gt.zip`
  - `ch4_test_images.zip`
  - `Challenge4_Test_Task1_GT.zip`
- **Licence:** available for research use only; redistribution is not
  permitted. You must download the four files yourself after accepting
  the competition's terms.
- **How to use here:** package the four zip files as a Kaggle dataset
  named `icdar2015-task41-raw` under your own account and attach it as
  an input to the notebook. Notebook 00 contains an
  `_find_icdar_mount` helper that locates the dataset wherever Kaggle
  mounted it.

## 3. COCO 2017 val (reference check only)

- **Source:** <https://cocodataset.org/#download> (`val2017.zip`,
  `annotations_trainval2017.zip`).
- **Licence:** CC BY 4.0 for the annotations, Flickr terms for the
  images.
- **How to use here:** attach the public Kaggle dataset
  `jessicali9530/coco2017` to the notebook, or follow the local-path
  instructions in notebook `04_coco_reference.ipynb`.

COCO is used only to validate that the pretrained checkpoints we use
reach the published reference accuracy on their training domain, so the
pipeline is set up correctly. No COCO training is performed.
