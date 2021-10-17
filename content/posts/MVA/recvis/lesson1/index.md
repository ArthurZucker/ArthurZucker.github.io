---
title: "Computer Vision and Object Recognition, lesson 1"
date: 2020-06-08T08:06:25+06:00 
description: Sample post with multiple images, embedded video ect.
menu:
  sidebar:
    name: Lesson 1
    identifier: recvis-lesson1
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

What is an edge? It describe a rapid changes in image intensity. 4 discontinuities can create those : 
- Surface NOrmal ?? 
- Depth discontinuity 
- Surface Reflectance 
- Illumination discontinuity.

Intensity profiles in the image vary. It can look like a step function, roof edge or line edges. Step is mostly used, given that it is the simplest. 

In real images, the intensity is noisy and the edges look a bit different from the step function. 

Edge detector has to find were the edge is (position), its magnitude (strength) and its orientation. It also has to be precise. Requirements are linked to performance, resistance to noise etc. 

## First derivative : 

For 1D functions : Local extrema in first derivative give the location of the edges, while the height gives its strength. 

For images: partial derivatives are used. 

Insert images where [x,0] and [0,y] for the gradient. Magnitude is the euclidan norm, and the gradient orientation is the tan-1(dy/dx).

But images are continuous. We could use finite difference as the discrete gradient => use 4 pixels. Can be implemented as convolution! That's really interesting. 


   | ----- | --- |
   | -1 | 1  |
   | -1 | 1  |

  Various gradient operators, what does the size changes? 
  Small = sensible to noise, but very good localization (what does it mean? how does it localize???). 
  Bigger give better detection, les sensible to noise, but take into account things that might be useless.

  Insert python code to compare various sobel filters? 

  The value returned is real, you then need to threshold. 
  Standard threshold vq hysteresis : if magnitude is between 2 threshold, compare with neighboring pixel. 

  But edges have to be grouped. 

## Second derivative : 

Here, zero-crossing indicates the presence of edges. You have to detect those. The  lablacian operator has to be used in that case. But it doesn't provide the orientation of the edges. 

We have to use at least 3 pixels for each directions. It can again be implemented as a convolution. We have to take into account the orientation, and the distance that is bigger for diagonal values. 

Negative values in the image were mapped to 128. Less will be between those two values. 

## Supress noise
Gaussian smoothing! Convolve the signal with the gaussian.
The intuition behind is that its a statistical model of noise! Its not just that "it works". 

Taking the derivative of the gaussian then convolving saves 1 operation. 

It works the same with the laplacian. Laplacian of Gaussian, then convolve it. 