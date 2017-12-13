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
* Applications that can't be programmed by hand (Autonomous helicopter, handwriting recognition, NLP, Computer Vision).
* Self-customizing programs (Amazon, netflix recommendations).
* Understanding human learning.

## What is machine learning?

Field of study that gives computers the ability to learn without being explicity programmed. 

A well-posed learning problem: A computer program is said to learn from experience E with respect to some task T and some performance measure P, if its performance on T, as measured by P, improves with experience E. 

Two main types of learning algorithms :
1. Supervised learning - Teach the computer how to do something.
2. Unsupervised learning - Learns by itself.

## Supervised learning

"Right answers" are given - Dataset with known values (right answers) given. Task of the algorithm to produce more of these "right answers". 

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

In linear regression, we need to come up with values for Q0 and Q1 so that the straight line we get corresponds or fits to the data well. How do we know it fits well? The idea is to choose Q0 and Q1 so that h(x) is close to the y's we already know from our training set. 

We can do this by minimizing Q1 and Q2 over a cost function. For most linear regression problems, the **squared error cost function** works well. There are other cost functions as well. 

## Cost function 

![Squared error cost function](https://i.stack.imgur.com/O752N.png "Squared error cost function")

**We measure the accuracy of our hypothesis function by using a cost function.** This takes an average difference (actually a fancier version of an average) of all the results of the hypothesis with inputs from x's and the actual output y's.

So, the smaller the value of the cost function, the better fit our line is to the training examples. How do we minimize the cost function? By using an algorithm called gradient descent. 

## Gradient descent 

Gradient descent is a general algorithm. What this means is, it is not only used to minimize the cost function of linear regression but is also used to minimize other functions. So we have our hypothesis function and we have a way of measuring how well it fits into the data (the cost function). Now we need to estimate the parameters in the hypothesis function. That's where gradient descent comes in. 

We put Q0 on the x axis and Q1 on the y axis, with the cost function on the vertical z axis. The points on our graph will be the result of the cost function using our hypothesis with those specific theta parameters. We will know that we have succeeded when our cost function is at the very bottom of the pits in our graph, i.e. when its value is the minimum.

![Graph described above](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/bn9SyaDIEeav5QpTGIv-Pg_0d06dca3d225f3de8b5a4a7e92254153_Screenshot-2016-11-01-23.48.26.png?expiry=1513296000000&hmac=GKjyEevxUsdOFKOG9bb4ANzT7fIi6ljk6L4f4oqcvcU)

To do the above, we use the gradient descent algorithm, which is :

![General gradient descent algorithm](https://2.bp.blogspot.com/-AdV-O-MoZHE/TtLibFTaf9I/AAAAAAAAAVM/aOxUGP7zl98/s1600/gradient+descent+algorithm+OLS.png "General gradient descent algorithm")

The alfa in the equation above is called the "learning rate", i.e. it tells us "how big a step" we take down from each point on the "hill" (i.e. how big a step we take while updating Qj). 

Here, both Q0 and Q1, i.e. for j = 0 and 1 are updated simultaneously. What this means is, we don't plug in the new value of Q0 into Q1 (or vice versa). We store both the values of of Q0 and Q1 in temp variables, and _then_ substitute the Q's for their temp variables. 

## Let's combine 'em!

By combining gradient descent with the cost function of linear regression, we get the algorithm for linear regression! 

![Parameters for linear regression](/img/LRGD "Parameters for linear regression")

To get the above, gradient descent looks at _every_ example in the training set on every step, and this is called **batch gradient descent**. Gradient descent leads to the local minima in general, fortunately linear regression has only one minima - the global minima and therefore, assuming the learning rate isn't too large, it will always converge to the global minima. 

And that's it! We've successfully learned our first machine learning algorithm.  


















