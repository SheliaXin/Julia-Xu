---
layout: default_post
title:  "Notes For Deep Learning"
date:   2017-09-05 12:05:54 +0800
meta: Summary of Course on Coursera and some useful Tips.
categories: Machine Learning
---


#### Neural Network framework:
1. Initialization of each parameters
2. Repeat:
    - Forward propagation (Compute z, a, yPred, loss)
    - Backward propagation (Compute gradients - dz, da; dw, db), and update parameters (gradient descent)

**Tips:**

  - If all $W^{[l]} <1$ or $W^{[l]} >1$ even slightly, the gradients will vanish/explode. We can reduce this problem by controlling the variance of $w$ during the initialization. For sigmoid, set $Var(w_i) = \frac{1}{n}$. For ReLu, set $Var(w_i) = \frac{2}{n}$. For tanh, set  $Var(w_i) =\sqrt{\frac{1}{n^{[l-1]}}} $ or $\sqrt{\frac{2}{n^{[l-1]} + n^{[l]}}}$.

  - Use [Gradient Checking](http://ufldl.stanford.edu/tutorial/supervised/DebuggingGradientChecking/) to debug. (See Details Course2 Week1)


#### Activation function: A Non-linear function
1. **tanh** function always works better than sigmoid function. tanh ( $tanh(z) = \frac{e^z - e^{-z}}{e^z +e^{-z}}$ ) function is a shifted version of sigmoid, but goes cross (0,0). The mean of its output is closer to zero, and so it centers the data better for the next layer.

2. When z is very small/large, both sigmoid & tanh has small slope. -> slow down gradient descent. -> **Use RELU** (rectified linear unit) (a = max(0,z)).

3. One disadvantage of RELU is that the derivative is equal to zero when z is negative (In practice, it works just fine. another version is **Leaky ReLu** (a = max(0.01z, z)), often works better, but not used widely).

**Tips:**

  - If you are doing binary classification, usually use sigmoid function as output layer.
  - On other layers RELU is often the default choice of activation function.

#### Regularization of Neural Network

Regularization is usually used to reduce overfitting.

1. Regularization with Frobenius Norm (weight decay), The cost function will be:

$$J(w^{[1]}, b^{[1]}, \dots, w^{[L]}) = \frac{1}{m} \sum_{i=1}^{m} L(\hat{y}^{(i)}, y^{(i)}) + \frac{\lambda}{2m} \sum_{l=1}^{L} \sum_{l=1}^{L} ||w^{[l]}||^2_{F}$$

where,
$$||w^{[l]}||^2_{F} = \sum_{i=1}^{n^{[l-1]}} \sum_{j=1}^{n^{[l]}} (w_{ij}^{[l]})^2$$.

2. Dropout Regularization: Go through each layer of the Neural Network, randomly eliminate the nodes with a given probability. [!$a^[i]$ need to be updated by dividing the probability, to keep the expected value; Dropout only implemented on training set, not testing set.]

3. Other methods: Data augmentation, Early stopping.


#### Tuning Parameters
- In deep learning, we usually recommend that you: <small>[From Coursera: Neural Networks and Deep Learning - HW1 ]</small>
  - Choose the learning rate that better minimizes the cost function.
  - If your model overfits, use other techniques to reduce overfitting.
