# Road Object Detection Under Adverse Weather Conditions

## Problem

Reliable road-object detection is difficult in adverse weather. Fog, snow, rain, and reduced visibility can obscure objects, reduce image quality, and cause standard computer-vision systems to miss or misclassify road users. These failures are especially important for traffic monitoring and intelligent-transportation applications, where detecting people, bicycles, cars, motorcycles, buses, and trucks consistently is essential for safety and decision-making.

## Solution

This project develops and evaluates YOLOv8-based object-detection models on the DAWN adverse-weather dataset. The workflow includes:

- Preparing dataset metadata and train/validation/test splits.
- Training and comparing YOLOv8n, YOLOv8s, and YOLOv8m models.
- Evaluating precision, recall, F1 score, mAP@50, and mAP@50-95.
- Performing model ranking and error analysis across object classes and weather conditions.
- Selecting the model with the strongest overall test performance.

YOLOv8s was selected as the final model because it achieved the highest test mAP@50-95:

| Metric | YOLOv8s |
|---|---:|
| Precision | 0.8728 |
| Recall | 0.5843 |
| F1 score | 0.7000 |
| mAP@50 | 0.6927 |
| mAP@50-95 | 0.4253 |

The model detects six road-object classes: **Person, Bicycle, Car, Motorcycle, Bus, and Truck**.

## Impact

Compared with the YOLOv8n baseline, the selected YOLOv8s model improved:

- Precision by **4.49 percentage points**.
- Recall by **8.34 percentage points**.
- F1 score by **7.58 percentage points**.
- mAP@50 by **10.83 percentage points**.
- mAP@50-95 by **7.00 percentage points**.

These results demonstrate that systematic model comparison can improve detection quality in challenging weather conditions. The project also identifies where further work is needed: **fog** was the hardest observed weather condition, while **bicycle** was the weakest-performing object class. The trained models, evaluation outputs, error-analysis files, and notebook are included in this repository for reproducibility and future improvement.

## Background / Motivation

Autonomous and intelligent transportation systems must detect road users despite changes in visibility and weather. Models trained only on clear-weather images may perform poorly when objects are partially hidden, low contrast, or affected by fog, rain, snow, or sandstorms. This project investigates whether a YOLOv8 detector can provide useful and measurable performance on adverse-weather road scenes.

## Dataset

The project uses the **DAWN** adverse-weather road-object dataset. The dataset metadata defines separate training, validation, and test splits and six object classes:

1. Person
2. Bicycle
3. Car
4. Motorcycle
5. Bus
6. Truck

The repository contains the dataset configuration and split metadata. The original image dataset is not redistributed here; configure its local path before reproducing the experiments.

## Repository Structure

```text
.
├── Road_Object_Detection_Adverse_Weather.ipynb
├── Road Object Detection Report.docx.pdf
├── dataset_metadata-20261017T131113Z-1-001/
│   └── dataset_metadata/
│       ├── data.yaml
│       ├── train_split.csv
│       ├── val_split.csv
│       └── test_split.csv
├── training_runs-20261017T131121Z-1-001/
│   └── training_runs/
│       ├── YOLOv8n_*/
│       ├── YOLOv8s_*/
│       └── YOLOv8m_*/
└── final_results-20261017T131115Z-1-001/
    └── final_results/
        ├── error_analysis/
        ├── final_summary/
        └── visual_evaluation/
```

The notebook contains the analysis and experiment workflow. The training-runs directory contains model checkpoints and run artifacts, while the final-results directory contains evaluation summaries, error analysis, and visual examples.

## Method

The workflow is:

1. Prepare the DAWN metadata and configure the YOLO dataset paths.
2. Train YOLOv8n, YOLOv8s, and YOLOv8m models.
3. Evaluate the models on validation and test data.
4. Evaluate performance by weather condition and inspect difficult and successful detections.
5. Compare model metrics and select the model with the highest test mAP@50-95.

The final selection favors overall localization and classification quality rather than model size alone. YOLOv8s was selected over YOLOv8n and YOLOv8m using this criterion.

## Metrics

- **Precision:** the proportion of predicted detections that are correct.
- **Recall:** the proportion of ground-truth objects that are detected.
- **F1 score:** the harmonic mean of precision and recall.
- **mAP@50:** mean average precision at an IoU threshold of 0.50.
- **mAP@50-95:** mean average precision averaged across IoU thresholds from 0.50 to 0.95; this is the primary model-selection metric in this project.

## Results

The final test comparison was:

| Model | Precision | Recall | F1 | mAP@50 | mAP@50-95 |
|---|---:|---:|---:|---:|---:|
| YOLOv8s | 0.8728 | 0.5843 | 0.7000 | 0.6927 | 0.4253 |
| YOLOv8m | 0.7242 | 0.6146 | 0.6649 | 0.6446 | 0.4069 |
| YOLOv8n | 0.8279 | 0.5009 | 0.6242 | 0.5844 | 0.3552 |

YOLOv8s achieved the highest overall test mAP@50-95. The analysis identified **Car** as the strongest class, **Bicycle** as the weakest class, **Snow** as the best observed weather condition, and **Fog** as the hardest observed weather condition.

## How to Reproduce

1. Clone this repository and install the dependencies used by the notebook, including Python, Jupyter, and the Ultralytics YOLO package.
2. Obtain the DAWN dataset separately and arrange its images and labels according to the paths expected by `data.yaml`.
3. Update the dataset path in `dataset_metadata-20261017T131113Z-1-001/dataset_metadata/data.yaml` and any corresponding notebook path variables.
4. Open `Road_Object_Detection_Adverse_Weather.ipynb`.
5. Run the notebook from top to bottom to prepare metadata, train the models, evaluate the splits, and generate results.
6. Compare the generated metrics with the saved files in `final_results-20261017T131115Z-1-001/final_results/`.

The included checkpoints and result artifacts allow the reported analysis to be inspected without repeating every training run.

## Authors, Course, and License

- **Author:** `arifinalak`
- **Course:** CSE437
- **License:** No license file is currently included in this repository. Unless a license is added, the project should be treated as having all rights reserved.