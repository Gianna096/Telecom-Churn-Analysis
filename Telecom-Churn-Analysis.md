# Telecom-Churn-Analysis
Customer churn has a huge impact on companies and is the prime focus area for the companies to remain competitive and profitable. It has been observed across multiple industries that it is far easier to retain a customer than to secure a new customer and the telecom industry is no different. Thus, it is vitally important to understand the dynamics of customer churn.  

Looking at the stiff competition in the telecom industry and the ever-increasing demand for high quality yet affordable network plans motivated us to conduct an analysis to study the factors which play a crucial role in determining the *churn* or *no-churn*. 

In this project, we set out to develop a model which would accurately classify a customer as someone who would churn or not so that the telecom companies could use strategic methods to offer lucrative plans to the customer for preventing the churn before it actually does happen. Losing a customer without getting an understanding about the reasons for churn would not help in improving the churn rates. This analysis could be leveraged by the telecom companies to take proactive measures and it would also provide them the opportunity to reach out to customers before they churn to better understand their needs and concerns so that they could make the necessary adjustments.

**Data Description**

The dataset on Telecom Churn analysis had 7043 rows and 21 columns. The predictor variables in the dataset had information about customer demographics (like gender, age etc.), information about the services customers have subscribed for and the cost incurred by the customer. The dataset had few missing values which were dropped reducing the dataset to 7032 rows and 21 columns.

During Exploratory Data Analysis, we found some interesting details like senior citizens on average pay higher monthly bills than others (Refer to Figure 6) and people with annual contracts are less likely to churn as compared to people with monthly contracts (Refer to Figure 7).

<p align="center">
  <img width="560" height="300" src="https://github.com/Gianna096/Telecom-Churn-Analysis/blob/main/figures/Figure%206.png">
</p>

<p align="center">
  <img width="560" height="300" src="https://github.com/Gianna096/Telecom-Churn-Analysis/blob/main/figures/Figure%207.png">
</p>

PointPlots (Refer to Figure 8) illustrated that the customer who churned paid significantly lower total charges, irrespective of type of internet service, as compared to people who did not churn but for the contract type, things are opposite. Exploratory data analysis gave us a clear insight that people tend to churn less with increase in tenure (Refer to Figure 9).

<p align="center">
  <img width="560" height="300" src="https://github.com/Gianna096/Telecom-Churn-Analysis/blob/main/figures/Figure%208.png">
</p>
<p align="center">
  <img width="560" height="300" src="https://github.com/Gianna096/Telecom-Churn-Analysis/blob/main/figures/Figure%209.png">
</p>

In order to increase the usability of the dataset, we performed extensive feature engineering for all the predictor variables. Feature engineering for categorical variables was performed using the one-hot encoding technique. Feature engineering for numeric variables was performed using log features, polynomial features and interaction terms. The concatenated dataset had 11 columns, then we dropped original categorical variables from the dataset to reduce the redundant information in the dataset giving us the dataset with 7032 rows and 84 columns. Following this, we performed min-max standardization to make sure that the scale of certain numeric features does not have an impact during modeling.

The original dataset had only 26% rows for churn events which would have made it tough for our model to be able to predict churn events on test data or a new dataset (Refer to Figure 11). Therefore, we used undersampling technique to balance out the churn and no-churn events. We had a ratio of 1:1 for churn and no-churn in the dataset which we finally used for modeling.

<p align="center">
  <img width="460" height="400" src="https://github.com/Gianna096/Telecom-Churn-Analysis/blob/main/figures/Figure%2011.png">
</p>

During the data preparation phase, we experimented with the stratify method as well to make sure that the train and test data had similar ratio of churn and no-churn but as it turned out stratify wasn’t able to resolve the imbalance in the dataset and the models were not performing great at predicting churn, though the models were doing great while predicting no-churn.


**Model Description**

Modeling dataset with 3738 rows and 84 columns was split into training and validation in the ratio of 80:20 with stratified target variable. We followed the 4 steps to the models to get an optimized prediction result:

