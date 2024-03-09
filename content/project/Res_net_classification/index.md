---
title: Blood cell classification
summary: A deep-learning based medical image classification project.
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

This project using deep learning method to do the classification for the blood smear images. 
We test and compared three classic classification model here: ResNet, EfficientNet and the AlexNet.

## Methods
### Dataset
Here is the dataset link: https://www.kaggle.com/datasets/paultimothymooney/blood-cells.

The row dataset containing 410 images for 5 classes:
![Show 5 classes](/uploads/images/project_resnet_1.png)

We clean the data by:
>1. Delete 10% of the Neutrophil
>2. Training the less-amount class multi-time
>3. Drop the Basophil class
>4. Drop the double class
>5. Drop the null class
![The comparison](/uploads/images/project_resnet_2.png "Dataset distribution after cleaning")

Also, I do the data exploration by drawing the pixel distribution and average images.

| ![Average](/uploads/images/project_resnet_3.png "average images for each class") | ![Distribution](/uploads/images/project_resnet_4.png "Pixel distribution") |
|----------------------------------------------------------------------------------|----------------------------------------------------------------------------|



### Model selection
#### ResNet
This model solved the degradation problem: As the network became deeper and deeper, the error begin to increase - hard to converge.
- Not caused by overfitting, because the training error is also increase
- Not caused by gradients vanishing/exploding, because this problem has been largely addressed by normalization layers.

Core concept - the residual block
- The target weight is near the identity.
- A identity map adding the block-beginning layer feature to the block-ending layer.
- Solve the degradation problem.

![The Resisual block](/uploads/images/project_resnet_5.png "Residual learning: a building block.")

#### EfficientNet
The author of the EfficientNet firstly using neural architecture search to find the baseline network, which ensures the whole architecture to be smaller and more accurate. And then he proposes a compound scaling method, uniform scale network width, depth and resolution using a composite factor φ. He scaled up the baseline model by this composite factor and come up with the EfficientNet.

To test the robustness of the scaling method, the author applies the scaling method to MobileNets and Resnets, showing that the composite scaling method improves the accuracy of all these models.
![Scaling](/uploads/images/project_resnet_6.png "Model Scaling.")


#### AlexNet
Traditional CNN, just as a control group to evaluate the performance of the EfficientNet and the ResNet.


## Results
We evaluate the model by the training loss/accuracy graph, confusion matrix and the statistic information.

### The result of the EfficientNet
| ![EfficientNet loss graph](/uploads/images/project_resnet_7.png "The loss decreasing graph of the EfficientNet.")            | ![EfficientNet accuracy graph](/uploads/images/project_resnet_8.png "The accuracy increasing graph of the EfficientNet.") |
|------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|

![EfficientNet confusion matrix](/uploads/images/project_resnet_9.png "The confusion matrix of the EfficientNet.")

The statistic information of the EfficientNet:<br>
- The number of right prediction is 32
- The number of total prediction is 35
- The accuracy is 0.914
- For type NEUTROPHIL:
  - The recall/sensitivity is 0.833
  - The specificity is 1.000
  - The precision is 1.000
- For type EOSINOPHIL:
  - The recall/sensitivity is 1.000
  - The specificity is 0.938
  - The precision is 0.600
- For type MONOCYTE:
  - The recall/sensitivity is 0.667
  - The specificity is 1.000
  - The precision is 1.000
- For type LYMPHOCYTE:
  - The recall/sensitivity is 0.957
  - The specificity is 0.917
  - The precision is 0.957


### The result of the ResNet
| ![ResNet loss graph](/uploads/images/project_resnet_10.png "The loss decreasing graph of the ResNet.") | ![Resnet accuracy graph](/uploads/images/project_resnet_11.png "The accuracy increasing graph of the ResNet.") |
|--------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|

![ResNet confusion matrix](/uploads/images/project_resnet_12.png "The confusion matrix of the ResNet.")


The statistic information of the ResNet:<br>
- The number of right prediction is 28
- The number of total prediction is 35
- The accuracy is 0.800
- For type NEUTROPHIL:
  - The recall/sensitivity is 1.000
  - The specificity is 0.759
  - The precision is 0.462
- For type EOSINOPHIL:
  - The recall/sensitivity is 1.000
  - The specificity is 1.000
  - The precision is 1.000
- For type MONOCYTE:
  - The recall/sensitivity is 1.000
  - The specificity is 1.000
  - The precision is 1.000
- For type LYMPHOCYTE:
  - The recall/sensitivity is 0.696
  - The specificity is 1.000
  - The precision is 1.000

### The result of the AlexNet
| ![AlexNet loss graph](/uploads/images/project_resnet_13.png "The loss decreasing graph of the AlexNet.") | ![AlexNet accuracy graph](/uploads/images/project_resnet_14.png "The accuracy increasing graph of the AlexNet.") |
|----------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------|

![AlexNet confusion matrix](/uploads/images/project_resnet_15.png "The confusion matrix of the AlexNet.")

The statistic information of the AlexNet:<br>
- The number of right prediction is 6
- The number of total prediction is 35
- The accuracy is 0.171
- For type NEUTROPHIL:
  - The recall/sensitivity is 1.000
  - The specificity is 0.000
  - The precision is 0.171
- For type EOSINOPHIL:
  - The recall/sensitivity is 0.000
  - The specificity is 1.000
  - The precision is 0
- For type MONOCYTE:
  - The recall/sensitivity is 0.000
  - The specificity is 1.000
  - The precision is 0
- For type LYMPHOCYTE:
  - The recall/sensitivity is 0.000
  - The specificity is 1.000
  - The precision is 0

Obviously, the AlexNet can't catch enough feature to make right decision.

### Models comparison
<div class="table">

|    Model     | Accuracy | Average sensitivity | Average specificity |
|:------------:|:--------:|:-------------------:|:-------------------:|
|   AlexNet    |   0.17   |        0.25         |        0.75         |
|    ResNet    |   0.80   |        9.92         |        0.94         |
| EfficientNet |   0.91   |        0.86         |        0.97         |

</div>

## Conclusion
In this project, I trained 3 classification models and test their performance. Although the traditional AlexNet
can't extract enough feature to make right decision, the performance of the ResNet and the EfficientNet
is pretty good. Especially for the EfficientNet, the accuracy of it reach above 90 percent.
