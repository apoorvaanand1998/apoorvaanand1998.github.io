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

How do we fit all those multiple features to our data? Of course! We use gradient descent. Now, since we're still using _linear_ regression, our cost function remains the same. So, partially differentiating w.r.t all Q's, we get the following algorithm for calculating the parameters in multivariate linear regression : 

![Parameters for multivariate linear regression](/img/PMLR "Parameters for multivariate linear regression")

We can speed up gradient descent by having each of our input values in roughly the same range. Ideally - -1 <= x(i) <= 1.

There are two techniques that help with this - feature scaling and mean normalization. 

### Feature scaling 

Feature scaling involves dividing the input values by the range (i.e. the maximum value minus the minimum value) of the input variable.

### Mean normalization

![Mean normalization formula](/img/MN.png "Mean normalization formula")

Where u_i is the average value of that feature, and s_i is the range or standard deviation. We don't apply this to x0 because x0 - u_0 = 0.

## Choosing the right learning rate and knowing when to stop running the algorithm

If one has chosen the right learning rate then after plotting number of iterations against J(Q) (The cost function), we should get the cost function to flatten i.e. the gradient descent has converged at the minimum, and that means we can stop running the algorithm. 

Now, if the cost function, instead of decreasing every iteration, decides to increase or oscillate then we should decrease our learning rate (while keeping in mind that if we decrease it too much, then the algorithm will be slow).

## Adding new features to get a better model 

We can combine multiple features into one. For example, we can combine x1 and x2 into a new feature x3 by taking x1⋅x2 if we think that x3 is a more important feature for the model we are building.

### Polynomial regression

Our hypothesis function need not be linear (a straight line) if that does not fit the data well. We can change the behavior or curve of our hypothesis function by making it a quadratic, cubic or square root function (or any other form). This means knowing the shape of different functions helps! 

For example, if our hypothesis function is h(x) = Q0 + Q1.x1 then we can create additional features based on x1, to get the quadratic function h(x) = Q0 + Q1.x1 + Q2.x1.x1 or the cubic function h(x) = Q0 + Q1.x1 + Q2.x1.x1 + Q3.x1.x1.x1

In the cubic version, we have created new features x2 and x3 where x2 = (x1)^2 and x3 = (x1)^3.

To make it a square root function, we could do - h(x) = Q0 + Q1.x1 + Q2.((x1)^(0.5))

One important thing to keep in mind is, if you choose your features this way then feature scaling becomes very important.

## Normal equation

The normal equation method is used to compute the parameters analytically as opposed to iteratively (using gradient descent). 

Q (Parameter matrix) = ((X'.X)^(-1)).X'.y (Here the inverse is always done using 'pinv' in octave, this is done in case X'.X is not invertible)

where y is the vector that contains all the output/target variables and each row in X is the transpose of the feature vector for all input variable/features (called the design matrix). 

When you use the normal equation method to compute the parameters, feature scaling is not necessary. 

![X matrix](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/dykma6dwEea3qApInhZCFg_333df5f11086fee19c4fb81bc34d5125_Screenshot-2016-11-10-10.06.16.png?expiry=1513641600000&hmac=tJDVD9Jq_c-dbewUSsK7vFQFgk6pCEvyNTFWfP6ZCdg "Finding out the X matrix")

| Gradient descent | Normal equation |
| :--------------- | :-------------- |
| Need to choose alpha	| No need to choose alpha |
| Needs many iterations	| No need to iterate |
| O (kn^2) |	O (n^3) | 
| Works well when n is large |	Slow if n is very large |

Next up, programming assignment - 1! I'm scared, but also excited.
