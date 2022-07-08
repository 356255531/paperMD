# Self-Supervised Learning Disentangled Group Representation as Feature
Authors: [Tan Wang](https://openreview.net/profile?id=~Tan_Wang1), [Zhongqi Yue](https://openreview.net/profile?id=~Zhongqi_Yue1), [Jianqiang Huang](https://openreview.net/profile?id=~Jianqiang_Huang2), [Qianru Sun](https://openreview.net/profile?id=~Qianru_Sun2), [Hanwang Zhang](https://openreview.net/profile?id=~Hanwang_Zhang3)Venue: NeurIPS 2021
## Comments
## Summary
In this paper, authors formulate the notion of “good” representation from a group-theoretic view using Higgins’ definition of disentangled representation[^1], and show that existing Self-Supervised Learning (SSL) only disentangles simple augmentation features such as rotation and colorization, thus unable to modularize the remaining semantics.

To break the limitation, we propose an iterative SSL algorithm: Iterative Partition-based Invariant Risk Minimization (IP-IRM), which successfully grounds the abstract semantics and the group acting on them into concrete contrastive learning.

## Background
The author believes that the current research over focused on the downstream tasks but ignores the importance of learning a **good** representation.

## Problem
The most self-supervised learning methods have 2 stage, 
1. Learning the invariance from the augmented images,
2. Applying the learned feature in the downstream tasks.

However, no formal definition or metrics for a good representation. 

What's more, the current research focus more on the performance of downstream tasks with the learned features, rather than understanding the learning mechanism in the first stage (invariant feature learning). 

## Approach
The author follows the definition of disentangled representation from Higgins[^1] and extends the definition towards two important properties in the common views, namely robustness and zero-shot generalization.

There are two major observation from the visualization of SimCLR[^2] and the proposed method.
1. Even if we only use the augmentation-related feature, the classification accuracy of a standard SSL (SimCLR) does not lose much as compared to the full feature use. 
2. Figure 2 (b) visualizes that the CNN features in each layer are indeed entangled (e.g., tyre, motor, and background in the motorcycle image). In contrast, our approach IP-IRM, to be introduced below, disentangles more useful features beyond augmentations.
![[Screenshot 2022-07-08 at 19.51.48.png]]
## Experiment
## Conclusion 
[^1]: Irina Higgins, David Amos, David Pfau, Sebastien Racaniere, Loic Matthey, Danilo Rezende, and Alexander Lerchner. Towards a definition of disentangled representations. arXiv preprint arXiv:1812.02230, 2018.
[^2]: Ting Chen, Simon Kornblith, Mohammad Norouzi, and Geoffrey Hinton. A simple framework for contrastive learning of visual representations. In International conference on machine learning, pages 1597–1607. PMLR, 2020.