1. **Spot-checking** - to discover the algorithm which was best suited to solve the business problem.
We used Logistic Regression, Linear Discriminant Analysis, KNN, Decision Tree Classifier, Gaussian Naïve Bayes, SVC, Bagging Classifier, Random Forest Classifier, Extra Trees Classifier, Gradient Boosting Classifier for spot-checking. Logistic Regression yielded best results for the classification problem with an overall highest accuracy. 

2. **Hyperparameter** tuning - to modify parameters in the logistic regression and linear discriminant analysis. 
For Logistic Regression, we tuned penalty and solver parameters and for Linear Discriminant Analysis we tuned solver and tolerance.

3. **Permutation feature importance** - to get insights about the importance of each variable used in the model. 
This step gave us the insight that the features like contract-type, gender, payment methods and the services subscribed by the customer played a vital role in making predictions. On the other hand, seemingly important features like monthly charges and total charges paid to the telecom company during the entire length of stay with the company were less important features.

4. **Implementation of results of permutation feature importance on logistic regression model**. With only important features, the LR model yielded a recall value of 83% which was more than the tuned logistic regression with all the features. 

5. **Furthur improvement: Neural network model**
Neural Network yielded exceptional results on training data with accuracy of predicting churn in 89% and on validation data it was 80% (Refer to Figure 3-5 and Figure 3-6). We used two hidden layers in the neural network which was a good trade-off between the model accuracy and the model execution time.
 
<p align="center">
  <img width="460" height="500" src="https://github.com/Gianna096/Telecom-Churn-Analysis/blob/main/figures/Figure%203-5%2C3-6.png">
</p>

**Results**
We implemented spot-checking with 10 different models to determine the algorithm which was best suited to solve the business problem. Our criteria for the best models was based on total accuracy and recall while considering overall model complexity. The logistic regression had a recall rate of .80, giving an accuracy of 0.76. The second best model was linear discriminant analysis which had an accuracy of 0.76.  (Refer to Figure 1 and Figure 3-1)

<p align="center">
  <img width="460" height="300" src="https://github.com/Gianna096/Telecom-Churn-Analysis/blob/main/figures/Figure%201.png">
</p>

With the aim of having the least number of false positives, we tried to reduce this type of misclassification. As it is evident by the confusion matrix of logistic regression, we get true negative 286 which are the customers which will certainly not churn. These customers could be targeted to increase the revenue for the telecom company. Also, this model gives the highest number of true positives - 299, which is the highest when compared to the result produced by other models.

Hyperparameter tuning for logistic regression further improved the performance of the model. As we see in the confusion matrix for tuned logistic regression model, we get an accuracy rate of 0.77 and get a higher recall rate of 0.82 compared to the previous model. (Refer to Figure 3-2, Table1)
<p align="center">
  <img width="460" height="300" src="https://github.com/Gianna096/Telecom-Churn-Analysis/blob/main/figures/Figure%203-2.png">
</p>
After using hyperparameter tuning and based on the results in the confusion matrix, we decided that the best model is logistic regression. Subsequently, we performed permutation feature importance to get insights about which variables played a significant role in the model result. Based on the plot of permutation feature importance, we recognized the variables having most positive and negative affect on the model accuracy. (Refer to Figure 4)
<p align="center">
  <img width="460" height="300" src="https://github.com/Gianna096/Telecom-Churn-Analysis/blob/main/figures/Figure%204.png">
</p>
We refined our model based on these recognized variables. At this time, we included only important features for building a classification model. We build a model in two ways. First, we built a model with top 20 variables which gave an overall accuracy of 0.74 and 0.75 recall. Next, we built which had all the features except the least important 30 variables. It returned an overall accuracy of 0.78 and recall of 0.83. Finally, we concluded that dropping features of lesser importance gives better results. (Refer to Figure 3-3, Figure 3-4)
<p align="center">
  <img width="460" height="300" src="https://github.com/Gianna096/Telecom-Churn-Analysis/blob/main/figures/Figure%203-3.png">
