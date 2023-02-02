# Symmetry-induced Disentanglement on Graphs

Authors:[Giangiacomo Mercatali](https://openreview.net/profile?id=~Giangiacomo_Mercatali1), [Andre Freitas](https://openreview.net/profile?id=~Andre_Freitas1), [Vikas Garg](https://openreview.net/profile?email=vikas.garg%40aalto.fi)
Venue: [**NeurIPS 2022 Conference** homepage](https://openreview.net/group?id=NeurIPS.cc/2022/Conference "Venue Homepage")

## Summary
___
This present conditional symmetry as the notion of disentanglement in graph structure. The contribution of this method can be structured as following:
1. uses Lie algebra to encode certain graph properties (No explicit indication if they are independent factors as in ICA) such that those properties can be leverated for a generative setting using e.g., VAE.
2. segregates the latent space into uncoupled and entangled parts (Isn't the meaning of disentanglement to find the independent factors, or recover the original sources?)

## Contribution
___
1. A rigorous symmetry-based formalism for disentanglement on graphs
2. A parameterization using Lie algebra based on the intuition that a Lie algebra coordinate represents a single graph propert
3. Two algorithms for Symmetry-Induced Disentanglement under unconditional (SIDU) and conditional (SIDC) settings, both using a two-level variational auto-encoding mechanism
4. A systematic evaluation on several disentanglement metrics

## Background and Problem to be solved
___
Problem to solve: Disentangle latent factors that control certain graph properties in a generative setting.

The most rigorous definition over disentanglemnt learning probably still comes from Higgins et al ^[Irina Higgins, Sébastien Racanière, and Danilo Rezende. Symmetry-based representations for artificial and biological general intelligence. Frontiers in Computational Neuroscience, page 28, 2022]. She states that, the equivariant part of disentangled representation can be represented by a Lie group for some applications and such Lie groups can be further decomposed as cross products of multiple subgroups.

The satisfication of transformation symmetry is widely demonstrated as a key  aspect to disentangle semantic factor in data-driven approaches.

## Approach
___
### 1. Symmetry-based Formalism for Disentanglement on Graphs
![[Screenshot 2023-01-31 at 10.25.11.png]]

![[Screenshot 2023-01-31 at 10.26.12.png]]

### 2. Disentanglement on graphs
![[Screenshot 2023-01-31 at 10.32.26.png]]
##### Intuition
A latent representation $\hat{Z}$, obtained, e.g., from a graph encoder, is disentangled with respect to a Lie group $G$, if a change in the coordinate $t_i$ is associated with a change in only the $i$th component of $\hat{Z}$, i.e., only $\hat{z}_i$.
![[Screenshot 2023-01-31 at 10.37.32.png]]

### 3. Further constrains
1. Commutativity induced by the transformation sysmetry
2. Hessian penalty: the Hessian matrix with respect to a disentangled representation is always zero. This penalty in a Lie algebra parameterization setup, as $H_{ij} = \frac{\delta^2g(T)}{\delta t_i \delta t_j}$ where $g(T) =exp(\sum^k_{i=1} t_i \mathbb{A}_i)$  , and show that if $\mathbb{A}_i\mathbb{A}_j = 0 \forall i, j$ then $H_{ij} = 0$.

### 4. Method
![[Screenshot 2023-01-31 at 10.46.45.png]]
We use the following notation for model variables: latent graph embeddings $Z$ (and $\hat{Z}$), graph features $X$, symmetry Lie group structure $T$ , and the graph adjacency matrix $A$. We next derive lower bounds on log-likelihood for both the unconditional and conditional settings (see Appendix for details).
![[Screenshot 2023-01-31 at 10.50.27.png]]
## Experiment
___
### Disentanglement evaluation
#### 1. Ablation study
The auther used 5 disentanglement metrics: β-VAE (Beta), FactorVAE (FVM), Mutual Information Gap (MIG), DCI Disentanglement, and Factor Leakage (FL)
![[Screenshot 2023-02-02 at 10.05.48.png]]
The hessian penalty results to be effectively enhancing disentangled representations, while the commutative penalty is less effective, and we can explain this result because the former requires the Lie algebra basis elements to have mutual products of zeros while subgroup decomposition only requires their commutators to be zeros, which also confirms the results obtained for image datasets.
#### 2. Correlation analysis (doesn't it tells how entangled the feature are???)
![[Screenshot 2023-02-02 at 10.37.01.png]]
#### 3. Disentanglement results
![[Screenshot 2023-02-02 at 11.09.57.png]]
### Compression and few-shots classification
### Molecular graph generation
## Thoughts
___
1. Nothing really new in terms of theory
2. Good story line
3. How do you find the application of Lie algebra here?