# Analysing and Predicting Perth Home Prices

<img src="https://raw.githubusercontent.com/ricardocmuller/Perth_House_Prices_Analysis_and_Predictions/main/images/perth%20house%20prices%20.PNG" width=100%>

The goal of this project is to better understand the __significance of certain features__ on a __house's price__ in the Perth Metropolitan Area (Western Australia), and conducting a comparison between __character homes__ and __new homes__.

The following key questions will be answered:

1. What is the distribution of Perth house prices? 
2. Are older homes generally more expensive than newer homes?
3. What features have strongest correlation with price, and does this differ between older and newer homes?
4. What features are most important in predicting a house's price?


## This repo includes the following:

- "_Perth_House_Prices_Analysis_and_Predictions.ipynb_" - Jupyter notebook showcasing Python data pre-processing workflow with the raw CSV file, data manipulation, exploration and analysis, machine learning model training and evaluation.

- "_all_perth_house_sales_310121.csv_" - Raw CSV file containing Perth house sales data sourced from [here](https://www.kaggle.com/syuzai/perth-house-prices).

- "_House Sales Data (Cleaned).csv_" - The pre-processed dataset with missing values imputed and outlier values addressed.

- "_Perth House Sales Data - Analysis.pbix_" - Power BI Desktop document for data visualization and further analysis that uses the pre-processed version of CSV file.

- "_Perth House Sales Data - Analysis.pdf_" - PDF report exported from the Power BI document.


## Insights

Below are some of the main insights and visualizations of this project, although the __Jupyter notebook is far more thorough and captures the associated code in pre-processing the data and training the machine learning model__:

### __Insights on PRICE Distribution__

<img src="https://raw.githubusercontent.com/ricardocmuller/Perth_House_Prices_Analysis_and_Predictions/main/images/perth%20house%20prices%20.PNG">

<img src="https://github.com/ricardocmuller/Perth_House_Prices_Analysis_and_Predictions/blob/main/images/probability%20density%20function.png?raw=true" width=75%>

- The two newly created datasets derived from the __houses_df__ DataFrame have different numbers of observations with __houses_pre_1950_df__ having 2,062 observations, and __houses_post_1950_df__ having 31,594, which makes sense given the construction of properties has increased with the passing of time to meet growing population numbers.

- The <code>PRICE</code> feature is right skewed and not normally distributed, with probabilities tapering off more slowly for expensive homes.

- Most property prices in the dataset sit between \$400,000 and \$450,000, with a median of $535,500.

- Character homes are generally more expensive than New homes, with a greater proportion of homes in the dataset having a higher price tag. The median price of a character home is also notably higher than a new home.


### __Insights on Feature Correlation__

<img src="https://github.com/ricardocmuller/Perth_House_Prices_Analysis_and_Predictions/blob/main/images/correlation.png?raw=true" width=60%>

<img src="https://github.com/ricardocmuller/Perth_House_Prices_Analysis_and_Predictions/blob/main/images/feature%20correlation%20df.PNG?raw=true">

- A house's <CODE>PRICE</CODE> generally has the strongest correlation with <CODE>FLOOR_AREA</CODE>, followed by the number of <CODE>BATHROOMS</CODE> then number of <CODE>BEDROOMS</CODE>. All of these are indicators of the size of the house, and their positive correlation with <CODE>PRICE</CODE> suggests that larger houses with additional rooms are (understandably) more expensive.

- <code>BUILD_YEAR</code> has also been shown to have a weak negative correlation with house price, which indicate that older homes generally have slightly higher prices.

- The correlation of features with <code>PRICE</code> is fairly consistent in the different DataFrames, although <code>BEDROOMS</code> has a higher correlation with <code>PRICE</code> in older homes.


### __Insights on the impact of Floor Area on Price__

<img src="https://github.com/ricardocmuller/Perth_House_Prices_Analysis_and_Predictions/blob/main/images/average%20Perth%20suburb%20property%20price%20and%20floor%20area.png?raw=true">

- Larger homes are generally more expensive.

- Character homes on average have higher prices than new homes of the same size. This is captured through how the blue dots are generally located below the orange dots (i.e. new homes have lower price), yet they share the same or very similar floor area. The linear regression model fit further solidifies this.

- Therefore, the price per square metre of an older home is generally higher than that of a new home.


### __Insights on Machine Learning Modelling__

![ml model metrics](https://user-images.githubusercontent.com/95157802/211782399-d22d1617-8457-48e4-b8f9-95f941107443.png)

![feature importance](https://user-images.githubusercontent.com/95157802/211782429-3afe5a41-bbb9-4b3f-9643-e8476cdc8f20.png)

![actual vs predicted describe](https://user-images.githubusercontent.com/95157802/211782483-6a44d325-dcb2-4b3e-8a67-7f5c8ab9c055.png)

- The best machine learning model from the models experimented with is the ensemble learning method RandomForestRegression.

- Fine tuning the model with the hyperparameters in the hyperparameter grid search shows a very slight improvement to the model performance, with a final R-squared value of 0.8096, and Root Mean Squared Error (RMSE) of $153,257.

- The 3 most important features in the model which have larger effect on the <code>PRICE</code> target variable were determined to be <CODE>POSTCODE</CODE>, <CODE>FLOOR_AREA</CODE> and <CODE>CBD_DIST</CODE>.

- When comparing the actual and predicted prices, the Mean, 25th, 50th and 75th percentiles are notably close, however the Min, Max and Std show larger discrepancies. This implies the model typically performs better for observations with commonly observed values, but underperforms on outliers and more extreme data.



### __Insights from visualizing Predicted vs Actual values for home Prices__

![actual vs predicted scatter](https://user-images.githubusercontent.com/95157802/211782808-82e9f69c-259a-4a36-b750-9b3ce0eccac0.png)

![actual vs predicted prob density](https://user-images.githubusercontent.com/95157802/211782831-f9d686ac-519e-42af-a8ba-1644eb27448a.png)

![prediction error amount hist](https://user-images.githubusercontent.com/95157802/211782847-c305471f-156e-4187-af3d-54f68e635232.png)

- The model generally performs better on observations that have more commonly observed values, and the predicted values take on a positively skewed distribution that closely follows the actual price distritbution.

- The model predicts there are more properties with commonly observed price values than there actually are. It also underperforms on observations which take on more extreme lower values, such as house prices between \$0 and $250,000. This could be due to the lack of sufficient observations in this lower price range during training.

- Model prediction errors follow a similar shape to a normal distribution with a mean error of -3,945.46 (which is close to 0 given the range of potential house prices), meaning there is an almost equal amount of positive and negative discrepancies between the predicted and actual values (error values to either side of the mean).

- 68% of errors (within 1 standard deviation of the mean) between the actual and predicted values are between -\$157,162 and $149,272.


## __Conclusion__

This study has allowed for a deeper look into Perth property prices and the effect features have on these prices through the visualization and re-expression of the data. 

It has reinforced how character homes are on average more expensive than newer homes that may share some of the same features, with the price per square metre of a character home being typically higher than that of a new home of the same size. The year of construction has also been shown to have a weak negative correlation with house price, meaning that older homes generally have slightly higher prices.

The machine learning model developed reveals that <code>POSTCODE</code>, <code>FLOOR_AREA</code> and <code>CBD_DIST</code> are the most important features in informing a property's price. <code>BUILD_YEAR</code> is only the 5th most important feature in the final model, meaning that the location of the house, its size, and its distance from the CBD are generally more telling of a home's price than the home's year of construction. 

The model does have room for improvement, however, especially to reduce its RMSE. Some strategies that could be experimented with involve: creating models specific to suburban or rural areas, training and testing against other model types, removing features that are potentially noisy, engineering new more informative features, or changing the definition of an outlier in the context of the study.
