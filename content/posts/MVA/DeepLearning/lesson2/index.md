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
