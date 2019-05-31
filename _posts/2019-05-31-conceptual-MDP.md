---
layout: post
title: Markov Decision Process (in terms of conceptual stories)
comments: true
---

There is a finite number of states $s$, describing the position or situation you are in.

At each state, you can choose one of the finitely many actions, $a$. 

Performing action $a$ when you are at state $s$ will lead to various outcomes, i.e. moving to another state $s\'$, with different probabilities, $P(s\'\| s, a)$, or simply $P_{sa}$. Markov process means that this probability only depends on the current state and action, and not on any past history.

Doing $a$ at state $s$ also gives you a reward $R(s,a)$. Think of this as a reward for being in state $s$, minus a cost for doing action $a$, because some positions are better than others, and some actions are harder than others. If one ignores the benefit or cost of $a$, then the reward only depends on the current state.

Finally, discount factor $\gamma<1$ describes how important "delayed satisfactions" are compared to "instant gratification". When $\gamma=0$, future doesn't matter; when $\gamma = 1$, rewards promised for tomorrow is as good as the ones cashed out today.

A policy $\pi$ is a strategy of "what to do at each situation". 

The value function $V^\pi(s)$ is the expected total reward if you start from state $s$, and stick to your policy $\pi$.

Bellman equation says that at state $s$, expected total reward is the sum of two components: $R(s)$ the immediate reward at $s$, together with expected total reward from tomorrow on, discounted by a factor of $\gamma$. This is also a way to write an infinite sum "iteratively", as some kind of fixed point. We will come back to this iteration picture soon.

Value function depends on the policy, because actions can change the future('s likelihood). There is some optimal policy that will maximize the value function, and the best value at each state is called the optimal value function $V^\*(s)$. The Bellman equation for optimal value function is similar, except now since we are free to choose the best policy, at state $s$ we not only claims the immediate reward $R(s)$, we also want to pick the action that will lead to the maximum expected future rewards. If immediate $R$ also depends on $a$, then there is a trade-off between immediate and future rewards.

There are 2 main ways to approximately find the optimal value function: value iteration and policy iteration.

*Value iteration* means instead of considering all contributions from all future time, only focus on the next $i$ rewards for now, and get a better and better approximation by including more future days. 

* Before any iterations, set $V$ to be 0 for all state $s$, because it's not payday yet. 
* At the first iteration, claim the immediate reward for each state, so $V(s) = R(s)$. 
* At the second iteration, you need to decide what to do today so that you can get the highest pay tomorrow, and $V$ is the sum of first day reward plus the average second day reward. 

At each iteration, simply consider further into the future. Value iteration converges simply by definition. (I think what I just described is called the synchronous update)

*Policy iteration*: Before playing the game, you first decide on what to do at each situation (i.e. fixed a policy $\pi$). Next, starting from different states, you play the game to completion/for many turns, repeat for many times, so that you can evaluate how good each state $s$ is on average, i.e. find the value of $V^\pi(s)$. (Actually, you can find this value by solving the system of linear equation, Bellman equation; but this is of course less conceptual). Next, you reevaluate the initial policy: at state $s$, you really should be choosing the action that on average moves you towards the states that gives you higher outcomes. Now you have a new policy $\pi\'$ (called greedy with respect to $V$, because you are expecting that what works now might work next time). Repeat by again playing the game repeatedly, to find the new value of each state. Iterate. 

In the 2 paragraphs above, we are already assuming that we know $P_{sa}$ exactly. In practice, this information takes experimentation and learning: repeatedly try action $a$ at state $s$, and record the percentage of each outcome state. Maybe add some Laplace smoothing to avoid 0/0; i.e. if you never tried action $a$, or you did but have never seen $s\'$ happening yet, don't immediately dismiss $s\'$ as impossible, but instead keep an open mind by leaving it some default nonzero/equal probability.