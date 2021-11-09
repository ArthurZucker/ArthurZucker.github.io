---
title: "Backward propagation using matrix notations"
date: 2021-11-09
description: An explanation of the mathematics behind backward propagation. 
menu:
  sidebar:
    name: Backward propagation
    identifier: backward_prop
hero: images/forest.jpg
tags: ["ML","Backward Propagation","English"]
categories: ["Basic"]
math: true
summary: "An explanation of the mathematics behind backward propagation. "
---

<style>
r { color: Red }
o { color: Orange }
g { color: Green }
b { color: Blue }
</style>


## Introduction 

$$
\begin{equation}
H=\text{ReLU}(W_i X+B_i)\\
Y=W_oH+B_o
\tag{1}
\end{equation}
$$


where $X$ is the input, $Y$ is the output, $H$ is the hidden layer, and $W_i$, $W_o$, $B_i$ and $B_o$ are the network parameters that need to be trained. Here the subscripts $i$ and $o$ stand for the *input* and *output* layer, respectively. This network was also discussed in the class and is illustrated in the above figure where the input units are shown in green, the hidden units in blue and the output in yellow. This network is implemented in the function `nnet_forward_logloss`.

You will train the parameters of the network from labelled training data $\{X^n,Y^n\}$ where $X^n$ are points in $\mathbb{R}^2$ and $Y^n\in\{-1,1\}$ are labels for each point. You will use the stochastic gradient descent algorithm discussed in the class to minimize the loss of the network on the training data given by 

\begin{equation}
L=\sum_n s(Y^n,\bar{Y}(X^n))
\tag{2}
\end{equation}

where $Y^n$ is the target label for the n-th example and $\bar{Y}(X^n)$ is the network’s output for the n-th example $X^n$. The skeleton of the training procedure is provided in the `train_loop` function. 

We will use the logistic loss, which has the following form:

