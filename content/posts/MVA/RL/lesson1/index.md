---
title: "Reinforcement learning, lesson 1"
date: 2020-06-08T08:06:25+06:00 
description: Sample post with multiple images, embedded video ect.
menu:
  sidebar:
    name: Lesson 1
    identifier: rl-lesson1
    parent: rl
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

The course is provided by Matteo Pirotta a Facebook AI Researcher, and is based on one of the previous MVA RL classes by Alessandro Lazaric (FAIR). @TODO add links to their linkdin or websites

## Introduction 

### What is RL? When to use it? Why RL? 

RL, a short for Reinforcement Learning, is a subclass of machine learning, which focuses on building a model able to learn from his action in an environnement. It builds its knowledge threw *reinforcing* what it knows, threw trial and error. 

RL has a lot of applications, ranging from finance (where the goal can be to optimize sales live, and the model learns to buy/sell) to robotics, game solving or exploration. Any task which requires an action to be taken to maximize a utility function can use RL models. One of the most successful usage of RL is **[alphago]()**, a model which taught himself how to play *Go*, and beat the world champion. *Go* was considered to be the last barrier, one of the most complex game, given the huge amount of configurations : more than **??** which is more atom than the universe contains. 

Let's try to give a proper definition to RL. 
In any RL model, there is :
 - an RL agent
 - an Environment, deterministic or stochastic
 - actions
 - rewards, sometimes long-term like in go, or short term in portfolio management. But you can have intermediate rewards/signals. You need the knowledge to do that, but might not be possible. Long time effects/certain configurations are optimal?. The function is still free to be designed.  
 - states, sometimes unknown, like the stock prices that are unpredictable. Can only see a realization. Lots of uncertainty. 

Goal is to maximize the reward. Sometimes you don't know the Environment / reward and can only observe! Connected to adaptive control theory, act by looking at the observations you get through the interactions with the systems. 

**Framework for learning by interaction under uncertainty**, agent takes action, receives reward, and the environment evolves to the next state. 

### Content of this note : 

 - Reward : function? 
 - Value : cumulative reward an agent can take
 - Policy : Actions to take in a state

How to model and RL problem? 
 - Markov process

How to solve it? 
 - Dynamic programming 

Solve incrementally? 
- temporal difference, Q-learning using stochastic approximation.

How to solve approximately an RL problem? 
- policy gradient, TD based method, deep RL

## 1. Markov Decision Process

A RL problem is modelled using *Markov processes*. 

### The Reinforcement Learning Model 

(insert image provide)

It can be described using simple keywords : 
* Environment, which defines where the Agent evolves 
* Agent, is the ??? learning 
* Actions and their associated rewards
* States, which allow the definition of the system 

Lets follow along a simple example throughout this course, in order to better understand each notions. 
TODO, define the 4 notions above in the case of a simple atari game.

### The RL interactions 

The classic RL interaction is as follows: 

We have a discrete decision time $t$ (which would be for example seconds), and at each timestamp : 

1. The *agent* selects an *action* $a_t$, based on $s_t$ the current *state* of the system. 
2. The *agent* gets his *reward* $r_t$
3. The *Environment* moves to a new state $s_{t+1}$

### Markov chains

Markov Chains are the building blocks of RL. A Markov Chain is a stochastic  (which means that it includes randomness )  model describing a sequence of possible events in which the probability of each event depends only on the state attained in the previous event[^1]. In order to create a model, we need to introduce mathematical definitions. 

[^1]: https://en.wikipedia.org/wiki/Markov_chain

<g>Definition :</g> Given $S$, a state space and a bounded  compact subset of the Euclidean space, the discrete time dynamic system $(s_t)_{t\in \mathbb{N}}$  is a markov Chain **if it satisfies** the <r>Markov property</r>: 

$$ \mathbb{P}\left(s_{t+1}=s \mid s_{t}, s_{t-1}, \ldots, s_{0}\right)=\mathbb{P}\left(s_{t+1}=s \mid s_{t}\right)$$

This means that given an initial state $s_0$, the markov chain is defined by the transition probability :  $p\left(s^{\prime} \mid s\right)=\mathbb{P}\left(s_{t+1}=s^{\prime} \mid s_{t}=s\right)$. 


<o> Intuition:</o> a markov chain only needs an initial state, and a transition probability to figure out any later state, it is defined by the transition probability. 

@TODO add 4 states markov chain example with attari like states

### Markov Decision Process (MDP)

A Markov Decision Process is a tool, to model decision making when outcomes can be random. 

<g>Definition :</g> a Markov Decision Process is defined as a tuple <b>$M=(S,A,p,r)$</b> with 

