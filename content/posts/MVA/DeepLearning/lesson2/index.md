---
title: "Deep Learning, lesson 1"
date: 2021-19-10
description: Sample post with multiple images, embedded video ect.
menu:
  sidebar:
    name: Lesson 2
    identifier: dl-lesson2
    parent: dl
    weight: 10
hero: images/forest.jpg
tags: ["Markdown","DL","activation functions"]
categories: ["Course notes"]
math: true
summary: "Comparing activation functions  "
---

<style>
r { color: Red }
o { color: Orange }
g { color: Green }
b { color: Blue }
</style>

### Sigmoid 
 Usually used in the last layer, because it gives strong confidence for example. Usefull for the optimisation. 

## Loss function

Cross entropy and NLL (Negative Log Likelihood) for regression here

Quizz: 

1. MSE, if sigma is constant? Write the density of the gaussian distribution then simplify and remove the constant variance (should do this on paper looks pretty important for intuition)

### Classification problems 
Softlax used in the last layer. But if we don't have a class, we should give him a random class? We don't really want to force the output, but need to know where the network is not confident. Paper on how RELU fails to express the non-confidence **look at the slides**

## Generalization 
Link to double descent?? Grooking 

## Regularization 
Weight decay, make our parameters smaller with L2 regularitaion? 

Normalisation??? Why? Because the activation function has more mapping when you are between 0 znd 1 or something of the kind. 


## Optimization for deep learning 
large scae optimisation paper to read 

Identifiable model? ONe set of param can rule out everything? Which mean only one minima. But in NN we can change the order of the neurons and still have similar outputs, thus most of the models are non identifiable. Most of the model have various local minimum, but they are pretty similar. 

Identifiying and attacking the saddle point problem 

## Back propagation 
Follow threw example using the chain rule. Partial derivatives and all


## Wheight Initalizer 

### Xavier 
Unifrom with particular distribution?? Add this to @TODO ANKI. Same activation and gradient variance between all layers. 

## Batch normalisation 
Normalisation the distribution of input features. Prevents exploding gradients and more resilieent to scaling, but why? 


### Data Augmentation 
INterpolate two inputs together. Use it as an input to the network, modify cross entropy to work with it **mixup** **cutup**. Real data augmentation creating inputs out of the distribution (they can not exist!) artifical modification. 

### Dropout 
Use bagging and enesmelbe methods on the various models. You can consider all the variations of the network and train them. Then select the best.  