\begin{equation}
s(Y, \bar{Y}(X))=\log(1+\exp(-Y. \bar{Y}(X))
\tag{3}
\end{equation}

where $Y$ is the target label and $\bar{Y}(X)$ is the output of the network for input example $X$. With the logistic loss, the output of the network can be interpreted as a probability $P(\text{class}=1|X) =\sigma(X)$ , where $\sigma(X) =1/(1+\exp(-X))$ is the sigmoid function. Note also that $P(\text{class}=-1|X)=1-P(\text{class}=1|X)$.


Given that in the next task, X will be a 2D vector representing the input vector, I will answer to this question with $X$ as a vector of input and not a matrix ( if X represented a batch of input, the computation would be a bit different). 

So let $X\in \mathbb{R}^{d}$ with $d$ the dimension of $X$. Let's start by computing the local gradients associated with each neurones. 

- Given X, we have the first neuron which outputs $H = ReLu(W_i \times X + B_i)$ with $H\in \mathbb{R}^{h}, B_i \in \mathbb{R}^{h}, W_i\in \mathbb{R}^{hxd}, X \in ℝ^{d}$. The 2 local gradients that can be computed are the following: $\frac{\partial H}{\partial W_i} $ and $\frac{\partial H}{\partial B_i} $.   
  
   -  $\frac{\partial H}{\partial W_i} $ : the derivative of a vector by a matrix is quite uncommon and it's the first time I am getting involved with it. We have that $W_i \in ℝ^{hxd}$ (yes, in the previous definition, in order to compute $W_iX$, the dimensions should be $(hxd)\times h$, with X a row vector, but the next function uses a different format for W). Based on the litterature [<sup>1</sup>](#fn1) [<sup>2</sup>](#fn2) , the derivative of $\frac{\partial W_i X + B_i}{\partial W_i} = X \otimes I_h \in ℝ^{hd \times h } $ with $\otimes$ the Kronecher product, and $I_h$ the identity square matrix of dimension $h$. We thus deduce that : $$\frac{\partial H}{\partial W_i} = diag(𝟙_{W_i \times X + B_i \succeq  0 }) X \otimes I_h  $$ . Note that $diag(𝟙_{W_i \times X + B_i \succeq  0 })$ is a matrix of $ℝ^{h\times h}$.The dimension of this partial derivative is $ (h, h)\times (h \times hd) $. Which gives a vector of dimensions $h\times hd$. 
      
  -  $\frac{\partial H}{\partial B_i} $ : here the computation is straight forward, we can conclude that $\frac{\partial H}{\partial B_i} = diag(𝟙_{W_i \times X + B_i \succeq  0 })$ with dimension $h\times h$. 

- The second neuron which outputs $\bar Y = W_o \times H + B_o$ also has 2 local gradients that can be computed on the fly: $\frac{\partial \bar Y}{\partial W_o} $ and $\frac{\partial \bar Y}{\partial B_o} $. 

  -  $\frac{\partial \bar Y}{\partial W_o}= H $ . The dimension of this partial derivative is $h$. It is the derivative of a scalar by a vector, which gives a vector. 
      
  -  $\frac{\partial \bar Y}{\partial B_o}= 1$ , since $B_0$ is a scalar, and Y is a scalar. 

  -  $\frac{\partial \bar Y}{\partial H}= W_0$ which is of size $h$.  

- Finally, we can compute the derivates relative to the loss function $s(Y,\bar Y)$.
 - Note that $Y$ and $\bar Y$ are both scalars, $ \frac{\partial s(Y, \bar{Y})}{\partial \bar Y} = \frac{-Y \exp(-Y. \bar{Y})}{1+\exp(-Y. \bar{Y})}  = -Y.σ(-Y\bar Y)$ which is a scalar. 
 - $ \frac{\partial s(Y, \bar{Y})}{\partial W_o} =\frac{\partial s(Y, \bar{Y})}{\partial \bar Y}\frac{\partial \bar{Y}}{\partial W_o} = -Y.σ(-Y\bar Y) H $
 - $ \frac{\partial s(Y, \bar{Y})}{\partial B_o} =\frac{\partial s(Y, \bar{Y})}{\partial \bar Y}\frac{\partial \bar{Y}}{\partial B_o} = -Y.σ(-Y\bar Y)  $
 - $ \frac{\partial s(Y, \bar{Y})}{\partial W_i} =\frac{\partial s(Y, \bar{Y})}{\partial \bar Y}\frac{\partial \bar{Y}}{\partial H} \frac{\partial H}{\partial W_i} = -Y.σ(-Y\bar Y) W_0  diag(𝟙_{W_i \times X + B_i \succeq  0 }) X \otimes I_h$
 - $ \frac{\partial s(Y, \bar{Y})}{\partial B_i} =\frac{\partial s(Y, \bar{Y})}{\partial \bar Y}\frac{\partial \bar{Y}}{\partial H} \frac{\partial H}{\partial B_i} = -Y.σ(-Y\bar Y) W_0  diag(𝟙_{W_i \times X + B_i \succeq  0 }) $

 In the next function, it is important to note that the dimension of $W_i$ is incorrect (compared to the notations introduced in this section), indeed, the matrix $W_i \in ℝ^{d\times h}$ instead of $W_i \in ℝ^{h\times d}$. This changes the dimensions of the results I 

## Implementation :

```
def ind(H):
  return (H>0)*1.0
def gradient_nn(X, Y, Wi, bi, Wo, bo):
    '''
    Compute gradient of the logistic loss of the neural network on example X with
    target label Y, with respect to the parameters Wi,bi,Wo,bo.

    Input:
        X ... 2d vector of the input example
        Y ... the target label in {-1,1}   
        Wi,bi,Wo,bo ... parameters of the network
        Wi ... [dxh] 
        bi ... [h] 
        Wo ... [h]
        bo ... 1
        where h... is the number of hidden units
              d... is the number of input dimensions (d=2)

    Output: 
        grad_s_Wi [dxh] ... gradient of loss s(Y,Y(X)) w.r.t  Wi
        grad_s_bi [h]   ... gradient of loss s(Y,Y(X)) w.r.t. bi
        grad_s_Wo [h]   ... gradient of loss s(Y,Y(X)) w.r.t. Wo
        grad_s_bo 1     ... gradient of loss s(Y,Y(X)) w.r.t. bo
    '''
    # THe operators and the format of X does not allow for the same implementation as 
    # what is described in the previous theoretical answer. 
    H = np.maximum(np.matmul(X,Wi) + bi, 0)
    Yo = np.dot(Wo, H) + bo
    h,d = len(Wo), len(X)
    grad_s_bo = -Y*sigm(-Y*Yo)                                    # scalar
    grad_s_Wo = grad_s_bo*H                                       # (h,)  
    grad_h_Wi = (np.diag(ind(H)) @ np.kron(X,np.eye(h)))          # hxh @ ( h x (h,d)) which can be reshaped
    grad_s_Wi = grad_s_bo * ( Wo @ grad_h_Wi).reshape(d,h)       
    grad_s_bi = grad_s_bo*Wo@np.diag(ind(H))                      # h \times h,h gives h 
    return grad_s_Wi,grad_s_bi,grad_s_Wo,grad_s_bo
    ##########################    
```
    