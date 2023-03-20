
![correlation_temp](img/sagemaker.jpeg) ![temp](img/autogluon.png)


# Abstract

Bike-sharing demand is highly relevant to related problems companies encounter, such as Uber, Lyft, and DoorDash. Predicting demand not only helps businesses prepare for spikes in their services but also improves customer experience by limiting delays


## Project Environment

AWS Sagemaker Studio was used for this project as it can be seen in the project repo.

## Data set

Data was downloaded from kaggle.
```
!kaggle competitions download -c bike-sharing-demand
!unzip -o bike-sharing-demand.zip
```

## Problem Statement

Predict Bike Sharing Demand with AutoGluon AutoML


# Conclusion

* **Initial**
The training time takes is very long compered to when feature engineering was applied
There was no data preprocessing in the initial stage of training which is good feature
 * **New features**
The score was improved as well as the training time. The new features which were added during feature engineering enhaced the model training fro better  results
* **Hyperparameter Tuning**
The time for training was a lot faster compared to the other stages. The number of models for training were 14 compared to 15 with the default parameters.

## Reflection

1. Many models are better than few and hyperparemeter tuning enhances learning.
   There is no train split manually the model does that internally.
   The model handles missing values and this is the second stage during training.
2. I will spend more time doing the data analysis to get to know data in detail trying different analysis methods.



