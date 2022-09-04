## Cancer Image recognition using CNN and Vision Transformers (ViT)

As part of my masters coursework, one of my elected projects was to design and implement a solution to detect and classify different severity of tumors using **machine learning**. Usage of machine learning in the medical field is a widely popular research area with numerous academic studies already published online. For this project I explore pre-trained CNNs and Vision transformer models for histopathic image recognition. 

**Note**: 
This project is intended for academic purposes - merely to demonstrate the application of learnings in real-world practice. I am NOT an expert in this field.

## **Task**
To build an image classification model which predicts patient histopathic images into 4 classes:
  - (0) meaning no cancers present
  - (1), (2) and (3) representing the type of tumor present
  
## **Data**
858 images of resolution 1024x1024 provided along with labels (on class) 

### Sample Data
|Class 0|Class 1|Class 2|Class 3|
|---|---|---|---|
|![image](https://user-images.githubusercontent.com/90996172/188314619-835dd405-4ad5-43ef-8c87-d825787a588b.png)|![image](https://user-images.githubusercontent.com/90996172/188314626-b45f989f-8315-4dee-8789-bc08a5d271c9.png)|![image](https://user-images.githubusercontent.com/90996172/188314629-7fb59854-f644-47e6-b61b-4ef52cc510a8.png)|![image](https://user-images.githubusercontent.com/90996172/188314645-6d412463-01a8-4776-8c7f-87bf33f71a9e.png)|

Pre-processed data via the following steps:
  1) Created training, validation and test set for cross validation
  2) Scaled images to reduce feature (1024 x 1024 x 3 RGB -> 224 x 224 x 3)
  3) Normalized pixels for similar brightness
  4) Augmented data - random cropping & random flipping

## Model Training methodology
 1) Initialised global varables - batch size, no. epochs, feature extraction
 2) Initialised CNN/ViT models with pre-training (from Pytorch) - did NOT build CNN/ViT from scratch
 3) Selected Cross Entropy Loss function and Stochastic gradient descent optimizer 
 4) Executed model training
 
## Training Outpout
 ![image](https://user-images.githubusercontent.com/90996172/188314330-022499b8-c8b9-47b1-a336-a1191535eb90.png)

## Model Evaluation Metrics:
||Alexnet|Resnet|vgg|densene|ViT|
---|---|---|---|---|---|
Recall|.9268|.8780|.8049|.9512|1.000|
F1 Score|.8312|.8174|.7980|.8377|.9891|

What?
  - Recall: Calculates the cost of type II error (false negatives) for the model. This implies patients with tumors are misdiadnosed as healthy.
  - F1 Score (class): Model evlaution metric that is sensitive to Type I (false positives) and Type II errors.
  
## Results:
The ViT model works remarkably well for histopathic image recognition and acheived an F1.score of 98.91% (way higher than group average) without any type II errors as indicated by recall of 100%. Of the 88 images in the test set, only 2 images were misclassified (class 1 and 3) which shows 
 
### WIP
  - Hyperparameter tuning for the following...
    1) Batch size for training
    2) Learning Rate of SGD optimizer
    3) Momentum 
    4) Epoch Size
  - Ensembling methods (combining models together)
  - Weighted F1 Scoring to increase weight of Type II error (instead of even distribution across 4 classes)
  - Randomly shuffling data and remodelling in case for 'lucky draw' for results. 
  - Procuring more images due to uneven distribution of images across classes
