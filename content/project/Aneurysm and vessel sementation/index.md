---
title: The aneurysm and vessel segmentation for 3D digital subtraction angiography images
summary: A deep-learning based medical image processing algorithm.
tags:
  - Deep Learning
date: '2022-04-27T00:00:00Z'

# Optional external URL for project (replaces project detail page).
external_link: ''

authors:
  - Zhenhao Zhao

image:
  caption: 
  focal_point: Smart

# links:
#   - icon: twitter
#     icon_pack: fab
#     name: Follow
#     url: https://twitter.com/georgecushen
url_code: ''
url_pdf: ''
url_slides: ''
url_video: ''

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
# slides: example
---

## Project overview
For this project, the No New U-Net (nnUNet) was used for accurate segmentation of 3D digital subtraction angiography images. The dice coefficient was taken as the evaluation standard, and the accuracy had reached above 90 percent. 

## Model selection
In this experiment, we chose 3D nnUNet for aneurysm segmentation. Compared with the common 3D UNet model, nnUNet has made great innovations in data set preprocessing. And achieved good results in various medical imaging competitions.

## Result
### The segmentation dice accuracy

<div class="table">

|           Model           | Vessel dice on validation set (mean/std) | Aneurysm dice on validation set (mean/std) |
|:-------------------------:|:----------------------------------------:|:------------------------------------------:|
| nnUNet (patch size = 192) |               0.933/0.051                |                0.841/0.206                 |
| nnUNet (patch size = 96)  |               0.934/0.057                |                0.905/0.093                 |

</div>

### Visualize the segmentation
We visualize the segmentation with the Visualization Toolkit (VTK).


The left image is the model predict and the right image is the ground truth.
![Example image](/uploads/images/project_anseg_1.png)
![Example image](/uploads/images/project_anseg_2.png)


