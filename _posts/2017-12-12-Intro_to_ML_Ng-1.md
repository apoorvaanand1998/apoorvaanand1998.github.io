---
layout: post
title: Introduction to Machine Learning - 1
subtitle: Am I actually doing this?
tags: [Computer Science, Machine Learning, Andrew Ng]
---

This is it. This is my first post. Let's begin.

Applications of machine learning :
* Ranking webpages.
* Facial recognition. 
* Filtering spam.
* Database mining - Large datasets from growth of automation/web (Web click data, medical records, biology, engineering).
* Applications that can't program by hand (Autonomous helicopter, handwriting recognition, NLP, Computer Vision).
* Self-customizing programs (Amazon, netflix recommendations).
* Understanding human learning.

## What is machine learning?

Field of study that gives computers the ability to learn without being explicity programmed. 

A well-posed learning problem: A computer program is said to learn from experience E with respect to some task T and some performance measure P, if its performance on T, as measured by P, improves with experience E. 

Two main types of learning algorithms :
1. Supervised learning - Teach the computer how to do something.
2. Unsupervised learning - Learns by itself.

## Supervised learning

"Right answers" are given - Dataset with known valued (right answers) given. Task of the algorithm to produce more of these "right answers". 

In supervised learning, we are given a data set and already know what our correct output should look like, having the idea that there is a relationship between the input and the output.

Types :
* Regression - Predict continuous valued output.
* Classification - Predict discrete valued output. 

## Unsupervised learning

In supervised learning, we are told explicitly what the "right answer" is. In unsupervised learning, the datasets have no "labels". "Here's a dataset - Can you find some structure in the data?" is the question that unsupervised learning algorithms seek to answer.

Unsupervised learning allows us to approach problems with little or no idea what our results should look like. We can derive structure from data where we don't necessarily know the effect of the variables. We can derive this structure by clustering the data based on relationships among the variables in the data. With unsupervised learning there is no feedback based on the prediction results.

Types :
* Clustering: Take a collection of 1,000,000 different genes, and find a way to automatically group these genes into groups that are somehow similar or related by different variables, such as lifespan, location, roles, and so on.
* Non-clustering: The "Cocktail Party Algorithm", allows you to find structure in a chaotic environment. (i.e. identifying individual voices and music from a mesh of sounds at a cocktail party).

## Linear regression with one variable

The "linear" in linear regression comes from trying to fit the values of the dataset into a straight line i.e. into a linear function. 

In supervised learning, the dataset used for "learning" is called the training set. 

Notation :
* m = Number of training examples
* x = "Input" variable/features 
* y = "Output" variable/"Target" variable (what you're trying to predict)
* (x, y) - Particular training example
* (x(i), y(i)) - Refers to the i-th entry of the training set (It's actually (x^(i), y^(i))

![Supervised learning flowchart](http://images.slideplayer.com/25/7764095/slides/slide_4.jpg "Supervised learning flowchart and Univariate linear regression function")

Why is linear regression represented by h(x) = Q0 + Q1(x)? Remember y = mx + c?
Here Qi's are known as the "parameters" of the model (Q is actually supposed to be "theta", and (0 and 1) in (Q0 and Q1) are subscripts).

In linear regression, we need to come up with values for Q0 and Q1 so that the straight line that we get corresponds or fits to the data well. How do we know it fits well? The idea is to choose Q0 and Q1 so that h(x) is close to the y's we already know from our training set. 

We can do this by minimizing Q1 and Q2 over a cost function. For most linear regression problems, the **squared error cost function** works well. There are other cost functions as well. 

## Cost Function 

![Squared error cost function](https://i.stack.imgur.com/O752N.png "Squared error cost function")

We can measure the accuracy of our hypothesis function by using a cost function. This takes an average difference (actually a fancier version of an average) of all the results of the hypothesis with inputs from x's and the actual output y's.












