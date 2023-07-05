# Table of Content
 * [Abstract](#Abstract)
 * [Data Source](#Data-Source)
 * [Data Cleaning](#Data-Cleaning)
 * [Some Cool Data Analysis Images](#Some-Cool-Data-Analysis-Images)
   * [Burnt Area with respect to Months](#Burnt-Area-with-respect-to-Months)
   * [Visualization of the Area Burnt in the X, Y Co-ordinates](#Visualization-of-the-Area-Burnt-in-the-X,-Y-Coordinates)
   * [Burnt Area with respect to Temperature](#Burnt-Area-with-respect-to-Temperature)
 * [Evaluation and Training of Models](#Evaluation-and-Training-of-Models)
   * [Training and Testing Data](#Training-and-Testing-Data)
   * [SVM](#SVM)
   * [Decision Tree Classifier](#Decision-Tree-Classifier)
   * [Random Forest Classifier](#Random-Forest-Classifier)
   * [Gaussian NB](#Gaussian-NB)
   * [Voting Classifier](#Voting-Classifier)
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

# Some Cool Data Analysis Images

### Burnt Area with respect to Months

<img width="258" alt="image" src="https://github.com/madhuammulu8/Forest-Fires-Prediction-using-Spatial-Data/assets/65707202/1b4544d7-e97c-4bbf-bf76-d5a4aa4c4c09">

### Visualization of the Area Burnt in the X, Y Coordinates

<img width="221" alt="image" src="https://github.com/madhuammulu8/Forest-Fires-Prediction-using-Spatial-Data/assets/65707202/db5147bf-1bd2-48be-8368-0cb212741384">

### Burnt Area with respect to Temperature

<img width="255" alt="image" src="https://github.com/madhuammulu8/Forest-Fires-Prediction-using-Spatial-Data/assets/65707202/caf106a7-ccd2-4bed-ad71-a0e9684c9fbe">

# Evaluation and Training of Models

We tried different machine learning algorithms such as SVM, Decision Tree Classifier, Random Forest Classifier, Gaussian NB, and Voting Classifier using the area as testing data by dropping DMC, ISI, FFMC, and Temp.

### Training and Testing Data: 

We used sklearn to train and test the data where formatted data because we cannot use the string(month and day feature) and also we can see we have dropped the area feature since we are going to use it as test data

```
from sklearn.model_selection import train_test_split
X=df
X_new_month=recon(X)
X['month']=X_new_month
X_new_days=recon2(X)
X['day']=X_new_days
y = X['area']
y1=ar_cat(X)
y=y1
X = X.drop('area', axis=1)
X_train, X_test, y_train, y_test = train_test_split(X, y, train_size=0.7, shuffle=True, random_state=1)

```

### SVM: 
Support vector machines are supervised machine learning algorithm which helps in analyzing and classifying the data we got an F1 score for the first classifier for the SVM about 64 for testing data

```
from sklearn import svm
model = svm.SVC(kernel='poly')
model.fit(X_train,y_train)

test_predicted = model.predict(X_test)
train_predicted = model.predict(X_train)

from sklearn.metrics import accuracy_score

train_accuracy = f1_score(y_train, train_predicted,average=None)
test_accuracy = f1_score(y_test, test_predicted,average=None)
print('SVM training accuracy is', train_accuracy)
print('SVM test accuracy is', test_accuracy)
```

### Decision Tree Classifier: 
It is one of the most powerful algorithms and we got an F1 score of 1st classifier 54 for testing data

```
from sklearn.tree import DecisionTreeClassifier
model = DecisionTreeClassifier(max_depth=7 ,min_samples_leaf=6 ,min_samples_split=4)
model.fit(X_train,y_train)
test_predicted = model.predict(X_test)
train_predicted = model.predict(X_train)

from sklearn.metrics import accuracy_score

train_accuracy = f1_score(y_train, train_predicted,average=None)
test_accuracy = f1_score(y_test, test_predicted,average=None)
print('DecisionTreeClassifier training accuracy is', train_accuracy)
print('DecisionTreeClassifier test accuracy is', test_accuracy)

```

### Random Forest Classifier:
It is an assembling method that operates by constructing a multi-decision tree and it got a 61% F1 score for testing data

```
from sklearn.ensemble import RandomForestClassifier
model = RandomForestClassifier(n_estimators=100, max_depth=2, random_state=0)
model.fit(X_train,y_train)
test_predicted = model.predict(X_test)
train_predicted = model.predict(X_train)

from sklearn.metrics import accuracy_score
train_accuracy = f1_score(y_train, train_predicted,average=None)
test_accuracy = f1_score(y_test, test_predicted,average=None)
print('RandomForestClassifier training accuracy is', train_accuracy)
print('RandomForestClassifier test accuracy is', test_accuracy)
```

### Gaussian NB:
It works based on Navies Bayes with strong independence assumption and Testing accuracy of 49 for one of the classifier 

```
from sklearn.naive_bayes import GaussianNB
model = GaussianNB()
model.fit(X_train, y_train)
final = model.predict(X_test)

test_predicted = model.predict(X_test)
train_predicted = model.predict(X_train)

from sklearn.metrics import accuracy_score
train_accuracy = f1_score(y_train, train_predicted,average=None)
test_accuracy = f1_score(y_test, test_predicted,average=None)
print('GaussianNB training accuracy is', train_accuracy)
print('GaussianNB test accuracy is', test_accuracy)
```

### Voting Classifier:
The voting classifier aggregates the results from the above classifier and takes the majority vote to decide if a particular object belongs to a class or not.

```
from sklearn.ensemble import VotingClassifier
from sklearn import svm
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import RandomForestClassifier
m1= GaussianNB()
m2=svm.SVC(kernel='poly')
m3=RandomForestClassifier(n_estimators=100, max_depth=2, random_state=0)
m4=DecisionTreeClassifier(max_depth=7 ,min_samples_leaf=6 ,min_samples_split=4)
eclf1 = VotingClassifier(estimators=[ ('gnb', m1), ('rf', m3), ('dtc', m4),('svm',m2)], voting='hard')
eclf1.fit(X_train, y_train)
test_predicted = eclf1.predict(X_test)
train_predicted = eclf1.predict(X_train)

from sklearn.metrics import accuracy_score
train_accuracy = accuracy_score(y_train, train_predicted)
test_accuracy = accuracy_score(y_test, test_predicted)
print('Ensemble training accuracy is', train_accuracy)
print('Ensemble test accuracy is', test_accuracy)
```
# Outcome
The outcome of our project we have found the spreading point of forest fire in Montesinho Natural Park and we have plotted the point on the map.

<img width="317" alt="image" src="https://github.com/madhuammulu8/Forest-Fires-Prediction-using-Spatial-Data/assets/65707202/648f7d3a-070e-4206-99ee-737fbeb151b1">
