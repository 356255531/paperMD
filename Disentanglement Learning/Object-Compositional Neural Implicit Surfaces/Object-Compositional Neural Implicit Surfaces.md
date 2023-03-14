# Object-Compositional Neural Implicit Surfaces
[Qianyi Wu](https://arxiv.org/search/cs?searchtype=author&query=Wu%2C+Q), [Xian Liu](https://arxiv.org/search/cs?searchtype=author&query=Liu%2C+X), [Yuedong Chen](https://arxiv.org/search/cs?searchtype=author&query=Chen%2C+Y), [Kejie Li](https://arxiv.org/search/cs?searchtype=author&query=Li%2C+K), [Chuanxia Zheng](https://arxiv.org/search/cs?searchtype=author&query=Zheng%2C+C), [Jianfei Cai](https://arxiv.org/search/cs?searchtype=author&query=Cai%2C+J), [Jianmin Zheng](https://arxiv.org/search/cs?searchtype=author&query=Zheng%2C+J)
## Summary
This work explores the connect of object **geometry** and 2d **semantic infomration** (segmentation) and learn signed distance function (SDFs, implicit function) for each individual object from mutli-view image. With the learned object SDFs, both high-fidelity 3D surface and novel view syhthesis can be generated, therefore, disentangled objects in scenes.

## Background
1. NERF mainly neglects the object geomety information (i.e., object surfaces).
2. Prior works focus on scene-level 3D reconstruction and noval view synthesis. Less attention was spent on  object-compositional scene reconstruction.

## Contribution
1. The author proposes to use the per-object signed distance functions for surface modelling.
2. The author propose a method of incoorperating semantic segmentation for learning object surface priors.

## Approach
Given a set of N posed images $A = \{x_1,x_2, ··· ,x_N\}$ and the corresponding instance semantic segmentation masks $S = \{s_1,s_2, ··· ,s_N\}$, the goal is to learn ***object-compositional implicit 3D representation***, i.e., per-object SDFs, which are capable of reconstruction the whole scene $\Omega$ and also individual objects $O$.

![[Screenshot 2023-03-14 at 10.58.59.png]]

## Experiment
https://www.youtube.com/watch?v=23vxOV19bEw
## Comment
Supervisions:
- object segmentation
- number of objects
Training and inference:
