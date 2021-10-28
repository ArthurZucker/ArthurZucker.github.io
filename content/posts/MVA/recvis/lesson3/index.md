---
title: "Computer Vision and Object Recognition, lesson 3"
date: 2020-06-08T08:06:25+06:00 
description: Sample post with multiple images, embedded video ect.
menu:
  sidebar:
    name: Lesson 3
    identifier: recvis-lesson3
    parent: recvis
    weight: 10
hero: images/forest.jpg
tags: ["Markdown","Content Organization","Multi-lingual"]
categories: ["Basic"]
math: true
summary: "How to model an RL problem: Markov Decision Processes "
---

<style>
r { color: Red }
o { color: Orange }
g { color: Green }
b { color: Blue }
</style>



Neighbourhood consensus network NIPS

# how do we scale previous methods up? 

Mainly two strategies :
1. NN 
2. Quantisize 

## 1 Efficient Approximate NN search 
A set of local descriptors, but linear NN search is bad, too slow. 
So use approximate NN. Find a match that is nearby. 
 - Best Bin First, K-d trees: explore the cells intersecting the ball to the euclidian distance. Verify that there are no closer points. Youi don't go to the last leaf. Complexity depends on the distribution of the points. Thus the solution is the Approximate NN. Backtracking with limited NB of cell explored, based on their priority ranking. You can also use randomized K-d trees. 
 - Locality Sebsitive Hashing : hash the inpus, have the proba of close inspace points, proba of hash being similar is high
