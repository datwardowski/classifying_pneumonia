# Classifying Pneumonia
#### Dominika Twardowski

## Problem Statement
**Can we build an automated system to accurately detect pneumonia based on chest X-rays?**



## Executive Summary
The aim of this project was to use images of chest X-rays of pediatric patients and try to accurately identify the images as either normal lungs or pneumonia lungs. The images were obtained from a Kaggle dataset provided by Guangzhou Women and Children’s Medical Center. In total there were 5,856 images.  The chest X-rays were performed as part of the patients routine medical care and the images were labeled by expert physicians. The images were separated into Normal and Pneumonia and then separated into train, test, and validation sets prior to my introduction to the data.  I realized that the images, although only separated into Pneumonia and Normal folders, the Pneumonia images were also labelled as viral or bacterial. So after building a neural network model with a 93% (Adapted Resnet50 model) accuracy for classifying the binary classes, I decided to split the pneumonia images into viral and bacterial images. To obtain my best classifier, I had to ensemble two of my neural network models. For the three class classification problem I was able to attain a 86.1% accuracy.

**Models built**:   
Binary Classification:
- Fully Custom neural network
- Adapted InceptionV3 model
- Adapted Resnet50 model

Three class classification:
- Adapted InceptionV3 model
- Adapted Resnet50 model
- Ensemble model
  
**Code Overview**:  
The binary notebooks are in one folder together and each model is built in a separate notebook. Resnet50 and Inceptionv3 are pretrained models which were used for the base layer and Imagenet, an  image database, was used for the weights for these layers. Finally there is a results notebook which includes the confusion matrices for all the binary models as well as a ROC curve comparing all the models. 
  
The three class classification notebooks are in another folder. All the images were labelled by experts and I manually separated the pneumonia labelled images into virus and bacteria since the images were also labelled as viral or bacterial pneumonia. Since I found the most success with using pretrained network as my base layer, I decided to skip making a fully custom model. I trained the same pretrained models for the three class as I did for the binary classification. The notebooks are each labelled with the name of model and if they contain an ROC curve they have that in the title. The ensemble model was built by using the weights from my adapted InceptionV3 model and adapted Resnet50 model for the three classes. Then they were ensembled together to make a final classification of the images. The ensemble model was further trained and these notebooks are labelled with "continue_training" 01, 02, and 03. 


The weights for the models are not included in the repository since they were too large to upload. The initial dataset can be found at the datasource sited at the bottom. 

## Conclusion & Recommendations
  
The purpose of this project was to build a classification model that would most accurately predict whether an image was from a healthy patient or a patient with pneumonia. After achieving an accuracy of 93%, the project was expanded to see if good accuracy could be attained for the classification between normal, bacterial (pneumonia), or viral (pneumonia) images.
  
**How will success be evaluated**: Success will be evaluated based on a model performing better than the baseline and then the best model will be chosen based off best accuracy score. Secondary success metric will be looking at the recall of the pneumonia class (bacteria/virus class).
  
I have successfully built an automated system that is not only able to accurately detect pneumonia, but is also successful at identifying the type of the pneumonia. All the models successfully outperformed the baseline. The adapted Resnet50 model was the best model in the binary classification problem with an accuracy of 92.6% and a 0.94 recall for Pneumonia. The best model for the three class classification problem was the ensemble model. The accuracy for the ensemble model was 86.1% and recall of 0.95 for bacteria and 0.78 for virus.
  
### Binary Classification Results
|                     	| Accuracy 	| AUROC 	| Recall            	| Precision         	|
|:-------------------:	|----------	|-------	|-------------------	|-------------------	|
| Custom              	| 85.1%    	| 0.92  	| 0.93(P)   0.71(N) 	| 0.84(P)   0.87(N) 	|
| Adapted InceptionV3 	| 89.1%    	| 0.96  	| 0.94(P)   0.80(N) 	| 0.89(P)   0.90(N) 	|
| Adapted Resnet50    	| 92.6%    	| 0.97  	| 0.94(P)   0.90(N) 	| 0.94(P)   0.91(N) 	|


### Three class Classification Results
|             	| Accuracy 	| AUROC                        	| Recall                       	| Precision                     	|
|:-----------:	|----------	|------------------------------	|------------------------------	|-------------------------------	|
| InceptionV3 	| 85.7%    	| 0.98 (B)  0.97 (N)  0.94 (V) 	| 0.95 (B)  0.82 (N)  0. 77(V) 	| 0.85 (B)   0.95 (N)  0.75 (V) 	|
| Resnet50    	| 81.7%    	| 0.97 (B)  0.96 (N)  0.91 (V) 	| 0.90 (B)  0.75 (N)  0.78 (V) 	| 0.82 (B)  0.97 (N)  0.65 (V)  	|
| Ensemble    	| 86.1%    	| 0.98 (B)  0.97(N)  0.94 (V)  	| 0.95 (B)  0.81 (N)  0.78 (V) 	| 0.85 (B)  0.97 (N)  0.75 (V)  	|


**Recommendations**:
  A potential improvement could be incorporating additional models to the ensemble model which would hopefully increase the accuracy of the ensemble model. Another potential improvement would be increasing the training time of the models, gaining more chest X-ray images to train on, and implementing class weight function to address the class imbalance. The recall is not as high as I would like for the viral pneumonia class so I would like to tune the sensitivity for these images and hopefully improve the performance for the viral class.

 In the future I would like to explore the possibility of creating a web application which would allow a user to upload a chest X-ray image and it would let the user know if it is an image of normal lungs, bacterial, or viral pneumonia. 

Overall, my model did well thanks in part to my  incorporating pretrained neural networks as the base layers of the model. By adapting these successful pretrained networks I was able to create successful models which classified chest X-ray images correctly on the testing data with an accuracy score of 93% on the binary classes and 86% on the three classes.

## Data Sources
Kaggle Dataset: https://www.kaggle.com/paultimothymooney/chest-xray-pneumonia

Additional Resources:  
- https://www.scielosp.org/article/bwho/2008.v86n5/408-416B/ 
- https://data.unicef.org/topic/child-health/pneumonia/ 
- https://www.mayoclinic.org/diseases-conditions/pneumonia/symptoms-causes/syc-20354204?p=1
