---
layout: post
title:  Project
date:   2017-11-15
excerpt: "Predicting House Prices"
image: "/images/bank.jpg"
---

## Motivation

In the financial industry, the need for banks to better understand their customers has never been higher. PWC states that developing a customer-centric model has become the top priority for banks. This entails looking at the vast amount of information banks have on their customers, and leveraging on the data insights to a) create new products and b) to increase revenue by selling existing products more effecitvely.

I wanted to create a model that could predict whether a customer was likely to take up a financial product with the bank. 

## Success Metrics

The accuracy of the model, fitted on classifier models would serve as the metric for my project. 

## Data

Due to the sensitive nature of the information that banks have on their clients, good data sets are hard to come by. I used the UCI Machine Learning Repository's 'Bank Marketing' dataset, which contains 41187 rows and 21 features.                                                                                        

## Exploratory Data Analysis 

The dataset contains a mix of categorical and numerical features.

{% include image.html url="https://i.imgur.com/4W6kGIX.png" description="bankdf" %}
<br>
A quick look around at the dataset shows me the following:

{% include image.html url="https://i.imgur.com/RzKDplR.png" description="age" %}

The age group is skewed to the right, with most people in their 30s to 40s.

{% include image.html url="https://i.imgur.com/tDDng0p.png" description="campaign" %}

Most people were contacted less than 10 times for the current marketing campaign. The median was 2 times.

{% include image.html url="https://i.imgur.com/15LbmxF.png" description="previous" %}

Most of the customers have never been contacted before prior to this campaign.

### What months are best for marketing?
<br>
{% include image.html url="https://i.imgur.com/CG1q3uD.png" description="monthvc" %}

The three busiest months for marketing were in May, July and August, corresponding to the summer months. 

### Which features can best explain whether a customer is going to take a term deposit?

I performed some data preprocessing on the categorical data. Using patsy, I generated a dataframe that encodes each category as a feature. The result was that the original 20 features expanded to a set of 48 features.

I then took a look at the dataset in terms of how many successful calls there were (as compared to the unsuccessful ones). 

{% include image.html url="https://i.imgur.com/D3qFGMo.png" description="imba" %}
<br>
From the above it can be seen that the dataset is somewhat imbalanced, with only 4640 positive samples. 

Next up, I did a GridSearch of the dataset to determine the 'best hyperparameters', then used it to train a logistic regression model.

{% include image.html url="https://i.imgur.com/p06sMkF.png" description="gridsearch" %}

<br>
## Exploring Decision Trees

Decision trees are a non-parametric supervised learning method used for classification and regression. The goal is to create a model that predicts the value of a target variable by learning simple decision rules inferred from the data features. 

Depending on the data, decision trees can can split into many, many branches. I trained three models ofmax depth 1, 2 and 3. The decision tree with max depth = 3 is shown here}:

{% include image.html url="https://i.imgur.com/peCwmq8.png" description="dt" %}
{% include image.html url="https://i.imgur.com/Gdh2LCn.png" description="top feat" %}
<br>
The decision tree model had the effect of telling me that most of the engineered features are not predictive for determining whether a customer takes up the bank's term deposit. Therefore I will seek to refit the logistic regression model to see how (if any) the scores will change.

{% include image.html url="https://i.imgur.com/7kD8YNy.png" description="rus" %}

<br>
## Limitations, Conclusions and Thoughts

1. The dataset is small. There are many other data points that should be easily available, such as customers' salary, that if included, could lead to be better classification score.
2. Future marketing campaigns should focus on the young and elderly, while the months of March and May are the best time to ramp up the marketing activities.
3. When marketing, try to target those who have never been contacted in the previous campaign before.  


Source code for my project is [here.](https://github.com/ekbq/hello-world/blob/master/Capstone/Capstone%20-%20Clickbait.ipynb)