* $S$ the (finite) State space
* $A$ the (finite) Action space
* $p(s'|s,a)$ the transition probability, such that $\mathbb{P}\left(s_{t+1}=s' \mid s_{t}=s,a_t=a\right)$
* $r(s,a,s')$ is the reward of the transition from $s$ to $s'$ taking the action $a$. The reward can be stochastic, but we can express its distribution, $v$ for $s,a$ as $v(s,a)$. Thus the reward can be writtent as : $r(s,a) = \mathbb{E}_{R\sim v(s,a)}[R]$. 

#### Assumptions

 <b>Markov assumptions</b> : the current state $s$ and the action $a$ are a sufficient statistic for the next state $s'$. This means that "no other statistic that can be calculated from the same sample provides any additional information as to the value of the parameter"[^2]. Our statistic provides as much information as possible. 

[^2]:https://en.wikipedia.org/wiki/Sufficient_statistic#cite_note-Fisher1922-1

 <b>Time assumption</b> : time is discrete, not continuous. At each step, $t\rightarrow t+1$.

 <b>Reward assumption</b> : the reward is uniquely defined by a transition from a state $s$, to $s'$ and an action $a$. 

 <b>Stationary assumption</b> : transition and reward don't change with time. Otherwise, it's non-stationary. 

## 2. Policy 

<g>Definition : </g>a decision rule $d$, which chooses an action from the state $S$ of the system can be : 

- Deterministic, given the same set of state $S$, the action $a\in A$ will be chosen
- Stochastic, a probability distribution over the actions determines $a$.  
- History-dependant, and is thus  
- Markov

<g>Definition</g> : A policy is a sequence of decision rules, it can be :

- Non-stationary, then $\pi = (d_0,d_1,...)$ 
- stationary, then $\pi = (d,d,...)$

At each round t, an agent following the policy $\pi$ selects the actions $a_t \sim d_t(s_t)$ .

### Markov chain of a policy 

A stationary policy defines a Markov chain on a random process! Why?  Well the transition probability of a random process $(s_t)_{t \in \mathbb{N}}$ with regards to a stationary policy $\pi$ is the following : 

$$ P^\pi (s'\mid s) = \mathbb{P}(s_{t+1}=s' \mid s_t = s, \pi) $$  

Every actions in $A$ (even if it does not take the state from $s$ to $s'$) has to be taken into account. Thus we deduce that $$ p^\pi (s'\mid s) = \sum_{a\in A} \pi(s,a)p(s'\mid s,a) $$

## 3. Optimality Principle

This part answers the question of how good is a policy, and how do we measure this.

### State value function 

The state value function allows us to determine the effectiveness of a policy. Various definitions can be used depending on the problem at hand. For the following definitions, let $\pi = (d_1, d_2, ...,)$ be a deterministic policy. 

<div style="padding-left: 30px;">
:game_die: The <g>Finite time horizon T</g> policy, sets a deadline $T$, at which the sum of the rewards up to $T$ will be computed. The value function can be expressed as : 


$$ V^\pi(t,s) = \mathbb{E}\left[ \sum_{\tau = t}^{T-1} r(s_\tau,d_\tau(h_\tau)) + R(s_T) \mid s_t = s; \pi = (d_1, d_2, ...,) \right ]$$

Here, where $R$ is a value function for the final state. This mathematical formula simply expresses the fact that the state value function $V$, for a certain policy $\pi$, a time $t$ which will be the the "beginning" of the computation, and a state $s$ such that at time $t$, the system is in the state $s$, is equal to the Expectation of the sum of the rewards obtained taking actions according ot the policy, and receiving the corresponding rewards. We have to take into account the Expectation because the decision process can be stochastic, and thus the Expectation gives the equivalent of the mean rewards in a stochastic model. \
$\qquad$:memo: It is usually used when there is a deadline to meet. 
</div>


<div style="padding-left: 30px;">
:game_die: The <g> Infinite Time Horizon with discount </g> translates a problem that never terminates. Rewards closer in time receive a higher importance :

$$ V^{\pi}\left(s\right)\ =\ \mathbb{E}\left[\sum_{t=0}^{\infty}\gamma^tr\left(s_t,d_t\left(h_t\right)\right)\ \mid s_{0\ }=s;\pi \right] $$

where $0\leq\gamma<1$ is the *discount* factor. If it's small, the value function focusses on short-term reward, if it's big, on long term reward. 
This series always converges  \
$\qquad$:memo: We implement it when there is uncertainty about the deadline, or intrinsic definition of discount ?????? @TODO give examples 
</div>



<div style="padding-left: 30px;">
:game_die: The <g> Stochastic shortest path </g>, the problem never terminates but the agent will reach a termination state. 

$$V^{\pi}\left(s\right)\ =\ \mathbb{E}\left[\sum_{t=0}^{T_{\pi}}r\left(s_t,d_t\left(h_t\right)\right)\ \mid s_{0\ }=s;\pi\right]$$

$T_{\pi}$ : first random time when the termination state is achieved.   \
$\qquad$:memo: Used when there is a specific goal condition
</div>


<div style="padding-left: 30px;">
:game_die: The <g> Infinite time horizon with average reward</g>, the problem never terminates but the agent focuses on the expected average of the rewards  

$$V^{\pi}\left(s\right)\ =\ \lim_{T\to\infty}\ \mathbb{E}\left[\frac{1}{T}\sum_{t=0}^{T-1}r\left(s_t,d_t\left(h_t\right)\right)\ \mid s_{0\ }=s;\pi\right]$$

$T_{\pi}$ : first random time when the termination state is achieved.   \
$\qquad$:memo: Used when the system should be constantly controlled over tim
</div>


