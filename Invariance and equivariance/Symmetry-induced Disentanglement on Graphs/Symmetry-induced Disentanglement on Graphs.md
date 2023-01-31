# Symmetry-induced Disentanglement on Graphs

Authors:[Giangiacomo Mercatali](https://openreview.net/profile?id=~Giangiacomo_Mercatali1), [Andre Freitas](https://openreview.net/profile?id=~Andre_Freitas1), [Vikas Garg](https://openreview.net/profile?email=vikas.garg%40aalto.fi)
Venue: [**NeurIPS 2022 Conference** homepage](https://openreview.net/group?id=NeurIPS.cc/2022/Conference "Venue Homepage")

## Summary
___
This present conditional symmetry as the notion of disentanglement in graph structure. The contribution of this method can be structured as following:
1. uses Lie algebra to encode certain graph properties (No explicit indication if they are independent factors as in ICA) using e.g., VAE.
2. segregates the latent space into uncoupled and entangled parts (Isn't the meaning of disentanglement to find the independent factors, or recover the original sources?)

## Method in short
___
The author use invariance for "symmetry regularization" to guarantee equivariance.

## Background and Problem to be solved
___
The author emphasis on the limitation of equivariant nets:
1. needs specialized implemetation
2. is only capable of dealing with linear groups, e.g., permuataion group, and continuous Lie groups

Basic arguments:
1. Geometry is concerned with invariant quantities under certain transformation.
2. Euclidean group preserves the angle, length and parallelism of lines. Enforcing equivariant to Euclidean group is sufficient to ensure the equal distance of two points before and after transformation.

Intuitive example:
![[Pasted image 20230116210158.png]]
The group action can have a non-linear and unknown action on the input space. For instance, In the pendulum example aboved, the 3-dimensional Euclidean group $E(3)$ acts on the value of each input image pixel using an unknown and non-linear action. The color and brightness encode the pendium angle and angular velocity (darker is clock-wise and brighter is anticlock-wise, zero in middle), accordingly.
The SymReg objective for the Euclidean group learns this embedding by preserving the pairwise distance between the codes before $dist(f (x), f (x′))$ and after $dist(f (t_X (g, x)), f (t_X (g, x)))$ transformations of the input by $t_X$ with $dist(\cdot)$ being a distance metric.

### Preliminaries
___
- A group $G$ equipped with a group action operator ($G$-action operator) on a set 
$X$ is defined by a function (transformation) $t ∶ G \times X \to X$.
- Transformation symmetry of a embedding $f:X \to Z$:
$$f (t_X (g, x)) = t_Z (g, f (x)),\ \forall (g, x) \in G \times X$$

## Approach
___
#### Corollary 1: 
*Any* ***injective*** *function* $f ∶ X \to Z$ *is equivariant to any transformation group* $t_X ∶ G \times  X \to X$, *if we define G action on the embedding space as*
$$t_Z (g, z) \equiv f (t_X (g, f^{-1}(z))), \ \forall g, z \in G \times Z$$
The corollary above tells you two things,
1. Since $f$ is injective, $x=f^{-1}$ recovers all $z \in Z$ , where you can have non-linear group actions $t_X \in T_X$ while having linear $t_z$ (somehow without proof if it works for all possible non-linear group actions).
2. Corollary 1 assumes injectivity of $f$ for the entire $X$. In practice, you have many ways to enforce it, e.g., using a decoder such as momentum decoder, hinge loss or any loss monotonically decrease with distance (almost all negative distance metric?? then why mention so??).

#### More Informed but Less Practical Setting: with Access to the Group Element $g \in G$
When the dataset contains the tripples $(x, g, x_t = t_X (g, x))$, then the invariant loss can be written as
$$L^{informed}_G (f, D) = \sum_{(x,g,xt)\in D} \ell (f (x_t) − t_Z (g, f (x))).$$
Depending on the group structure and properties, the author introduces the equivariance as regularizer,
- Euclidean Group (Distance preserving):
$$L_{E(n)}(f, D)=\sum_{((x, x_t), (x', x'_{t}))} \ell(||f(x)-f(x')|| - ||f(x_t) - f(x_t')||)$$
- Orthognal Group (Angle preserving):
$$L_{O(n)}(f, D)=\sum_{((x, x_t), (x', x'_{t}))} \ell(f(x)^Tf(x') - f(x_t)^Tf(x_t'))$$
- Conformal Group
- Unitary Group and etc.

####  More General Setup
Find a invariant ploynomial^[These polynomials form an algebra studied in the field of invariant theory] $P(\cdot)$ associated with the underlying group such that $P (t_Z(z, g)) = P (z), \ \forall g \in G.$ The existence of such polynomials habe been answer by Hilbert^["Our proposal, in its most general form is to ensure invariance of polynomial bases within the orbits of the latent space before-after transformation of the input."] and this also includes classical Lie Groups.
Some other examples includes Lorentz, Poincare group (where their polynomial bases are determinant) in the Minkowski space and etc. They preserves different invariance of two samples before and after certain embedding.

#### Decomposing the Representation
The author denotes the decomposition **active** to contrast it with the **passive** case, where the action of different subgroups is always mixed in the dataset (the decomposition of group into subgroups can not be revealed in the dataset).

For the active case, the loss function 
$$L^{active}_G (f, D) = \sum_{i=1}^k L_{G_i}(f_i, D_i)+ L^{inv}_{G/G_i} (fi, D/D_i),$$
whose first term is the symmetry regularization and second term enforcing the invariance to the group action, e.g., $∥f (x) − f (t_X (g, x))∥$.

## Experiment
___
#### Qualitative Analysis
**The Pendulum**: 32 × 32 pixels input, group action is the torques applied to the pendulum. The objective function is
$$L_{E(n)}(f, D)=\sum_{((x, x_t), (x', x'_{t}))} \ell(||f(x)-f(x')|| - ||f(x_t) - f(x_t')||)$$
The visualization of the learned representations:
![[Pasted image 20230116210158.png]]
The color and brightness encode the pendium angle and angular velocity (darker is clock-wise and brighter is anticlock-wise, zero in middle), accordingly.

**Mountain Car**:
The visualization of the learned representations:
![[Pasted image 20230117090449.png]]
Colors show the change in the location and the brightness shows
the velocity.

As a comparision, the visualization of the representation learned using SimCLR and VAE
![[Pasted image 20230117090844.png]]

#### Quantitative Analysis
The author picked Atari games Pong and Space Invaders as our environments for the world modeling experiments. He trained amd froze the encoder using Euclidean SymReg
$$L_{E(n)}(f, D)=\sum_{((x, x_t), (x', x'_{t}))} \ell(||f(x)-f(x')|| - ||f(x_t) - f(x_t')||).$$
And then learned an MLP based transition function in the latent space and finally reprorted the Rank 1 (H@1) and Mean Reciprocal Rank (MRR), which are invariant to the embedding scale. These evaluation metrics measure the relative closeness of the following state’s representation predicted by the transition model and the representation of the observed next state.
![[Pasted image 20230117092501.png]]
![[Pasted image 20230117092518.png]]

## Conclusion and Thoughts
___
1. Identifying the group invariants can be still cumbersome
2. What is the role of the invariance term here? Not used at all?
3. What happens when you don't have the proper distance metric of example pairs?
4. What would be interesting for the multi-object disentanglement learning?