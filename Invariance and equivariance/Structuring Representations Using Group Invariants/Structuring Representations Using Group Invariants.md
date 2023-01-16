# Structuring Representations Using Group Invariants

Authors: [Mehran Shakerinava](https://openreview.net/profile?id=~Mehran_Shakerinava1), [Arnab Kumar Mondal](https://openreview.net/profile?id=~Arnab_Kumar_Mondal1), [Siamak Ravanbakhsh](https://openreview.net/profile?id=~Siamak_Ravanbakhsh1)
Venue: [**NeurIPS 2022 Conference** homepage](https://openreview.net/group?id=NeurIPS.cc/2022/Conference "Venue Homepage")

## Short Summary
___
Learn equivariance purely based on the invariance of inputs after applying symmetries on top of it. This method offers
1. the convenience of not knowing the nonliear group actions
2. the disentangled representation

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
### Corollary 1: 
*Any* ***injective*** *function* $f ∶ X \to Z$ *is equivariant to any transformation group* $t_X ∶ G \times  X \to X$, *if we define G action on the embedding space as*
$$t_Z (g, z) \equiv f (t_X (g, f^{-1}(z))), \ \forall g, z \in G \times Z$$
The corollary above tells you two things,
1. Since $f$ is injective, $x=f^{-1}$ recovers all $z \in Z$ , where you can have non-linear group actions $t_X \in T_X$ while having linear $t_z$ (somehow without proof if it works for all possible non-linear group actions).
2. Corollary 1 assumes injectivity of $f$ for the entire $X$. In practice, you have many ways to enforce it, e.g., using a decoder such as momentum decoder, hinge loss or any loss monotonically decrease with distance (almost all negative distance metric?? then why mention so??).

### Setup 1: With access to the group element g
When the dataset contains the tripples $(x, g, x_t = t_X (g, x))$, then the invariant loss can be written as
$$L^{informed}_G (f, D) = \sum_{(x,g,xt)\in D} \ell (f (x_t) − t_Z (g, f (x))).$$
Depending on the group structure and properties, the author introduces the equivariance as regularizer,
- Euclidean Group (Distance preserving):
$$L_{E(n)}(f, D)=\sum_{((x, x_t), (x', x'_{t}))} \ell(||f(x)-f(x')|| - ||f(x_t) - f(x_t')||)$$
- Orthognal Group (Angle preserving):
$$L_{O(n)}(f, D)=\sum_{((x, x_t), (x', x'_{t}))} \ell(f(x)^Tf(x') - f(x_t)^Tf(x_t'))$$
- Conformal Group
- Unitary Group and etc.
## Experiment
## Conclusion and Thoughts
