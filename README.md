# Predicting Customer Churn for SyriaTel

**Author**: [Benjamin Jaron](mailto:bmjaron@gmail.com)

# Table of Contents
* [Overview](#I.Overview)
* [Data](#II.Data)
* [EDA](#III.EDA)
* [Modeling](#IV.Modeling)
* [Conclusions](#V.Conclusions)

# I. Overview

Our client is SyriaTel, which is a telecommunications company. SyriaTel is facing the problem of customer churning, which causes a loss in profits. In order to address this, SyriaTel wants to offer customers that are likely to churn special benefits in order to maintain their business and ensure a long-term relationship. SyriaTel has presented us with customer data and asked us to build a model to predict customer churn. This model will, in turn, provide the client with a method to identify which customers to conciliate.

Below we'll explore and analyze the data, then use machine learning algorithms to build a model that will predict customer churn. 

# II. Data 

The data used for this project contained 3,333 entries, which each represent a different customer. There are also 21 distinct features, one of them being churn (and this will be our target). The other 20 columns represent various details about the given customer, including the customer's state and service usage. They can be grouped into a few subsets: 
* **Customer information:** this includes the features such as state, area code, phone number, etc.
* **Plan information:** this includes the details of the plan of a given customers. The features here are international plan and voicemail plan.
* **Usage and charges:** this accounts for the bulk of the features, and includes the features for amount of calls, minutes and charges. This also includes international usage and charges.
* **Customer service interaction:** this is the column customer service calls, and shows how many times the customer reached out to customer service.

# III. EDA 

We explored the data and found a few meaningful relationships between the features and churn. 

## A. Introductory note: we have imbalanced data
![bar_plot_1](https://github.com/bmjaron/phase_3_project/assets/115658357/0565c4ef-6974-4148-8e68-c678ea6a654c)

We see that only 14.5% of customers churn. This is something that we'll have to account for as we process the data for modeling.



## B. Relationship between customer service calls and churn

One would expect that a customer service calls is less happy with the service, and therefore more likely to churn. Our data confirmed this assumption.

![download](https://github.com/bmjaron/phase_3_project/assets/115658357/f753bbe5-1ff1-42fb-8252-fc2b45625b5f)

![download](https://github.com/bmjaron/phase_3_project/assets/115658357/de6589a3-2f80-4297-af23-3531cec3ae8b)

## C. Relationship between daytime usage and churn

Usage obviously determines the amount that a customer gets charged. We found that daytime usage was highest, and so was daytime charge. We also found that the price/minute for daytime usage was highest. Our data showed that customers that churned incurred a higher daytime charge, in general, than those that did not churn. We hypothesize that daytime charge is a driver of churn. 

![download](https://github.com/bmjaron/phase_3_project/assets/115658357/eddf6230-287c-4141-86c8-4ec4784cf331)


![download](https://github.com/bmjaron/phase_3_project/assets/115658357/592db28e-f091-4559-b1bc-1421b8ae5f74)

## D. Type of plan and churn

There also is a relationship betewen the type and plan and churn. We noticed that customers with international plans churn in much higher proportion than those without an international plan. Similarly, customers with a voicemail plan churn in much higher proportion than those without a voicemail plan. 

![download](https://github.com/bmjaron/phase_3_project/assets/115658357/061d5964-74ef-432e-a5c8-be72e1b3454b)

![download](https://github.com/bmjaron/phase_3_project/assets/115658357/f2b396bc-0e3b-432d-8080-fd358185cfe0)


# IV. Modeling

## A. Overview (and a word about our scoring metric)

The model that we used was a XGBoost classifier, and we were able to achieve a recall score of 78%. 

We felt that recall, which is the ratio of predicted positives to true positives, was the most approriate method to score our model. This is because SyriaTel suffers financially from every customer that churns, and wants to identify customers that are prone to churning and attempt to retain them. Accordingly, false negatives are much more harmful than false positives. Every single false negative means that we missed an opportunity to retain a customer, whereas a false positive would mean giving discounts/benefits to a customer that wasn't going to churn. In our opinion, doling out benefits to those that don't need them poses less of a financial strain than losing customers and having to rebuild clientele. 

## B. Method to determine best model

In order to test our model, we broke our data into 3 sets. A training set, testing set and holdout set. For each model we tested, we used cross-validation to find the recall score of the training data, and then used the trained model to predict churn using the testing set, and again found the recall score. A discrepancy between the two would either be indicative of underfitting or overfitting. The model that had the best training/testing scores and least underfitting/overfitting was our XGBoost classifier. We then tested that model on the totally unseen holdout set, and calculated the recall score. Below is the confusion matrix for the testing and holdout sets. 

![download](https://github.com/bmjaron/phase_3_project/assets/115658357/301e6ae6-775e-4f93-a863-df1d0617d625)

As mentioned above, we found that our model had a recall score of roughly 78%. This was a slight deviation from the 81% recall score on the testing set, but was similar to the roughly 78% recall score for the cross-validation of the training data. Overall, we're encouraged by the consistency. 

![download](https://github.com/bmjaron/phase_3_project/assets/115658357/78c5e7c4-84df-4809-a56a-b4002b1b1092)

## C. Feature importance

Below is a plot of the feature importance. 

![download](https://github.com/bmjaron/phase_3_project/assets/115658357/07d16971-f380-48c7-8bc3-eb0ca26d9050)


We revealed during our EDA the relationships between international charges, daytime charges and customer service calls and churn. We were surprised to discover that the single most important feature in our model was voicemail plan. This is something to explore in the future. 

## V. Conclusions 

We recommend that SyriaTel use our model to predict churn, as we have a recall score of roughly 78%. In terms of how to remedy the situation, our EDA and modeling has shown that addressing the charges for daytime usage, international usage, and voicemail plan are a good place to begin. 


