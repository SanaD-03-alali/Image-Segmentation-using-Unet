# Bird's-Eye Mapper: Road Segmentation from Satellite Images

## Overview

This project focuses on segmenting roads from satellite images using a UNet model. The goal is to classify each pixel in an image as either a road (1) or background (0). The project employs a combination of original satellite imagery, augmented datasets, and advanced preprocessing techniques to achieve high segmentation accuracy.

---

## Dataset

The dataset comprises:

- **Original Data**: 100 high-resolution images acquired from Google Maps.
- **Generated Data**: Over 1,000 images synthesized using a Pix2Pix GAN model.
- **Augmented Data**: Basic augmentation techniques (e.g., rotation, flipping) and advanced techniques (e.g., random brightness and contrast adjustments).

---

## Model

The model used is a pretrained UNet architecture from `segmentation_models_pytorch`. It is fine-tuned to handle the dataset’s specific characteristics and improve segmentation performance over multiple trials.

---

## Trials

### Trial Descriptions

| Trial | Description |
|-------|-------------|
| **Trial 1** | Baseline training using only the original dataset (100 images). |
| **Trial 2** | Training with the original dataset combined with Pix2Pix-generated images (1,100+ images). |
| **Trial 3** | Incorporating basic augmentation (e.g., rotation, flipping) into the dataset. |
| **Trial 4** | Increasing the number of epochs to assess performance improvement with extended training. |
| **Trial 5** | Applying advanced augmentation techniques, including:  
  - **Elastic Transformations**: Random distortions mimicking terrain or lens effects, enhancing robustness to irregular road shapes.  
  - **Shadow/Cloud Overlays**: Simulated shadows or clouds as semi-transparent layers to improve generalization for real-world conditions. 

---

### Results

| Trial | Image Size | Batch Size | Epochs | Test F1 Score | Train Loss | Validation Loss | Learning Rate |
|-------|------------|------------|--------|---------------|------------|-----------------|---------------|
| **Trial 1** (Original data, 100 images) | 416x416 | 4  | 15 | 0.96  | 0.1035 | 0.1962 | 0.0001 |
| **Trial 2** (Original + Generated, 1,100+) | 416x416 | 32 | 10 | 0.982 | 0.0459 | 0.0455 | 0.0001 |
| **Trial 3** (Basic Augmentation)         | 416x416 | 32 | 10 | 0.932 | 0.3047 | 0.3102 | 0.0001 |
| **Trial 4** (Increased Epochs)           | 416x416 | 32 | 20 | 0.979 | 0.0854 | 0.1214 | 0.0001 |
| **Trial 5** (Advanced Augmentation)      | 416x416 | 32 | 20 | 0.992 | 0.1300 | 0.2249 | 0.0001 |

---

### Observations

- **Trial 1**: Served as a baseline with moderate performance, indicating potential for improvement.
- **Trial 2**: Leveraging the generated dataset significantly boosted F1 score and reduced both train and validation losses.
- **Trial 3**: Basic augmentations slightly reduced performance, possibly due to insufficient diversity in the augmentations.
- **Trial 4**: Increasing epochs improved performance, achieving an F1 score close to Trial 2 but with slightly higher losses.
- **Trial 5**: Advanced augmentations further enhanced performance, achieving the highest F1 score (0.992) while maintaining reasonable train and validation losses.

---

## Files

- **`Image_Segmentation_trial1+2.ipynb`**: Contains code for Trials 1 and 2.
- **`Image_Segmentation_trial3,4,5.ipynb`**: Contains code for Trials 3, 4, and 5.
- **`results_final.xlsx`**: Consolidated results for all trials.
- **`Bird's-Eye Mapper.pdf`**: Contains the paper for our work.
- **`results_final.xlsx`**: Consolidated results for all trials.
- **`Predictions_original_data`**: This folder contains the predictions for trial 1.
- **`Predictions_10epochs_with_generation`**: This folder contains the predictions for trial 2.
- **`Predictions_20epochs_basic`**: This folder contains the predictions for trial 4.
- **`Predictions_20epochs_fullAug`**: This folder contains the predictions for trial 5.
