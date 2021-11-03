---
title: "Reinforcement learning, lesson 2"
date: 2021-10-18
description: Sample post with multiple images, embedded video ect.
menu:
  sidebar:
    name: Lesson 2
    identifier: rl-lesson2
    parent: rl
    weight: 60
hero: images/path.png
tags: ["MVA","Reinforcement Learning","English"]
categories: ["Basic"]
math: true
summary: "How to model an RL problem: Dynamic programming "
---
This post sums up the content of the lesson n°2 of RL on dynamic programming

---

<style>
r { color: Red }
o { color: Orange }
g { color: Green }
b { color: Blue }
</style>

# Solving the infinite-Horizon discounted MDPs

The problem we have to solve is the following : 
$$
\begin{align*}
\max _{\pi} V^{\pi}\left(s_{0}\right)= & \\
= & \max _{\pi} \mathbb{E}\left[r\left(s_{0}, d_{0}\left(a_{0} \mid s_{0}\right)\right)+\gamma r\left(s_{1}, d_{1}\left(a_{1} \mid s_{0}, s_{1}\right)\right)+\gamma^{2} r\left(s_{2}, d_{2}\left(a_{2} \mid s_{0}, s_{1}, s_{2}\right)\right)+\ldots\right] \\
=&\mathbb{E}\left[\sum_{t=0}^{\infty} \gamma^{t} r\left(s_{t}, a_{t}\right) \mid a_{t} \sim d_{t}\left(\cdot \mid h_{t}\right)\right]
\end{align*}
$$

## Reducing the search space : 

### History based to markov decision 

{{< alert type="danger" >}}
Theorem (Bertsekas [2007])

Consider an MDP with $|A|<\infty$ and an initial distribution $\beta$ over states such that $|\{s \in S: \beta(s)>0\}|<\infty .$ For any policy $\pi$, let
$$
p_{t}^{\pi}(s, a)=\mathbb{P}\left[S_{t}=s, A_{t}=a\right] ; \quad p_{t}^{\pi}(s)=\mathbb{P}\left[S_{t}=s\right]
$$
Then for any history-based policy $\pi$ there exists a Markov policy $\bar{\pi}$ such that
$$
p_{t}^{\bar{\pi}}(s, a)=p_{t}^{\pi}(s, a) ; \quad p_{t}^{\bar{\pi}}(s)=p_{t}^{\pi}(s)
$$
for any $s \in S, a \in A$ and $t \in \mathbb{N}^{+}$
{{< /alert >}}

Introduced the Discounted Occupancy measure but I don't know why. 

### Non-stationary to stationary 

{{< alert type="danger" >}}
Theorem (Bertsekas [2007])
Consider an MDP with $|A|<\infty$ and an initial distribution $\beta$ over states such that $|\{s \in S: \beta(s)>0\}|<\infty$
Then for any non-stationary policy $\pi$ there exists a stationary policy $\bar{\pi}$ such that
$$
\rho_{\gamma}^{\bar{\pi}}(s, a)=\rho_{\gamma}^{\pi}(s, a) ; \quad \rho_{\gamma}^{\bar{\pi}}(s)=\rho_{\gamma}^{\pi}(s)
$$
for any $s \in S, a \in A$ and $t \in \mathbb{N}^{+}$
{{< /alert >}}

## Simplifying the value function 




## From stochastic to deterministic decision rules


Conclusion: we can now focus on stationary policies with deterministic markov decision rules. 


# Solving Finite-Horizon MDPs

# Solving Infinite-Horizon Undiscounted MDPs

# Summary
<!-- Started with a recap, but most of what was supposed to be a recap, was kinda new since I did not have time to go back on it. 

- always exists a deterministic markov stationary optimal policy. (mapping between state and action is deterministic). This allows to reduce the size of search. 
Focus on two task, policy evaluation (find the value function), policy learning (control) or finding the policy by solving the MDP. 

Bellman equations : for stochastic 
    $V^\pi (S) = \sum \pi(s,a) [\left r(s,a)) + \gamma\sum p(s'\mid s,a)V^\pi (s'), r(s,a)) is the expected reward on the policy $\pi$

He gave us a homework but I didn't really have time to do it, so let's focus on the explanations. 

The policy says that on s0 you choose a0, s1 choose a0, s2 choose a1 (defined by $\pi = {a_0,a_0,a_1}$)
The reward is 0 on 0, a_0. In state s1, same, but reward is 1/3 of Bernoulli. 1/3 is the expectation, which is why we put the 1/3 on the matrix reward. 

Not all MDP are goal oriented. Even if you have a stochastic goal. The optimal policy IN EXPECTATION with respect to the randomness, expected value with respect to the policy

1. Compute $V^\pi$ (using the bellman form)
    - $P^\pi$ = \begin{matrix}  &s0 & s1 & s2 \\ s0 &&&\\s1&&&\\s2&&&\\  \end{matrix}$
    - $r^{\pi}$ = [0,1/3,0]
    - Compute the inverse of $I-\gammaP^\pi$

We also saw the optimal bellman equation. A way of computing V* of S. Replace the expected reward with the max over the actions. 
It is not linear anymore, and today we will see how to compute it. 

The Q-function was introduced. $Q = \mathbb{E} [\sum_{t=0}^{\inf} g^t r(s_t,a_t) \mid (s_0,a_0) = (s,a)]$ gives the utility of each action in the state.  We can again write the bellman equation. 

_______ Was a bit lost after this, had to handle USB and bluetooth stuff

Value Iteration : apply the bellman operator iteratively, converge to an approximation of the optimal solution. Keep track of the greedy action -> return the optimal policy 

###  Complexity of the value operation 

Relies on the bellman operator, which means solving a matrix system. 

#### Extensions and Implementations 

Starvation : may end up in a loop / cycle of update that prevents you from converging

Can apply iteratively on the Q function. It's really generic. 

#### Policy iteration 

Iterate on them rather than value function. 

1. Start from policy
2. Each iteration : 
    - Policy evaluation -> bellman operator matrix equation
    - Policy improvement, compute greedy policy
3. Stop if the policy is not improving

Iterate over the $\pi$. Return $\pi$ at the end. 
The sequence generated is non decreasing. This means that it will converge in a **finite** ($ V^{\pi_k+1} \geq V^{\pi_k} $ ) number of iterations. VS the value function that has convergence in infinite.  

INSERT PROOF HERE! Was done in class.

Complexity? $O(S^3)$ which is a bit more than Value State function. 
Through Monte-Carlo is also interesting, through the expectation but it's an approximative method (control the approximation which propagates through the learning). In practice, different, but the one that converges is the exact one. 

POlicy improvement step, in $O(A)$ or $O(SA)$

Total depends on $\gamma$

#### Comparison between Value  and Policy Iteration 

Pros and Cons for each

## Other algorithms based on DP to compute optimal policy

Primal LP? 
 -->



## Example

Let's apply the notions to a simple example. Let's consider the following model : 

{{< img src="images/example_mdp1.png" title="Example of a markov decision process" align="center" >}}

<!-- {{< vs 3 >}}  stands for vertical space -->