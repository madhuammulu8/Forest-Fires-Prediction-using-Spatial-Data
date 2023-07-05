Table of Content
 * [Abstract](#Abstract)
 * [Data Source](#Data-Source)
 * [Data Cleaning](#Data-Cleaning)
 * [Some Cool Data Analysis Images](#Some-Cool-Data-Analysis-Images)
 * [Evaluation and Training of Models](#Evaluation-and-Training-of-Models)
 * [Outcome](#Outcome)

# Abstract

Our project comprises gathering and processing historical records of fire incidents in order to study the fire events and discover the patterns and links with multiple characteristics, including wind speed, air temperature, humidity, precipitation, Rain, etc. The two major objectives of the study will be to predict the predicted fire perimeter and to pinpoint it on the map. With the use of this information, we can locate any potential risk areas and, if required, evacuate. In addition, the project will construct and project forest fire hotspots onto a geographical map

# Data Source 

Forest Fires are becoming a bigger problem and a recent survey shows that at least in Portugal more than 300 people died from forest fires spread in the year 2016 and also causing damage to the local economy and environment, To get around this, we discovered the open-source dataset of Portugal's Montesinho Natural Park from the UC Irvine Machine Learning Repository (https://archive.ics.uci.edu/dataset/162/forest+fires)

# Data Cleaning

* Removed unnecessary or irrelevant observations; only Northeastern Portugal-related data was kept.
* Eliminated redundant or duplicate observations; these observations have been removed based on the incident name.
* Structural errors have been rectified, and any data that had the characters "-", "NA" or "" have been corrected by giving them a default value.
* Records that lacked necessary information were deleted.

# Some Cool Data Analysis Images : 

### Burnt Area with respect to Months

<img width="258" alt="image" src="https://github.com/madhuammulu8/Forest-Fires-Prediction-using-Spatial-Data/assets/65707202/1b4544d7-e97c-4bbf-bf76-d5a4aa4c4c09">

### Visualization of the Area Burnt in the X, Y Co-ordinates

<img width="221" alt="image" src="https://github.com/madhuammulu8/Forest-Fires-Prediction-using-Spatial-Data/assets/65707202/db5147bf-1bd2-48be-8368-0cb212741384">

### Burnt Area with respect to Temperature

<img width="255" alt="image" src="https://github.com/madhuammulu8/Forest-Fires-Prediction-using-Spatial-Data/assets/65707202/caf106a7-ccd2-4bed-ad71-a0e9684c9fbe">

# Evaluation and Training of Models

We tried different machine learning algorithms such as SVM, Decision Tree Classifier, Random Forest Classifier, Gaussian NB, and Voting Classifier using the area as testing data by dropping DMC, ISI, FFMC, and Temp.

### Training and Testing Data: 

We used sklearn to train and test the data where formatted data because we cannot use the string(month and day feature) and also we can see we have dropped the area feature since we are going to use it as test data

<img width="481" alt="image" src="https://github.com/madhuammulu8/Forest-Fires-Prediction-using-Spatial-Data/assets/65707202/ac810aeb-71b9-415b-9703-85896438a50f">

### SVM: 
Support vector machines are supervised machine learning algorithm which helps in analyzing and classifying the data we got an F1 score for the first classifier for the SVM about 64 for testing data

<img width="307" alt="image" src="https://github.com/madhuammulu8/Forest-Fires-Prediction-using-Spatial-Data/assets/65707202/78de2bed-0c2f-484b-9c73-5a6c7c328963">

### Decision Tree Classifier: 
It is one of the most powerful algorithms and we got an F1 score of 1st classifier 54 for testing data

<img width="452" alt="image" src="https://github.com/madhuammulu8/Forest-Fires-Prediction-using-Spatial-Data/assets/65707202/1ba01ba7-16cf-4d19-be22-74067e40eb9b">

### Random Forest Classifier:
It is an assembling method that operates by constructing a multi-decision tree and it got a 61% F1 score for testing data

<img width="433" alt="image" src="https://github.com/madhuammulu8/Forest-Fires-Prediction-using-Spatial-Data/assets/65707202/44510af2-4928-4112-bbba-f07ef13b87c7">

### Gaussian NB:
It works based on Navies Bayes with strong independence assumption and Testing accuracy of 49 for one of the classifier 

<img width="390" alt="image" src="https://github.com/madhuammulu8/Forest-Fires-Prediction-using-Spatial-Data/assets/65707202/0926eed8-3eff-40cb-9dde-025b31979800">

### Voting Classifier:
The voting classifier aggregates the results from the above classifier and takes the majority vote to decide if a particular object belongs to a class or not.

<img width="393" alt="image" src="https://github.com/madhuammulu8/Forest-Fires-Prediction-using-Spatial-Data/assets/65707202/99ec359e-3cd8-4ffc-8f06-ef2284854c66">

# Outcome : 
The outcome of our project we have found the spreading point of forest fire in Montesinho Natural Park and we have plotted the point on the map.

<img width="317" alt="image" src="https://github.com/madhuammulu8/Forest-Fires-Prediction-using-Spatial-Data/assets/65707202/648f7d3a-070e-4206-99ee-737fbeb151b1">
