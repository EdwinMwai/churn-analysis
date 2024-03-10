# **churn-analysis**
--- 

## Project Overview
SyriaTel Communications, a telecommunications company, aims to anticipate and mitigate customer churn, wherein customers discontinue their services with the company. Customer churn poses a significant challenge for service-oriented businesses due to its financial implications. It not only results in the loss of recurring payments but also entails additional costs associated with acquiring new customers.


## **Business Understanding**

In today's competitive landscape, understanding and effectively managing customer churn is paramount for businesses aiming to sustain growth and profitability. A churn predictive model serves as a valuable tool in this endeavor by providing insights into customer behavior and predicting which customers are likely to discontinue their relationship with the company

The business understanding of a churn predictive model encompasses several key aspects:

**Identification of Churn Factors:** By analyzing historical data and customer interactions, businesses can identify the key factors that contribute to churn. These factors may include customer demographics, purchase history, usage patterns, satisfaction levels, and engagement metrics. Understanding these factors allows businesses to tailor their retention strategies to address specific customer needs and preferences.

**Proactive Intervention:** One of the primary objectives of a churn predictive model is to enable proactive intervention. By accurately identifying customers at risk of churn, businesses can implement targeted retention efforts to mitigate the likelihood of defection. This may involve offering personalized incentives, providing enhanced customer support, or introducing new product features to enhance customer satisfaction and loyalty.

**Resource Allocation:** A churn predictive model helps businesses optimize resource allocation by focusing their retention efforts on customers who are most likely to churn. By prioritizing high-risk customers, businesses can allocate their time, budget, and resources more effectively, resulting in a higher return on investment for their retention initiatives.

**Customer Lifetime Value:** Understanding churn dynamics is crucial for estimating and maximizing customer lifetime value (CLV). By accurately predicting churn, businesses can identify opportunities to extend customer relationships, increase repeat purchases, and maximize revenue potential over the long term.

## **Problem Statement**

Customer churn presents a significant challenge for businesses across various industries, leading to revenue loss and decreased market share. In order to mitigate this issue, there is a critical need to develop an effective churn prediction model that can accurately forecast which customers are at risk of leaving. This model should enable companies to intervene proactively with targeted retention efforts, thereby reducing churn rates and improving overall customer retention.

## **Main Objective**
Develop a reliable and precise predictive models capable of forecasting customer churn risks, enabling companies to intervene with tailored retention measures before customers defect. Utilize insights from these models to devise and execute impactful retention strategies, including targeted marketing initiatives, personalized incentives, enhanced customer service, and product enhancements.

### Specific Objectives
---

1. **Data preprocessing:** Cleanse and preprocess the data to handle missing values, outliers, and inconsistencies, ensuring the accuracy and  reliability of the predictive model.

2. **Feature selection:** Select relevant features that have a significant impact on churn prediction while reducing dimensionality and improving model performance.

3. **Model selection:** Evaluate various machine learning algorithms and statistical techniques to identify the most suitable model for predicting customer churn, considering factors such as accuracy, interpretability, and scalability.

4. **Model training and validation:** Train the chosen model on a subset of the data and validate its performance using cross-validation techniques to ensure generalizability and robustness.

5. **Hyperparameter tuning:** Optimize the parameters of the selected model using techniques such as grid search or random search to improve predictive accuracy and minimize overfitting.

6. **Evaluation metrics:** Define appropriate evaluation metrics, such as accuracy, precision, recall, F1-score, and area under the ROC curve (AUC), to assess the performance of the churn prediction model objectively.
---

# EDA

In addressing SyriaTel's customer churn issue, I initiated an Exploratory Data Analysis (EDA) followed by the development of a machine learning classifier. This classifier aims to forecast which customers are likely to churn, enabling SyriaTel to implement a proactive strategy to retain its customer base effectively.

During the exploratory data analysis (EDA) phase, I delved into the following inquiries:

* Does contacting customer service indicate dissatisfaction among customers or possibly foreshadow churn?
* To what extent are individuals utilizing their plans, and what insights can this usage offer regarding churn?
* Do customers residing in specific regions exhibit a higher propensity for churn?


## Does contacting customer service indicate dissatisfaction among customers or possibly foreshadow churn?
**Findings**

![Alt text!](visualizations\boxplot.png)

The current churn rate within our training dataset stands at approximately 14.5%. Upon analyzing customer service interactions, it becomes evident that as the frequency of these calls rises, so does the probability of churn. Notably, when customers make four or more service calls, the likelihood of churn escalates from roughly 10% to 50%.

**Recommendation:**
Going by these discoveries, it might be beneficial to consider providing a more substantial incentive or discount to customers who contact customer service more than three times.

## To what extent are individuals utilizing their plans, and what insights can this usage offer regarding churn?
**Findings**

![Alt text](Visualizations\histogram3.png)

![Alt text](Visualizations\histogram4.png)

