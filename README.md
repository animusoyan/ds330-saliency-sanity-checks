# DS330 Saliency Map Sanity Checks

This project compares how Grad-CAM and Guided Backpropagation change when we progressively reset the weights of a pretrained ResNet-18.

## Reproduce the pilot

1. Download `experiment.ipynb` from this repository and open it in Google Colab.
2. Check that `SEEDS = [42, 44, 46]` in the first code cell.
3. Click **Run all**. When Colab asks for files, upload the four pilot images from this repository together: the dog, bicycle, bald eagle, and bananas.
4. Check that the notebook prints `Saved 72 rows to saliency_results.csv.` You can download the CSV from Colab’s **Files** panel.

## Pilot results

`saliency_results.csv` contains the saved pilot run: four images, three seeds, and six cumulative reset stages. Blank Grad-CAM values mean the rank correlation was undefined because a map was constant.

## Main 40-image run & ablation

To reproduce the full dataset run, download the 40 images listed in `image_sources.csv`, set the Section 3 output filename to `main_results.csv`, and run all cells in `experiment.ipynb`:

- `image_sources.csv`: Filenames, categories (8 balanced classes, 5 images each), and Wikimedia Commons URLs for the 40-image dataset.
- `main_results.csv`: Cascading randomization results across all 40 images, 3 seeds (`42, 44, 46`), and 6 cumulative reset stages (720 rows).
- `independent_reset_results.csv`: Independent reset ablation comparing `only_fc` vs. `only_stem` (`conv1` + `bn1`) starting from the pretrained ResNet-18 (240 rows).
- `fig1_cascade_similarity.png`: Median Spearman correlation and middle-50% (IQR) spread across the six cumulative reset stages with valid Grad-CAM counts.
- `fig2_qualitative_comparison.png`: Visual comparison of Grad-CAM and Guided Backpropagation across Pretrained, Classifier Reset (`fc`), and Full Reset (`+ stem`).
