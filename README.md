# Heart Disease Classification

Cardiovascular disease or heart disease is the leading cause of death amongst women and men and amongst most racial/ethnic groups in the United States. Heart disease describes a range of conditions that affect your heart. Diseases under the heart disease umbrella include blood vessel diseases, such as coronary artery disease. From the [CDC](https://www.cdc.gov/heartdisease/facts.htm), roughly every 1 in 4 deaths each year are due to heart disease. The WHO states that human life style is the main reason behind this heart problem. Apart from this there are many key factors which warns that the person may/may not getting chance of heart disease.

Using UCI’s heart disease dataset found [here](https://archive.ics.uci.edu/ml/datasets/Heart+Disease), I build classification models and used ensemble methods to produce a highly accurate model. In the current dataset, publications of this study included 303 patients and chose 14 out of 76 features that are relevant in predicting heart disease.

**Variable Descriptions**
* age: age in years
* sex: sex (1 = male; 0 = female)
* cp: chest pain type — Value 1: typical angina, Value 2: atypical angina, Value 3: non-anginal pain, Value 4: asymptomatic
* trestbps: resting blood pressure (in mm Hg on admission to the hospital)
* chol: serum cholestoral in mg/dl
* fbs: (fasting blood sugar > 120 mg/dl) (1 = true; 0 = false)
* restecg: resting electrocardiographic results- Value 0: normal, Value 1: having ST-T wave abnormality (T wave inversions and/or ST elevation or depression of > 0.05 mV), Value 2: showing probable or definite left ventricular hypertrophy by Estes’ criteria
* thalach: maximum heart rate achieved
* exang: exercise induced angina (1 = yes; 0 = no)
* oldpeak = ST depression induced by exercise relative to rest
* slope: the slope of the peak exercise ST segment- Value 1: upsloping, Value 2: flat, Value 3: downsloping
* ca: number of major vessels (0–3) colored by flourosopy
* thal: 3 = normal; 6 = fixed defect; 7 = reversable defect
* target: 1 = disease, 0 = no disease

**Variable Types**
* Continuous — age, trestbps, chol, thalach, oldpeak
* Binary — sex, fbs, exang, target
* Categorical — cp, restecg, slope, ca, thal

## Exploratory Data Analysis (code found in [1. EDA.ipynb](https://github.com/mkosaka1/HeartDisease_Classification/blob/main/1.%20EDA.ipynb))
<img align="left" width="100" height="100" src="https://github.com/mkosaka1/HeartDisease_Classification/blob/main/Images/Target_Distribution.pn">
There is a slight class imbalance, but not severe enough to require upsampling/downsampling methods.

Now let’s see how fasting blood sugar (**fbs**) varies amongst the target variable. Fbs is a diabetes indicator with fbs >120 mg/d is considered diabetic (True):
<img align="left" width="100" height="100" src="https://github.com/mkosaka1/HeartDisease_Classification/blob/main/Images/FBS_%26_Target.png">

Here, we see that the number for class true, is lower compared to class false. This provides an indication that fbs might not be a strong feature differentiating between heart disease an non-disease patient.

Next, we'll look at **ca** which is the number of major blood vessels (0-3) colored by a flourosopy.
![image3](https://github.com/mkosaka1/HeartDisease_Classification/blob/main/Images/Ca_%26_Target.png)
We can clearly see that a large proportion of those with heart disease were likely to have 0 major blood vessels to the heart.

## Classification (code found in [2. Classification.ipynb](https://github.com/mkosaka1/HeartDisease_Classification/blob/main/2.%20Classification.ipynb)
A simple dummy classifier resulted in an accuracy score of 49.18%.

Next I took different machine learning models to find which algorithm has the best accuracy score.
![image4](https://github.com/mkosaka1/HeartDisease_Classification/blob/main/Images/NoGridSearch_ModelEvaluation.png)

Then I selected the top 3 performing classification models (SVC,Logistic Regression, and Naive Bayes)and inputed them into a StackingCVClassifier. This resulted in an accuracy score of ~92%, outperforming all individual classification models.
![image6](https://github.com/mkosaka1/HeartDisease_Classification/blob/main/Images/StackingCVClassifier_report.png)
![image5](https://github.com/mkosaka1/HeartDisease_Classification/blob/main/Images/ROC.png)
![image9](https://github.com/mkosaka1/HeartDisease_Classification/blob/main/Images/Ensemble_CM.png)

Variable **ca** was the most important feature in predicting the target variable
![image8](https://github.com/mkosaka1/HeartDisease_Classification/blob/main/Images/Feature_Importance.png)

## Grid Search + Ensemble

Using grid search methods on all individual classification models then utilizing the Stacking CVClassifier resulted in the same ensemble accuracy without using grid search.
![image9](https://github.com/mkosaka1/HeartDisease_Classification/blob/main/Images/GridSearch_StackingClass.png)

## Summary

From this classification project, we can see that using a stacking cv classifier improves the overall accuracy compared to using individual classification models. Our base model performed at ~49% while our ensemble model performed at ~92% accuracy. Using the grid search plus ensemble methods did not improve the overall accuracy. 