It's evident that both the churned and non-churned customers maintained nearly identical usage patterns across day, evening, night, and international calls. Notably, the rates for international minutes remain constant at 27 cents per minute, irrespective of whether the customer possesses an international plan. Additionally, it's intriguing to observe that the churn rate was higher among customers with international plans compared to those without. This parity in international call charges suggests that churned customers with international plans might have perceived the plan's value differently, potentially leading them to believe that paying for the international plan wasn't worthwhile.

**Recommendation:**

Based on this analysis, I suggest adjusting the rates for international minutes such that Customers enrolled in an international plan should benefit from discounted rates for international calls compared to those without such a plan.

## Do customers residing in specific regions exhibit a higher propensity for churn?
**Findings**

![Alt text](Visualizations\histogram1.png)

It's evident that certain states exhibit significantly higher churn rates. When analyzed by state, Texas stands out with a notably higher churn rate than any other state, sitting at 27%. New Jersey, Maryland, and California also show elevated churn rates, exceeding 23%. Conversely, states with the lowest churn include Hawaii and Iowa, each below 0.5%.

### Other Findings From Our Visualizations

1. correlation

![Alt text](Visualizations\correlation.png)

It is evident that most features exhibit no correlation, some demonstrate perfect correlation. 

Specifically, the features "Total day charge" and "Total day minutes," "Total eve charge" and "Total eve minutes," "Total night charge" and "Total night minutes," as well as "Total int charge" and "Total int minutes" are fully positively correlated. This perfect correlation is logical example charges directly corresponds to the minutes used. 

The correlation coefficient of 1 indicates perfect multicollinearity, which affects nonlinear models differently than linear ones. While some nonlinear models may be impacted by perfect multicollinearity, others may not be affected.

2. Distribution of features

![Alt text](Visualizations\ditributions.png)

It is also evident that most features are normally distributed wit exception of customer service calls which was skewed to the right.

3. Class imbalance

![Alt text](Visualizations\output.png)

There is also class imbalance of the dependent varible which needed to be adressed

## Model Development

I started by developing a baseline model which was a logistic regression model. the model did not perform very well with the best metric being accuracy score at 0.75 and the others below 0.5.

Then I traine four differnt models on the same data set. The four model were:
- Random forest classifier
- Gradient boosting classifier
- Gaussian naive classifier
- SVC

I iterated through these four models using a function and output different metrics to help me pick the best model. 
The output metrics were precision score, accuracy score, recall score and f1 score. I also plot the confusion matrix for the better understanding of true positives, false positives, true negatives and false negatives. Out of the above models the Gradient boosting classifier performed better than the other models.

I decided to fine tune gradient boosting classifier

# Fine Tunning the model

I set a parameter grid to be used in the hyperparameter tuning. The parameters to be tuned were maximum depth, learning rate and n-estimator. I also set a cross validation of 5 folds.

The model metrics improved with recall score being 0.77 from 0.74, F1 score being 0.80 from 0.76 and ROC being 0.90.
This was the best that i could achieve from this model using this data set.


# Model Analysis


## Metric Used
In evaluating my model i used two metrics:

1. ROC(Receiver Operating Characteristic) curve analysis

I opted for employing ROC curve analysis to evaluate this model due to the following reasons:

* **Insights into Model Discrimination:** The ROC curve provide insights into the model's discrimination ability. A curve that is closer to the upper-left corner indicates better discrimination between churn and non-churn instances, while a diagonal line represents random guessing.
This also translates to high ROC score

* **Robustness to Class Imbalance:** ROC analysis is robust to class imbalance, which is a problem in this churn prediction tasks where the number of churned customers is significantly smaller than non-churned customers. By focusing on the true positive rate and false positive rate, ROC analysis gave insights into the model's performance regardless of class distribution.

2. Accuracy

I also opted to use accuracy because:

*  **Simplicity:** Accuracy is a straightforward scorevto understand and calculate, making it accessible to stakeholders with varying levels of technical expertise. It is the ratio of correctly classified instances to the total number of instances, providing a clear measure of overall model performance.

* **Intuitive Interpretation:** Accuracy represents the proportion of correct predictions made by the model, which is easy to interpret and communicate to stakeholders. Higher accuracy values indicate better predictive performance in identifying churned and non-churned customers.



## Model Fit & Score

![Alt text](Visualizations\roc.png)

The final model had the following validation ROC of 0.90

This value indicates better discrimination ability of the model which is approaching the maximum value of 1 for a perfect classifier.

This means that the final model has a high ability to distinguish between classes and its overall classification performance is also high across different threshold.

This model had an Accuracy of 0.94 which indicates that our model is able to predict correctly 94% 0f the cases and only miss 6%.


## Model limitations

In trying to fine tune the model to achieve better metrics score, i discovered that the model is easily overfitting on the training data. 
This was attributed by lack of enough data so that the model could generalize well.

## Recomedations

- In future i would recommend the we collect more data so that the model can perform better by reducing overfitting.
- I would recommend we get more data regarding competitors in states with higher churn rate and try to investigate their marketing strategy
- I would recommend we investigate on cell signal across the US to look for patterns in states with higher churn rate.
- i would also recomend we investigate the ability of the customer care representatives to handle the customers complaints and offer solution.

 




