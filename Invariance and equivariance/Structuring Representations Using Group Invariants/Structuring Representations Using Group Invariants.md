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

## Approach
___
#### Preliminaries
- A group $G$ equipped with a group action operator ($G$-action operator) on a set 
$X$ is defined by a function (transformation) $t ∶ G \times X \to X$.
- Transformation symmetry of a embedding $f:X \to Z$:
$$f (t_X (g, x)) = t_Z (g, f (x)),\ \forall (g, x) \in G \times X$$
### Corollary 1: 
*Any injective function f ∶ X → Z is equivariant to any transformation group $t_X ∶ G \times  X \to X$, if we define G action on the embedding space as*
$$t_Z (g, z) \equiv f (t_X (g, f^{-1}(z))), \ \forall g, z \in G \times Z$$

## Experiment
## Conclusion and Thoughts
