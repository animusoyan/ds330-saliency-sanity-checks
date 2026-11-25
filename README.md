# DS330 Saliency Map Sanity Checks

This project compares how Grad-CAM and Guided Backpropagation change when we progressively reset the weights of a pretrained ResNet-18.

## Reproduce the pilot

1. Download `experiment.ipynb` from this repository and open it in Google Colab.
2. Check that `SEEDS = [42, 44, 46]` in the first code cell.
3. Click **Run all**. When Colab asks for files, upload the four pilot images from this repository together: the dog, bicycle, bald eagle, and bananas.
4. Check that the notebook prints `Saved 72 rows to saliency_results.csv.` You can download the CSV from Colab’s **Files** panel.

## Pilot results

`saliency_results.csv` contains the saved pilot run: four images, three seeds, and six cumulative reset stages. Blank Grad-CAM values mean the rank correlation was undefined because a map was constant.

## Next step

Reproduce this pilot, then run the notebook on a larger image set. Save the larger run under a different CSV filename so we can keep both results.
