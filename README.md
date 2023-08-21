# Predicting Customer Churn for SyriaTel

## I. Overview

Our client is SyriaTel, which is a telecommunications company. SyriaTel is facing the problem of customer churning, which causes a loss in profits. In order to address this, SyriaTel wants to offer customers that are likely to churn special benefits in order to maintain their business and ensure a long-term relationship. SyriaTel has presented us with customer data and asked us to build a model to predict customer churn. This model will, in turn, provide the client with a method to identify which customers to conciliate.

Below we'll explore and analyze the data, then use machine learning algorithms to build a model that will predict customer churn. 

## II. Data 

The data used for this project contained 3,333 entries, which each represent a different customer. There are also 21 distinct features, one of them being churn (and this will be our target). The other 20 columns represent various details about the given customer, including the customer's state and service usage. They can be grouped into a few subsets: 
* **Customer information:** this includes the features such as state, area code, phone number, etc.
* **Plan information:** this includes the details of the plan of a given customers. The features here are international plan and voicemail plan.
* **Usage and charges:** this accounts for the bulk of the features, and includes the features for amount of calls, minutes and charges. This also includes international usage and charges.
* **Customer service interaction:** this is the column customer service calls, and shows how many times the customer reached out to customer service.

## III. EDA 

We explored the data and found a few meaningful relationships between the features and churn. 

### A. Introductory note: we have imbalanced data
![bar_plot_1](https://github.com/bmjaron/phase_3_project/assets/115658357/0565c4ef-6974-4148-8e68-c678ea6a654c)

We see that only 14.5% of customers churn. This is something that we'll have to account for as we process the data for modeling.



### B. Relationship between customer service calls and churn

One would expect that a customer service calls is less happy with the service, and therefore more likely to churn. Our data confirmed this assumption.
