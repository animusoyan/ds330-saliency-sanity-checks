# DS330 Saliency Map Sanity Checks

This project compares how Grad-CAM and Guided Backpropagation respond when we reset the weights of a pretrained ResNet-18. For each photo, we keep the pretrained model’s top predicted class fixed and use Spearman rank correlation to compare each reset model’s saliency map with the corresponding pretrained map.

We test 40 photos with three random seeds. The main experiment progressively resets the model from the final classifier back to the stem. A second experiment resets the classifier and stem separately, starting from the pretrained model each time.

## Reproduce the experiment in Colab

1. Extract `images.zip`. The `images` folder contains the 40 JPGs used in the experiment. [`image_sources.csv`](image_sources.csv) lists their categories and sources.
2. Open [`experiment.ipynb`](experiment.ipynb) in Google Colab. The default CPU runtime is sufficient.
3. Check that `SEEDS = [42, 44, 46]` in the setup cell and click **Run all**.
4. When prompted, select all 40 JPGs inside the extracted `images` folder.
5. After the run finishes, open Colab’s **Files** panel to download the two result CSVs and four figures.

To regenerate just Figures 3 and 4, upload the two saved CSVs to Colab’s **Files** panel and run the last two plotting cells in order.

## Outputs

| File | Contents |
|---|---|
| [`main_results.csv`](main_results.csv) | 720 rows from 40 photos, three seeds, and six cumulative reset stages. |
| [`independent_reset_results.csv`](independent_reset_results.csv) | 240 rows comparing classifier-only and stem-only resets. |
| [`fig1_cascade_similarity.png`](fig1_cascade_similarity.png) | Median similarity and the middle 50% of photo-level results at each cumulative reset stage, after averaging valid seed scores per photo. |
| [`fig2_qualitative_comparison.png`](fig2_qualitative_comparison.png) | Model input crops and saliency maps for two photos under the pretrained, classifier-only reset, and full-reset conditions. Each saliency map uses its own color scale. |
| [`fig3_independent_reset_errorbars.png`](fig3_independent_reset_errorbars.png) | Guided Backpropagation similarity after resetting only the classifier or only the stem. Dots show the median and bars show the middle 50% across photos after averaging seeds per photo. |
| [`fig4_classifier_reset_scatter.png`](fig4_classifier_reset_scatter.png) | A photo-by-photo comparison of Grad-CAM and Guided Backpropagation magnitude after the classifier-only reset. Each dot averages the seeds with valid scores for both methods. |

A blank Grad-CAM value means Spearman correlation was undefined because one of the maps was constant. The CSVs retain those rows, and the summaries use the available correlations.

## Earlier pilot

[`saliency_results.csv`](saliency_results.csv) contains the original four-image pilot. The pilot images are the dog, bicycle, bald eagle, and bananas in the repository.
