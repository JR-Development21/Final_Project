# Final_Project
## Introduction
Running as a sport is classically under-analyzed. Unlike baseball, football, and basketball, running doesn't have a high demand for analytics. This is largely due to the fact that it is generally not very well funded. As such, the data available in larger sports is not available for running, like movement, relative position, etc. because data collection is expensive. Perhaps the most criminally understudied event in athletics is the marathon, as it has a high rate of participation with an almost absent viewership. However, as the longest Olympic event, there are likely several interesting analytics that haven't been found as of yet. We therefore propose using a generalized boosting tree ensemble (GBM) to try to model large amounts of sparse marathon data. We will attempt to augment the sparsity of the matrix by adding new columns. During this analysis we hope to model the data from the top 1000 men's marathon performances with data found online. Additionally, we will use the model fit to that data to predict the 2021 Olympic men's marathon. Finally, we will use partial effect plots to find how diffferent features might be correlated with marathon time.
## Data
### Data Through 2016
The marathon data was found through links this article https://towardsdatascience.com/analysing-elite-running-performance-with-historical-data-b9c6bdd9c5d8 in the reference section (marked [1] and [3]). These datasets were scraped sites that record running results and wrangled by Kaggle users. The first dataset was scraped from sports-reference.com and contains the height and weight of athletes, as well as the years they competed in the Olympic games. The second was scraped from alltime-athletics.com and contains the top 1000 times recorded for various Olympic distances, including the athletes' names and country of origin. This should not be confused with the top 1000 times of Olympic running events, which is a mistake that results in bad prediction, as will be discussed later. The final dataset we used can be found at https://www.kaggle.com/tunguz/country-regional-and-world-gdp. It contains the gross domestic product (GDP) of most countries, as well as the associated country code. It should be noted that we only used the GDP from 2016.
### 2021 Olympic Results
In addition to these datasets, we scraped data from olympedia.org, since the results moved from sports-reference.com to olympedia.org. This data contained similar columns to those contained in the references in the towardsdatascience.com article, but contained data from the men's Olympic marathon from 2021.
## Data Wrangling

## EDA

## Model and Tuning

A gradient boosted regressor was trained on the marathon data set. We chose to use this model for a variety of reasons as outlined below:

	1. Gradient boosted models are flexible for working with many types of data sets without the excessive computational requirements of a deep learning model
	2. Many gradient boosting models can account for nan values in the dataset without imputation
	3. Gradient boosted models have shown to be strong at predicting on data, but at the cost of less interpretability. Our project focuses on prediction. 

On the hyperparameter tuning step, we chose five key parameters to tune our model:

learning_rate: Changes the contribution of each tree in the model

	- n_estimators: Considers the number of boosting stages to perform on the model
	- max_depth: Limits the number of nodes in trees
	- min_samples_split: Minimum number of samples needed to split a node. 
	- min_samples_leaf: Minimum number samples required to be a leaf node. 

Each of these hyperparameters were indicated to have the greatest effect on modifying the model for optimal tuning on the data set. 

The model was tuned using a repeated K-fold cross-validation using random search on the hyperparameters. This allowed for 15000 total fits on the model to find the optimal hyperparameters. 

The best model was as follows:

```python
GradientBoostingRegressor(learning_rate=0.05, max_depth=2.0, n_estimators=100, min_samples_leaf=0.1, min_samples_split=0.1)
```



## Results
The results of our analysis are quite interesting. After selecting the final model with the optimal hyperparameters, we found that the model predicted adequately, but not incredibly well. Its out-of-sample cross-validated root mean squared error (RMSE) was 58.96s, which is lower than the standard deviation of 64.54s, so we can reliably say that our model predicts better than the average. Additionally, our in-sample RMSE was 55.92s. Because GBM's don't have a true R^2 statistic, we don't report one here. Since the model fits the data, as can be seen by the relatively small RMSE, we can use it for limited inference. Based on the variable importance output by the model, the number of previous models is the most important variable, followed by the last marathon time run, the age of the athlete, and the year the race was held. In addtion, we can use the partial effect plots generated by Python to find additional inference. In essence, these plots show the marginalized increase or decrease that a variable has on the outcome and can be useful for interpreting tree ensembles. The following plot describes the effect of the number of previous marathons run. As could be expected, a higher number of previous top 1000 performances correlates with faster times, since the athlete is likely incredibly fast and consistent. This is shown by the steep downward trend of the plot.

![image](https://user-images.githubusercontent.com/58056607/145109986-16601288-c3dc-4e54-a9fa-bd67db61da2e.png)

Even though GDP wasn't a very important variable, it is interesting to visualize the effect that is often stereotyped in running of Kenyans and Ethiopians being great in running, as reflected by the steep drop at the beginning of the plot.

![image](https://user-images.githubusercontent.com/58056607/145110090-665878de-36fd-4823-b40d-f109fb4cb8c1.png)

This plot shows the effect of age on the times of runners. As could be expected, the older the athlete, the slower they run. This is also quite interesting considering that many past world record holders transferred to the marathon only upon 'aging out' of traditional track events due to the slowing effect of age.

![image](https://user-images.githubusercontent.com/58056607/145110181-5b4b751e-4b6f-4a1d-97cb-284a56378de9.png)

Finally, as a cautionary tale, we present our prediction results for the 2021 Olympics. It should first be noted that Olympic marathons rarely result in all-time top 1000 race times because the athletes are more focused on placing than time. Therefore, the predictions of our model should not come as a surprise. Using the model trained on the top 1000 marathon performances ever, we had an RMSE of 775s, which is terrible compared to the standard deviation of the data of 384s. The reason for this is clearly explained by the mean bias of the predictions of -685s. Therefore, our model consistently predicts as if the Olympic marathon would result in many top 1000 all-time race times because it was trained on that data. Therefore, our predictions are not comparing 'apples to apples', which explains why they are so bad. In order to combat this, we would need to train our model instead on previous Olympic marathon data, which we don't have access to as of this report.




## Conclusion
