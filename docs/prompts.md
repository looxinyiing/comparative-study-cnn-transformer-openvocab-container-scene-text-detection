# Prompt sets used in zero-shot evaluation

Eight prompts for the container dataset and four for ICDAR 2015 are
swept in notebooks 02 and 03 respectively. The full lists are reproduced
here so that the sweeps can be reproduced without reading the code.

## Container prompts (notebook 02)

The prompt string is passed to YOLO-World's `set_classes` method. One
class per sweep run.

1. `container number`
2. `shipping container code`
3. `ISO 6346 container code`
4. `container identification code`
5. `white text on a shipping container`
6. `printed text on the side of a container`
7. `alphanumeric code on a cargo container`
8. `BIC code on a container`

Each prompt is evaluated at a fixed confidence threshold on the held-out
test split. Precision, recall and mAP are recorded in
`results/container_prompt_sweep.csv`.

## ICDAR 2015 prompts (notebook 03)

1. `text`
2. `word`
3. `scene text`
4. `printed text`

Numbers in `results/icdar_prompt_sweep.csv`.
