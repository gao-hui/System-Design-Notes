# [System Design] Street View Blurring

## High-level Design

![Untitled](%5BSystem%20Design%5D%20Street%20View%20Blurring%20fb42078bc2c24689b38519af6aef3cb2/Untitled.png)

## System Responsibility:

- Predicting the location of each object in the image (regression problem)
- Predicting the class of each bounding box (multi-class classification problem)

## Two-Stage Networks

- Region proposal network (RPN)
- Classifier

Slower, more accurate

e.g., R-CNN, Fast R-CNN, Faster-RCNN

## One-Stage Networks

Use a single network (generate bounding boxes and object classes)

Faster, less accurate

e.g., YOLO, SSD

## Feature Engineering

Preprocessing: resizing and normalization

Data augmentation: increase the size of dataset

![Untitled](%5BSystem%20Design%5D%20Street%20View%20Blurring%20fb42078bc2c24689b38519af6aef3cb2/Untitled%201.png)

## Two-Stage Object Detection Network

Convolutional layers, Region Proposal Network (RPN), Classifier

![Untitled](%5BSystem%20Design%5D%20Street%20View%20Blurring%20fb42078bc2c24689b38519af6aef3cb2/Untitled%202.png)

## Model Training

- Regression loss (e.g., MSE): bounding boxes
- Classification loss (e.g., cross-entropy): classify object
- Final loss: combine the classification loss and regression loss with a parameter

## Evaluation

Intersection Over Union (IOU): the overlap between two bounding boxes

Offline metrics: 

- precision (varies with different IOU thresholds, for a specific class)
- average precision (various IOU thresholds, for a specific class)
- mean average precision (for all object classes)

Online metrics: user reports and complaints

## Overlapping bounding boxes

Non-maximum suppression (NMS): post-algorithm to select the most appropriate box

## Summary

![Untitled](%5BSystem%20Design%5D%20Street%20View%20Blurring%20fb42078bc2c24689b38519af6aef3cb2/Untitled%203.png)