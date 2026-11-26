# DS330 Saliency Map Sanity Checks

This project compares how Grad-CAM and Guided Backpropagation respond when we progressively reset the weights of a pretrained ResNet-18. Each image keeps the pretrained model’s top predicted class as its target throughout the experiment.

## Reproduce the 40-image experiment

1. Download [`images.zip`](images.zip) and extract it. The archive contains the exact 40 photos used in the experiment. [`image_sources.csv`](image_sources.csv) lists their categories and sources.
2. Download [`experiment.ipynb`](experiment.ipynb) and open it in Google Colab. The default CPU runtime is sufficient.
3. Check that `SEEDS = [42, 44, 46]` in the setup cell, then click **Run all**.
4. When Colab prompts you, select all 40 image files from the extracted folder.
5. When the run finishes, open Colab’s **Files** panel to download the two CSVs and two figures.

## Outputs

| File | Contents |
|---|---|
| [`main_results.csv`](main_results.csv) | 720 rows from 40 images, three seeds, and six cumulative reset stages. |
| [`independent_reset_results.csv`](independent_reset_results.csv) | 240 rows comparing classifier-only and stem-only resets. Each condition starts from the pretrained model. |
| [`fig1_cascade_similarity.png`](fig1_cascade_similarity.png) | Median Spearman correlations and interquartile ranges across images, after averaging valid correlations across seeds for each image. The figure shows valid Grad-CAM image counts at each stage. |
| [`fig2_qualitative_comparison.png`](fig2_qualitative_comparison.png) | The exact crops passed to ResNet and the corresponding saliency maps for the pretrained, classifier-reset, and fully reset models. Each heatmap uses its own color scale. |

A blank Grad-CAM value means Spearman correlation was undefined because one of the maps was constant. The notebook keeps those rows and summarizes the valid correlations.

## Earlier pilot

[`saliency_results.csv`](saliency_results.csv) contains the original four-image pilot with 72 rows. The pilot images are the dog, bicycle, bald eagle, and bananas stored in this repository.
