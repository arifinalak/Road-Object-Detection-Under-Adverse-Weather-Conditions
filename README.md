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