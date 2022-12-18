---
title: "Benchmarking hyperspectral DRL: a mostly negative reult."
date: 2022-11-30
katex: true
markup: "mmark"
---

## HyperSpectralDRL

Final project for CS285, Deep RL, UC Berkeley F22. 

"Benchmarking deep reinforcement learning algorithms for unsupervised hyperspectral band selection."

[Link](https://daniel-furman.github.io//research-outputs/Deep_RL_Final_Project.pdf) to tge write up.

### Conclusion
The project aims at exploring different DRL algorithms for hyper-spectral band selection. Overall, we find that for
this type of task Actor-Critic methods such as Actor-Critic and Soft Actor-Critic outperform traditional Q-Learning
methods such as DQN and DDQN in terms of correlation and in many classification tasks. While we found that the
agent is able to learn a valid representation of the search space, the effort and complexity of DRL (and most of the other
published methods) may not be required for this problem. The vast majority of findings by us and other researchers can
be comparably matched by randomly selecting bands and choosing the outcome with the best reward. However, if we
wanted to keep a higher number of bands, these complex approaches may show their usefulness in navigating the larger
search space.
