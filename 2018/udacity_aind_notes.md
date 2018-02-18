# AIND udacity

##### Content    
[Overall](#overall)  
[HMM](#HMM)  
[Deep learning notes](#DL)  
[CNN contes](#CNN)  

<a name="overall"/>

## Overall

Using anaconda (conda). It helps to maintain several enviroments. Is it python-sprecific?

Using cloud computing power with GPUs. Possible option: https://aws.amazon.com/ru/ec2/. You pay for computational time.

<a name="HMM"/>

## HMM (hidden markov models).

Can be very useful. Trick to setup probability distributions inside nodes with some HMM configuration.

Helpful with analysing time series/data.

<a name="DL"/>

## Deep learing notes

Context: classification of points.

Perceptron trick: change weights of a linear function by coordinates of a point, use a class label to modify bias. Use a learning rate.

Perceptron algorithm: making iterations of perceptron trick.

To consider classification probabilities we can use sigmoid function: 1/(e^(-t) + 1).

Using error-function for a gradient descent. It should be continuous and differentiable.

Log loss function = -log(probability of correct classification). We should minimize it. We should use it to avoid probability multiplication and replace it with sum of logs.

Softmax function: e^(s_1) / (sum of e^(s_i)). It helps to move from scores to class probabilities.

Encoding: instead of enum, use boolean vector: is class 0, is class 1, ...

Likelihood: overall probability of smth. Likelihood -> max.

Cross entropy (CE): from max likelihood to minimum of -log(likelihood). CE = -sum(y_i * log(p(smth))). We can use CE for two classes or for multiclasses.

Logistic regression: sigmoid function over linear function with using CE. Algorithm: iterate points and go by gradient direction with a learning rate. 

Logistic regression vs preceptron algorithm: logistic regression trying to improve the score even in a context of correct classification.

In complicated cases we should consider non-linear models/functions.

TODO: #29

<a name="CNN"/>

## CNN notes

TBD
