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


#### Activation function: A Non-linear function
- **tanh** function always works better than sigmoid function. tanh ( $tanh(z) = \frac{e^z - e^{-z}}{e^z +e^{-z}}$ ) function is a shifted version of sigmoid, but goes cross (0,0). The mean of its output is closer to zero, and so it centers the data better for the next layer.

- When z is very small/large, both sigmoid & tanh has small slope. -> slow down gradient descent. -> **Use RELU** (rectified linear unit) (a = max(0,z)).
- One disadvantage of RELU is that the derivative is equal to zero when z is negative (In practice, it works just fine. another version is **Leaky ReLu** (a = max(0.01z, z)), often works better, but not used widely).

- **Tips:**
  - If you are doing binary classification, usually use sigmoid function as output layer.
  - On other layers RELU is often the default choice of activation function.


#### Tuning Parameters
- In deep learning, we usually recommend that you: <small>[From Coursera: Neural Networks and Deep Learning - HW1 ]</small>
  - Choose the learning rate that better minimizes the cost function.
  - If your model overfits, use other techniques to reduce overfitting.
