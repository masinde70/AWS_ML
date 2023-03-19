# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### Masinde Mtesigwa Masinde

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
The number of models which were trained were 15, in this stage there was no data preprocessing.

```
Estimated performance of each model:
                     model   score_val  pred_time_val    fit_time  pred_time_val_marginal  fit_time_marginal  stack_level  can_infer  fit_order
0      WeightedEnsemble_L3  -52.847596      11.249226  502.330480                0.001120           0.436674            3       True         15
1   RandomForestMSE_BAG_L2  -53.473435      10.375775  403.099560                0.597212          25.713495            2       True         12
2     ExtraTreesMSE_BAG_L2  -53.810409      10.386975  385.264302                0.608412           7.878237            2       True         14
3          LightGBM_BAG_L2  -55.046580       9.989433  398.853544                0.210870          21.467479            2       True         11
4          CatBoost_BAG_L2  -55.516287       9.831613  446.834595                0.053049          69.448530            2       True         13
5        LightGBMXT_BAG_L2  -60.425971      13.133647  427.012202                3.355083          49.626137            2       True         10
6    KNeighborsDist_BAG_L1  -84.125061       0.038490    0.029288                0.038490           0.029288            1       True          2
7      WeightedEnsemble_L2  -84.125061       0.039427    0.675935                0.000937           0.646647            2       True          9
8    KNeighborsUnif_BAG_L1 -101.546199       0.038787    0.031544                0.038787           0.031544            1       True          1
9   RandomForestMSE_BAG_L1 -116.544294       0.534120   10.116589                0.534120          10.116589            1       True          5
10    ExtraTreesMSE_BAG_L1 -124.588053       0.530154    4.933934                0.530154           4.933934            1       True          7
11         CatBoost_BAG_L1 -130.482869       0.099427  191.457479                0.099427         191.457479            1       True          6
12         LightGBM_BAG_L1 -131.054162       1.488921   25.595079                1.488921          25.595079            1       True          4
13       LightGBMXT_BAG_L1 -131.460909       6.707506   59.929166                6.707506          59.929166            1       True          3
14  NeuralNetFastAI_BAG_L1 -136.015060       0.341158   85.292985                0.341158          85.292985            1       True          8
Number of models trained: 15

```
Best model was "WeightedEnsemble_L3"

### What was the top ranked model that performed?
The best top ranked model in Initial training was "WeightedEnsemble_L3"

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?
Here I did 

* Feature engineering
Transforming the weather and season columns to category from ints since autogluon sees them as ints.
Parsing the datetime to separate features for further analyis

* Plotting the distribution of registered vs casual rides.
The findings were as follows:
The registered users perform way more rides than casual ones. Furthermore, we can see that the two distributions are skewed to the right, meaning that, 
for most of the entries in the data, zero or a small number of rides. Finally, every entry in the data has quite a large number of rides (that is, higher than 800).
 * correlation 
     *  correlation between rides and temperature
     The higher temperatures have a positive impact on the number of rides (the correlation between registered/casual rides and temp is 0.31 and 0.46, respectively, and it's a  similar case for atemp). Note that as the values in the registered column are widely spread with respect to the different values in temp, we have a lower correlation compared to the casual column. ![correlation_temp.png](correlation_temp.png) ![correlation_atemp.png](correlation_atemp.png)
     * Correlation between rides and humidity ![correlation_hum.png](correlations_hum.png)
     * Correlation between the number of rides and the wind speed ![correlation_windspeed.png](correlations.png)
     * Correlation Matrix Plot ![correlation.png](correlations.png)

The conclusion of the visualization is that when the temperature is good the hire of the bike is good for both registered users and casual users.

### How much better did your model preform after adding additional features and why do you think that is?
The model performed better after changing some of the columns/features to categorical data and also after adding new features, from the score of 1.8 to 1.33

## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?
After hyperparameter tuning, the model slightly changed from the score of 1.33 to 1.32

### If you were given more time with this dataset, where do you think you would spend more time?
I will spend more time doing the data analysis to get to know data in detail trying different analysis methods.

### Table with the models you ran, the hyperparameters modified, and the kaggle score


### A line plot showing the top model score for the three (or more) training runs during the project.

![model_train_score.png](img/model_train_score.png)

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.


![model_test_score.png](img/model_test_score.png)

## Summary
```
Estimated performance of each model:
                             model   score_val  pred_time_val    fit_time  pred_time_val_marginal  fit_time_marginal  stack_level  can_infer  fit_order
0              WeightedEnsemble_L3  -45.237593       0.001964  136.536450                0.000992           0.555725            3       True         14
1   NeuralNetTorch_BAG_L2/877bc604  -45.947510       0.000861  124.461472                0.000160          32.741020            2       True         13
2               LightGBM_BAG_L2/T5  -49.723478       0.000812  103.239705                0.000111          11.519253            2       True         12
3              WeightedEnsemble_L2  -51.955120       0.001266   46.451789                0.000971           0.569900            2       True          7
4   NeuralNetTorch_BAG_L1/469e5854  -56.261557       0.000171   34.386352                0.000171          34.386352            1       True          6
5               LightGBM_BAG_L2/T2  -61.015430       0.000808  103.493750                0.000107          11.773299            2       True          9
6               LightGBM_BAG_L1/T5  -62.269851       0.000124   11.495537                0.000124          11.495537            1       True          5
7               LightGBM_BAG_L1/T2  -70.588170       0.000097   11.423693                0.000097          11.423693            1       True          2
8               LightGBM_BAG_L2/T3  -77.938179       0.000776  103.443859                0.000075          11.723408            2       True         10
9               LightGBM_BAG_L2/T1  -78.093263       0.000785  103.862269                0.000084          12.141818            2       True          8
10              LightGBM_BAG_L1/T3  -90.207152       0.000110   11.416231                0.000110          11.416231            1       True          3
11              LightGBM_BAG_L1/T1  -95.483677       0.000120   11.565247                0.000120          11.565247            1       True          1
12              LightGBM_BAG_L2/T4 -161.546488       0.000813  103.448732                0.000112          11.728281            2       True         11
13              LightGBM_BAG_L1/T4 -165.490162       0.000080   11.433391                0.000080          11.433391            1       True          4
Number of models trained: 14

```
# Conclusion

* **Initial**
The training time takes is very long compered to when feature engineering was applied
There was no data preprocessing in the initial stage of training which is good feature
 * **New features**
The score was improved as well as the training time. The new features which were added during feature engineering enhaced the model training fro better  results
* **Hyperparameter Tuning**
The time for training was a lot faster compared to the other stages. The number of models for training were 14 compared to 15 with the default parameters.

## Reflection

* **Lessons learnt**
Many models are better than few and hyperparemeter tuning enhances learning.
There is no train split manually the model does that internally.
The model handles missing values and this is the second stage during training

