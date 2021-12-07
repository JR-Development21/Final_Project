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

## Model Description/Fit/Justification

## Results
![image](https://user-images.githubusercontent.com/58056607/145109986-16601288-c3dc-4e54-a9fa-bd67db61da2e.png)
![image](https://user-images.githubusercontent.com/58056607/145110090-665878de-36fd-4823-b40d-f109fb4cb8c1.png)



## Conclusion
