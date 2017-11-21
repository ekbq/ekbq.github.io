---
layout: post
title:  Capstone Project
date:   2017-11-15
excerpt: "Bank Marketing"
image: "/images/bank.jpg"
---

## Motivation

In the financial industry, the need for banks to better understand their customers has never been higher. PWC states that developing a customer-centric model has become the top priority for banks. This entails looking at the vast amount of information banks have on their customers, and leveraging on the data insights to a) create new products and b) to increase revenue by selling existing products more effecitvely.

I wanted to create a model that could predict whether a customer was likely to take up a financial product with the bank. 

## Success Metrics

{% include image.html url="https://i.imgur.com/Jnb0JQY.png" description="confm" %}

The accuracy of the model, fitted on classifier models would serve as the metric for my project. 

## Data

Due to the sensitive nature of the information that banks have on their clients, good data sets are hard to come by. I used the UCI Machine Learning Repository's 'Bank Marketing' dataset, which contains 41187 rows and 21 features.                                                                                        

## Exploratory Data Analysis 

The dataset contains a mix of categorical and numerical features.

{% include image.html url="https://ibb.co/mauViR" description="df" %}

A quick look around at the dataset shows me the following:

{% include image.html url="https://imgur.com/raelAUv" description="age" %}

The age group is skewed to the right, with most people in their 30s to 40s.

{% include image.html url="https://imgur.com/MKgrsn1" description="campaign" %}

Most people were contacted less than 10 times for the current marketing campaign. The median was 2 times.

{% include image.html url="https://imgur.com/sHIm5v0" description="previous" %}

Most of the customers have never been contacted before prior to this campaign.

### What months are best for marketing?

{% include image.html url="https://imgur.com/35DAkL1" description="monthvc" %}

The three busiest months for marketing were in May, July and August, corresponding to the summer months. 

### Which features can best explain whether a customer is going to take a term deposit?

I performed some data preprocessing on the categorical data. Using patsy, I generated a dataframe that encodes each category as a feature. The result was that the original 20 features expanded to a set of 48 features.

I then took a look at the dataset in terms of how many successful calls there were (as compared to the unsuccessful ones). 

{% include image.html url="https://imgur.com/1XPiN7Z" description="monthvc" %}

From the above it can be seen that the dataset is somewhat imbalanced, with only 4640 positive samples. 

Next up, I did a GridSearch of the dataset to determine the 'best hyperparameters', then used it to train a logistic regression model.

{% include image.html url="https://imgur.com/IhM8vym" description="lrcv" %}

## Exploring Decision Trees

Decision trees are a non-parametric supervised learning method used for classification and regression. The goal is to create a model that predicts the value of a target variable by learning simple decision rules inferred from the data features. 

Depending on the data, decision trees can can split into many, many branches. I trained three models ofmax depth 1, 2 and 3. The decision tree with max depth = 3 is shown here}:

{% include image.html url="https://imgur.com/uIPyVUs" description="dt" %}
{% include image.html url="https://imgur.com/q0vZbOe" description="top feat" %}

The decision tree model had the effect of telling me that most of the engineered features are not predictive for determining whether a customer takes up the bank's term deposit. Therefore I will seek to refit the logistic regression model to see how (if any) the scores will change.

{% include image.html url="https://imgur.com/pgHKQsy" description="rus" %}


## Limitations, Conclusions and Thoughts

This has been a very interesting project for me. My final thoughts on this are:

1. A good model relies on having a very large corpus of text to learn its vocabulary from. Compared to datasets used in standard packages in NLP (e.g. Glove), my corpus appears to be too small. But large datasets have a tradeoff in that they take significantly longer times and computing resources to train. I believe my model's level of accuracy is still acceptable, relative to the training time taken.
	2. The use of simplistic Naive Bayes classifiers in predicting clickbait articles can do most of the heavy lifting, getting up to 70% of the job done (after balancing the dataset). The use of neural networks can help, as seen in my use of a LSTM RNN model, but I wonder whether the model will do as well when exposed to a completely new corpus.
3. There are many potential areas for improvement. For one, there are already papers published on the use of character-level RNNs, where every token is a single letter in the corpus. I did not consider the implementation of this model since my project is a classification problem, not a text-generative one. Another way to refine the model would be to introduce additional feature engineering that may help in classifying, e.g. using POS(part-of-speech) tagging to allow the model to better understand context within a sentence. Last but not least. 
4. Text data is unstructured, messy and hard to preprocess. There are dozens of scenarios that a regex has to take into account for it to properly clean the data. It is also hard to visualize given its high-dimensionality. Many errors can be made in between the steps of preprocessing and model training, without an easy way to spot them.
5. At the end of the day, as with all models, (garbage in = garbage out). Admittedly, my preprocessing steps only sought to remove basic items such as punctuation and unicode format. I note that articles may sometimes contain email addresses and emojis. There were also several words with spelling errors that I did not correct. A thorough cleaning of the dataset should be able to factor in all the above to ensure a better score.

Source code for my project is [here.](https://github.com/ekbq/hello-world/blob/master/Capstone/Capstone%20-%20Clickbait.ipynb)
