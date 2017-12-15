---
layout: post
title: Introduction to Machine Learning - 2
subtitle: Multivariate linear regression 
tags: [Computer Science, Machine Learning, Andrew Ng]
---

What a mouthful, and it makes it sound so complicated.

Notation :
* n = Number of features (This was 1 in univariate linear regression)
* x(i) = Input feature*s* of i-th example (Now that there are multiple features, we get a vector here)
* x_j(i) = Feature j in i-th example

## What will be the new form of the hypothesis?

h(x) = Q0 + Q1.x1 + Q2.x2 + ... + Qn.xn

Consider an example of predicting the price of a house, we can think about Q0 as the basic price of a house, Q1 as the price per square meter, Q2 as the price per floor, etc. x1 will be the number of square meters in the house, x2 the number of floors, etc.

Let us introduce another feature x0, whose value = 1 (Now there are n + 1 features along with n + 1 parameters). Why are we introducing this? This is done because it allows us to conveniently represent the above equation in the form of vector multiplication. This is known as **vectorization**. 

![Vectorization of multivariate linear regression](/img/VMLR "Vectorization of multivariate linear regression")

## Gradient descent for multiple features

How do we fit all those multiple features to our data? Of course! Using gradient descent. Now, since we're still using _linear_ regression, our cost function remains the same. So, partially differentiating w.r.t all Q's, we get the following algorithm for calculating the parameters in multivariate linear regression : 

![Parameters for multivariate linear regression](/img/PMLR "Parameters for multivariate linear regression")

We can speed up gradient descent by having each of our input values in roughly the same range. Ideally - -1 <= x(i) <= 1.

There are two techniques that help with this - feature scaling and mean normalization. 

### Feature scaling 

Feature scaling involves dividing the input values by the range (i.e. the maximum value minus the minimum value) of the input variable.

### Mean normalization

![Mean normalization formula](/img/MNMLR.png "Mean normalization formula")

Where s_i is the range or standard deviation. 

