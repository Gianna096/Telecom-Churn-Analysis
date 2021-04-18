# Telecom-Churn-Analysis
Customer churn has a huge impact on companies and is the prime focus area for the companies to remain competitive and profitable. It has been observed across multiple industries that it is far easier to retain a customer than to secure a new customer and the telecom industry is no different. Thus, it is vitally important to understand the dynamics of customer churn.  

Looking at the stiff competition in the telecom industry and the ever-increasing demand for high quality yet affordable network plans motivated us to conduct an analysis to study the factors which play a crucial role in determining the *churn* or *no-churn*. 

In this project, we set out to develop a model which would accurately classify a customer as someone who would churn or not so that the telecom companies could use strategic methods to offer lucrative plans to the customer for preventing the churn before it actually does happen. Losing a customer without getting an understanding about the reasons for churn would not help in improving the churn rates. This analysis could be leveraged by the telecom companies to take proactive measures and it would also provide them the opportunity to reach out to customers before they churn to better understand their needs and concerns so that they could make the necessary adjustments.

**Data Description**

The dataset on Telecom Churn analysis had 7043 rows and 21 columns. The predictor variables in the dataset had information about customer demographics (like gender, age etc.), information about the services customers have subscribed for and the cost incurred by the customer. The dataset had few missing values which were dropped reducing the dataset to 7032 rows and 21 columns.

During Exploratory Data Analysis, we found some interesting details like senior citizens on average pay higher monthly bills than others and people with annual contracts are less likely to churn as compared to people with monthly contracts. PointPlots illustrated that the customer who churned paid significantly lower total charges, irrespective of type of internet service, as compared to people who did not churn but for the contract type, things are opposite. Exploratory data analysis gave us a clear insight that people tend to churn less with increase in tenure.

In order to increase the usability of the dataset, we performed extensive feature engineering for all the predictor variables. Feature engineering for categorical variables was performed using the one-hot encoding technique. Feature engineering for numeric variables was performed using log features, polynomial features and interaction terms. The concatenated dataset had 11 columns, then we dropped original categorical variables from the dataset to reduce the redundant information in the dataset giving us the dataset with 7032 rows and 84 columns. Following this, we performed min-max standardization to make sure that the scale of certain numeric features does not have an impact during modeling.

The original dataset had only 26% rows for churn events which would have made it tough for our model to be able to predict churn events on test data or a new dataset (Refer to Figure 11, Appendix). Therefore, we used undersampling technique to balance out the churn and no-churn events. We had a ratio of 1:1 for churn and no-churn in the dataset which we finally used for modeling.

During the data preparation phase, we experimented with the stratify method as well to make sure that the train and test data had similar ratio of churn and no-churn but as it turned out stratify wasn’t able to resolve the imbalance in the dataset and the models were not performing great at predicting churn, though the models were doing great while predicting no-churn.


**Model Description**

Modeling dataset with 3738 rows and 84 columns was split into training and validation in the ratio of 80:20 with stratified target variable. We followed the 4 steps to the models to get an optimized prediction result:

1. Spot-checking - to discover the algorithm which was best suited to solve the business problem.
We used Logistic Regression, Linear Discriminant Analysis, KNN, Decision Tree Classifier, Gaussian Naïve Bayes, SVC, Bagging Classifier, Random Forest Classifier, Extra Trees Classifier, Gradient Boosting Classifier for spot-checking. Logistic Regression yielded best results for the classification problem with an overall highest accuracy. 

2. Hyperparameter tuning - to modify parameters in the logistic regression and linear discriminant analysis. 
For Logistic Regression, we tuned penalty and solver parameters and for Linear Discriminant Analysis we tuned solver and tolerance.

3. Permutation feature importance - to get insights about the importance of each variable used in the model. 
This step gave us the insight that the features like contract-type, gender, payment methods and the services subscribed by the customer played a vital role in making predictions. On the other hand, seemingly important features like monthly charges and total charges paid to the telecom company during the entire length of stay with the company were less important features.

4. Implementation of results of permutation feature importance on logistic regression model. With only important features, the LR model yielded a recall value of 83% which was more than the tuned logistic regression with all the features. 

5. Furthur improvement: Neural network model. 
Neural Network yielded exceptional results on training data with accuracy of predicting churn in 89% and on validation data it was 80%. We used two hidden layers in the neural network which was a good trade-off between the model accuracy and the model execution time.
