---
title: Camera Vision based Perception for UAS Autonomous Landing
summary: A deep-learning based UAS perception algorithm.
tags:
  - Deep Learning
date: '2022-04-27T00:00:00Z'

# Optional external URL for project (replaces project detail page).
external_link: ''

authors:
  - Zhenhao Zhao
  - Jonathan Lee
  - Zongyao Li
  - Peng Wei

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

The use of small Unmanned Aircraft Systems (UAS) is promising for last-mile package delivery. Commercial small
UASs have become more and more automated in executing a pre-defined flight plan and landing in a well-clear landing
pad. However, to achieve higher level autonomy during an off-nominal landing, a UAS needs to recognize landing scene
reconfiguration such as moving or static obstacles near/on the designated landing pad. These obstacles often include
people, pets, cars, and bikes. We explore the feasibility of using camera vision based perception to (1) identify the
landing pad, and (2) detect the obstacles near or on the landing pad. An accurate, fast and reliable perception module is
a key component for a fully autonomous landing stack, together with a prediction module and planning/control module.
In this project, we focus on implementing and evaluating two state-of-the-art deep learning models for UAS perception,
RetinaNet and YOLOv5. We compare the two models’ object detection accuracy and the computation speed with
real-world landing videos. 

## Methods
### Dataset
We trained the model on the VisDrone2019-Det dataset, which is a public dataset collected by the AISKYEYE
team at the Lab of Machine Learning and Data Mining, Tianjin University, China. The dataset consists of 7,019 static
images taken by various drone platforms collected from 14 cities that are thousands of kilometers away from each other.
Additionally, the dataset covers a broad distribution of locations from urban to rural, with different object densities. This
makes the model trained on this dataset robust and very suitable for this study.


### Model selection
We select YOLOv5 and RetinaNet for this project. In 2017, RetinaNet outperformed YOLOv2 on both the speed (ms) and accuracy (AP) for the COCO test-dev
dataset. But in the current years, the fifth generation of YOLO models was released. It is necessary to compare the two model
types in inference speed and accuracy and select the better model for our algorithms.


### Object tracking using the Kanade-Lucas-Tomasi tracker and landing pad detection
The plan for landing pad detection and tracking is as follows. First, we take a reference photo of the landing pad,
and extract features of the landing pad with the Harris feature detector. Second, we match the features in the video
frame to the reference features by minimizing the SSD (sum of squared difference) to draw the bounding box. Once we
detected the landing pad, we will track it by the Kanade-Lucas-Tomasi (KLT) Tracker for the remaining frames.


Another option is using ArUco markers to detect the landing pad. The ArUco library is based on OpenCV
and enables the detection of various tag dictionaries. ArUco markers are synthetic square markers containing an inner
binary matrix. There are several functions in the OpenCV library that can locate the markers precisely and quickly in
the images and videos. We can put several markers on the landing pad, and draw the landing pad bounding box based on
the location of the markers.


When both the bounding box of the objects and the landing pad are determined, the algorithm can give landing
advice. If there is intersection between the bounding boxes of objects and the landing pad, that means there are
pedestrians or cars on the landing pad. Therefore, the algorithm will consider the drone unsuitable for landing and the
drone will pause its landing process and hold its position. When the object leaves the landing area, the algorithm detects
that the landing pad’s bounding box does not overlap any other bounding box. It proves that the landing area is safe, and
the algorithm clears the UAS for landing


## Results

### Demo video
The YOLOv5 detection:
{{< youtube fQm7ZFBYHF4 >}}

The RetinaNet detection:
{{< youtube SGFQ4z6T_2o >}}

### Time consumption
![Example image](/uploads/images/project_UAS_1.png)

### The onboard GPU we used
NVIDIA JETSON XAVIER NX
![Example image](/uploads/images/project_UAS_2.JPG)