</p>
<p align="center">
  <img width="460" height="300" src="https://github.com/Gianna096/Telecom-Churn-Analysis/blob/main/figures/Figure%203-4.png">
</p>
**Discussion**
Customer churn has a huge impact on companies and is the prime focus area for the companies to remain competitive and profitable. Hence, significant research had been undertaken by researchers worldwide to understand the dynamics of customer churn. Customer churn has a huge impact on companies and is the prime focus area for the companies to remain competitive and profitable. Hence, significant research had been undertaken by researchers worldwide to understand the dynamics of customer churn. Customer churn has a huge impact on companies and is the prime focus area for the companies to remain competitive and profitable. Hence, significant research had been undertaken by researchers worldwide to understand the dynamics of customer churn. Churn in the telecom industry, as defined by Berson et al. (2000), is the movement of existing customers from one service provider to another. Customer churn is basically the inclination of a customer to leave a service provider (Phadke et al., 2013; Kirui et al., 2013; Chandar et al., 2006; Coussement and Poel, 2008; Buckinx and Poel, 2005; Bhambri, 2013; Xie et al., 2009; Chen et al., 2012).
Reichheld and Sasser (1990) researched that the revenue earned from retained customers increases over the period. This is pretty intuitive because if a customer has stayed loyal to a telecom company for a long time he must be satisfied with the products and services offered by the company and hence he would not shy away from opting for newer and higher priced services. On the flip side, companies tend to restore to the strategy of offering great pricing to new customers to build the relationship which is not the case in case of loyal customers. 

For current customers, companies tend to market their premium products and premium plans which would increase the revenue for the telecom company. 10
Other researchers divided the customer types into a postpaid and prepaid customer. As prepaid customers do not contract with service, so it is quite difficult to predict this kind of customer’s churn rate. As they researched prepaid customers, they found that network coverage and reception quality might influence customers to move to another company with a broader reach and better reception quality. Factors such as packaging prices, inadequate features, and older technology can also cause customers to leave the company service. Customers often compare their company services with others and churn to whoever they feel provides better overall value. When they divided the customer types into two types, they found that customers who did not have loyalty yet, they can leave the service for the simple reason. Thus, the company should propose, investigate, and design the strategy in a multidimensional way.

**Conclusions and Next Steps**
Based on our splitting rules of our interactive Tree, we found that “Contract”, “Tenure”, “internet service” variables play an integral role in predicting the churn rate. Refer to Figure 5, Appendix. These facts will help Telecom to identify in advance what kind of customers are more likely to leave the company and identify the risk in advance. This gives Telecom companies an opportunity to take proactive measures to retain the customers before they actually churn.

As we have observed in our analysis, features like tenure, monthly charges, type of contract and payment method are significant features which determine if a customer would churn or not. Telecom companies should try to promote annual and two-year contracts to the new customers as it will reduce the chances of customer churn right away. They could offer plans with premium services at a lower cost along with an annual contract which would encourage new customers to purchase an annual contract. It is highly recommended that Telecom companies adopt different 11 approaches for each type of customer as having the same strategy for everyone would not help in reducing the churn rates. In case of a new client, the company should focus on establishing long term relationships. 

For the existing customers, Telecom companies should provide bonuses or rewards so as to keep the customers interested and motivated to keep using the company's services. Permutation feature importance once again emphasizes that “monthly charges'', “tenure * monthly charges” and “Total charges” are significant variables in determining the churn rate so it is important for telecom companies to be strategic while pricing the products and services. One of the best strategies to retain an existing customer is to consistently offer bonuses and other rewards. Additionally, it is important to provide customized plans and personalized services based on customer’s service usage behavior.

The next step would certainly be to focus on increasing the accuracy in predicting the customers who are likely to churn (False Negative) to help address the business problem efficiently. Moreover, we have observed that the neural network does not significantly improve the accuracy of recall so it needs further discussion if it is worth complicating the model and degrading the execution time for the sake of minimal improvement in the accuracy.
