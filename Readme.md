# Browser ONNX Image Inference

## Project Goal

The main goal of this side project is to perform **object detection of the "Galo de Barcelos" (Rooster of Barcelos) directly in the web browser** using **ONNX models** and **ONNX Runtime Web** - with no server or backend involved at all.

The little app lets anyone:
- Upload an existing image
- Take a quick photo using the webcam (just a snapshot)
- Run inference on that single image
- See bounding boxes and confidence scores drawn right on the image

There is no real-time / continuous video processing planned. The focus is on reliable single-image inference running completely client-side.

### Why "Galo de Barcelos"?
This iconic Portuguese symbol is hand-painted with hugely diverse patterns, colors, shapes and artistic details. That high variability makes it a fun and challenging test case to see how far a compact object detector can generalize to handmade, non-standardized objects when everything runs locally in the browser.

## Main Objective

Providing a seamless, client-side experience for:
- Image acquisition (Upload or Camera).
- Instant object detection and localization.
- On-device processing powered by ONNX Runtime Web.

## Approach

1. Collect and annotate a (currently very small) dataset of "Galo de Barcelos" images
2. Fine-tune **RF-DETR** in two ways:
   - **Frozen backbone** - faster training, much lower memory usage, usually more stable with few examples
   - **Unfrozen / full fine-tuning** I try this when the frozen version clearly isn’t enough
3. Export the best models to **ONNX** (optimized, simplified, dynamic input shapes)
4. Build a clean browser demo (**RF-DETR ONNX - Image Inference**) for single-image detection

## Current Project Status (Very Early Stage)
This is a personal side project and it's still in a very early phase.

The dataset is currently very small.
Because of the limited data, I'm mainly experimenting with frozen backbone fine-tuning, this usually gives more stable results and much less overfitting when you don't have many examples.
The results are not perfect yet (some missed detections, false positives, inconsistent confidence scores, sensitivity to lighting / angle / background) — this is completely expected with such a small dataset.
In this first phase, my goal is simply to get the best results I can squeeze out of the current small dataset, make sure the full pipeline works (train → export → browser inference), and have a working proof-of-concept demo in the browser.

## What Will Be Released

Only the **ONNX models** and the **web inference demo** will be made publicly available in this repository.

I don’t have any plans (for now) to release:
- the dataset
- the annotations
- the training scripts / workflow

The training part is just my personal experimentation to produce decent ONNX files that can run in the browser.

## Model Naming Convention

The model filenames indicate the architecture state and optimization level:
- FR (Frozen): Indicates that the backbone weights were frozen during training.
- INT8: 8-bit Quantization

Example: fr_int8_v01.onnx

[Demo](https://joaosousa1.github.io/Browser-ONNX-Image-Inference/)

