# Fire and Smoke Detection Project Notes

Last updated: 2026-04-25

## Current Project State

- This repository is a small YOLOv8-based fire and smoke detection project.
- The current project is mainly for inference, not training.
- Main files:
  - `YOLOv8LiveCam.py`: live webcam detection with sound and email alerts.
  - `YOLOv8.py`: simple image/video model testing script.
  - `optimized150.pt`: existing trained YOLO model.
  - `alert_sound.mp3`: alert sound used during detection.
  - `requirements.txt`: Python dependencies.
- The loaded model class names are:
  - `0 = fire`
  - `1 = smoke`

## Dataset Decision

- Dataset source:
  - https://universe.roboflow.com/fire-and-smoke-detection-yolo/fire-and-smoke-detection-o4uhv/dataset/4
- Download format to use:
  - `YOLOv8`
- Dataset type:
  - Object detection
- Do not download COCO JSON, Pascal VOC XML, TFRecord, YOLO Darknet, segmentation, or classification formats for this project.

## Recommended Dataset Location

Place the downloaded and extracted dataset here:

```text
datasets/
  fire_smoke_roboflow_v4/
    train/
      images/
      labels/
    valid/
      images/
      labels/
    test/
      images/
      labels/
    data.yaml
```

Do not place dataset images and labels directly in the project root.

## Important Dataset Check

After downloading, check `datasets/fire_smoke_roboflow_v4/data.yaml`.

The class order should match the existing project logic:

```yaml
names:
  - Fire
  - Smoke
```

or:

```yaml
names:
  0: Fire
  1: Smoke
```

The exact capitalization is less important than the order.

## Notebook Conversion Plan

The project should be converted into a notebook-based workflow:

```text
notebooks/
  01_check_project_and_dataset.ipynb
  02_train_yolov8_fire_smoke.ipynb
  03_test_model.ipynb
  04_export_for_jetson.ipynb
  05_run_on_jetson_camera.ipynb
```

## Training Plan

- Do not train on Jetson Nano if a laptop, desktop, or Google Colab is available.
- Train on a stronger machine, then deploy the final model to Jetson Nano.
- Recommended starting model for Jetson Nano:
  - `yolov8n.pt`
- Optional if accuracy is too low and FPS is acceptable:
  - `yolov8s.pt`
- Avoid large YOLO models for Jetson Nano real-time deployment.

## Jetson Nano Deployment Plan

- Use Jetson Nano mainly for inference/deployment.
- Copy only necessary files to Jetson:
  - trained model, for example `best.pt`
  - inference notebook or script
  - `alert_sound.mp3`
  - minimal dependency/install instructions
  - class names/config if needed
- Avoid copying the full training dataset to Jetson unless specifically needed.

## Next User Action

1. Download the Roboflow dataset in `YOLOv8` format.
2. Extract it into `datasets/fire_smoke_roboflow_v4/`.
3. Confirm that `data.yaml` exists.
4. Confirm class order is Fire first, Smoke second.
5. Then continue with notebook creation and training setup.
