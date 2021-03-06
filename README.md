# Detecting Pneumonia with Deep Learning
![deep_learning](https://cdn-images-1.medium.com/max/1600/0*5BKVjZL7eojyU1wH.jpg)

**Authors** Sandra Wellbeck and Joe Marx

## Overview

Pneumonia is a viral or bacterial infection affecting the respiratory system, that begins by inflaming the air sacs in one or both of the lungs <sup>1</sup>. While symptoms of pneumonia can be mild, they can become severe if left undiagnosed and can result in death.  With a health care system under unprecented strain, any tool that can delegate a Doctor's responsibilites adds a great aount of value. Detecting pneumonia from an x-ray is difficult even for the human eye, so training a deep learning convulutional network to recognize pneumonia in an x-ray image is an effecient and effective way to ease the burden of Radiologists and help prevent cases from going undetected.

## Data
![pneumonia_matrix](/images/image_matrix.png)

This dataset was sourced from Kaggle. It is comprised of over 5.5 thousand jpeg images of chest x-rays. Pneumonia x-images included both bacterial and viral infected cases. Pneumonia cases appear to be cloudier than normal cases, though differences are very subtle.

<img src="https://github.com/JoeBrowz/pneumonia-neural-net/blob/main/images/cls_imbal.jpg?raw=true" width="40%" class="center">
Images were organized into train, validation, and test folders, inside of which they were split by diagnosis. About 292 images were randomly chosen from the train folder (half normal cases half pneumonia cases) and put into the val folder. Data is not stored in this repo, to access the data, please download from Kaggle, using the link at the bottom of the readme. Approximately 75% of the images provided are labeled as pneumonia-positve cases. Class imbalance has been addressed through subtle data augmentation of the training set and setting balanced class weights when training the neural network. 

## Approach

The prediction model was built using the Keras package from Tensorflow. The model was built iteratively, through a process of metric optimization. Accuracy, precision, and recall were used to evaluate performance and Adam was used as the loss function. Our final model consists of 6 2-dimensional convultional layers, using a relu activation function, l2 regularization, padding, and a He initializer, each followed by a 2 by 2 max-pooling layer. The first layer used a 7 by 7 convulation filter and each subsequent one used a 3 by 3. The feature tensor is then flattenned,  run through a dropout layer, then a dense layer, again with a relu activation and He initializer function. The model was training using as many as 100 epochs. 

<img src="images/epochs.png">

## Outcome

The model had 99% accuracy, 99% recall, and 98% precision on the validation set. And when tested on unseen data the model had 86% accuracy, 99% recall, and 82% precision. Notably, with very high recall, there are not many poisitve cases left undetected by the model. The cases would then be verified by a doctor to check for a false positive. As a next step, using pretrained models, other more specialized network architetures, PCA, and more sophisticated image augmentation should be implemented to improve accuracy on the unseen data. 

<img width="29%" src="/images/fn.jpg"> <img width="29%" src="/images/fp.jpg"> <img width="37%" src="/images/confusion_matrix.jpg"> 

```
├── Final_Notebook.ipynb           <- notebook containing all elements of model
├── images                         <- generated from code
├── models                         <- saved models (CANNOT STORE ON GITHUB)
├── README.md                      <- the top-level README for reviewers of this project
├── Pneumonia-Image-Classificat... <- a pdf of the project presentation
└── xrays                          <- dataset files (MUST BE DOWNLOADED FROM KAGGLE)

```


## Sources
Dataset: https://www.kaggle.com/paultimothymooney/chest-xray-pneumonia

<sup>1</sup> Mayoclinic https://www.mayoclinic.org/diseases-conditions/pneumonia/symptoms-causes/syc-20354204
