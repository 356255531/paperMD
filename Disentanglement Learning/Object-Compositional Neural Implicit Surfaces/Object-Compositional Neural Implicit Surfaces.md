# Object-Compositional Neural Implicit Surfaces
[Qianyi Wu](https://arxiv.org/search/cs?searchtype=author&query=Wu%2C+Q), [Xian Liu](https://arxiv.org/search/cs?searchtype=author&query=Liu%2C+X), [Yuedong Chen](https://arxiv.org/search/cs?searchtype=author&query=Chen%2C+Y), [Kejie Li](https://arxiv.org/search/cs?searchtype=author&query=Li%2C+K), [Chuanxia Zheng](https://arxiv.org/search/cs?searchtype=author&query=Zheng%2C+C), [Jianfei Cai](https://arxiv.org/search/cs?searchtype=author&query=Cai%2C+J), [Jianmin Zheng](https://arxiv.org/search/cs?searchtype=author&query=Zheng%2C+J)
## Summary
This work explores the connect of object **geometry** and 2d **semantic infomration** (segmentation) and learn signed distance function (SDFs, implicit function) for each individual object from mutli-view image. With the learned object SDFs, both high-fidelity 3D surface and novel view syhthesis can be generated, therefore, disentangled objects in scenes.

## Background
1. Implicit representation proved to be good at remembering the 3D information, e.g., density, color and segmentation. 
2. NERF mainly neglects the object geomety information (i.e., object surfaces).
3. Prior works focus on scene-level 3D reconstruction and noval view synthesis. Less attention was spent on  object-compositional scene reconstruction.

## Contribution
1. The author proposes to use the per-object signed distance functions for surface modelling.
2. The author propose a method of incoorperating semantic segmentation for learning object surface priors.

## Approach
Given a set of N posed images $A = \{x_1,x_2, ··· ,x_N\}$ and the corresponding instance semantic segmentation $S = \{s_1,s_2, ··· ,s_N\}$, the goal is to learn ***object-compositional implicit 3D representation***, i.e., per-object SDFs, which are capable of reconstruction the whole scene $\Omega$ and also individual objects $O$.

![[Screenshot 2023-03-14 at 10.58.59.png]]
### Background
#### Volumetric Rendering
Considering a ray $\boldsymbol{r}(v)=\boldsymbol{o} + v\boldsymbol{d}$ emanated from a camera position o in the direction of d, the color of the ray can be computed as an integral of the transparency $T (v)$, the density $\sigma(v)$ and the radiance $c(v)$ over samples taken along near and far bounds $v_{near}$ and $v_{far}$
![[Pasted image 20230314134806.png]]
#### SDF-based Neural Implicit Surface
Specifically, given a scene $\Omega \in \mathbb{R}^3$, and $M = \partial\Omega$ is the boundary surface. The Signed Distance Function $d_{\Omega}$ is defined as the distance from point $\boldsymbol{p}$ to the boundary $M$:
![[Pasted image 20230314135410.png]]
And finally transform the SDF-value to density following the previous work,
where $\beta$ is a learnable parameter in our implementation.
![[Pasted image 20230314135504.png]]
### Training
Specifically, given a static scene $\Omega$,it can be naturally represented by the spatial composition of $k$ different objects $\{O_i \subset \mathbb{R}^3|i=1,..,k\}$, i.e., $\Omega=\bigcup_{i=1}^k O_i$.
## Experiment
https://www.youtube.com/watch?v=23vxOV19bEw
## Discussion and comment
1. Could there be less supervisions? Although there is no 3D supervision, this paper almost used the strongest level 2D supervision (semantic segementation):
	- object segmentation
	- number of objects
2. Training and inference time: For any noval scene, the neural surface needed to be trained from scratch and therefore, very time-consuming. 
3. The properties of objects are non extracted, therefore, intractable for a controllable generation.
4. Need extra information such as the number of object etc.
