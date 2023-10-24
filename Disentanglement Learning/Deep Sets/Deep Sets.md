[Manzil Zaheer](https://arxiv.org/search/cs?searchtype=author&query=Zaheer,+M), [Satwik Kottur](https://arxiv.org/search/cs?searchtype=author&query=Kottur,+S), [Siamak Ravanbakhsh](https://arxiv.org/search/cs?searchtype=author&query=Ravanbakhsh,+S), [Barnabas Poczos](https://arxiv.org/search/cs?searchtype=author&query=Poczos,+B), [Ruslan Salakhutdinov](https://arxiv.org/search/cs?searchtype=author&query=Salakhutdinov,+R), [Alexander Smola](https://arxiv.org/search/cs?searchtype=author&query=Smola,+A)
Venue: NeurIPS 17

## TL;DR
This work focus on a class of learning problems whose objective functions are defined on sets and stay invariant to permutations of set elements. The authors propose 
1. an architecture called **DeepSets** to deal with sets as inputs and,
2. A **deep network** by following this architecture. 
 
The authors also show the condition/structure of a function being invariant to input set permutation with theoretical guarantees.    

## Background
This paper study machine learning problems with the inputs or outputs being permutation invariant sets rather than fixed dimensional. An example is the task of set expansion: where given a set of objects that are similar to each other (e.g. set of words {lion, tiger, leopard}), our goal is to find new objects from a large pool of candidates such that the selected new objects are similar to the query set (e.g. find words like jaguar or cheetah among all English words).

If the input is a set $x = \{x_1, . . . , x_M\}, x_m \in \mathcal{X}$, i.e., the input domain is the power set $X = 2^\mathcal{X}$, then we would like the response of the learnd function $f$ to be invariant to the ordering of the elements.

**Property 1** A function $f : 2^\mathcal{X} \to Y$ acting on sets must be permutation invariant to the order of objects in the set, i.e., for any permutation $$\pi : f({x_1, . . . , x_M}) = f({x_{\pi(1)}, . . . , x_{\pi(M)}}).$$
## Proposed structure
If $\mathcal{X}$ is **countable** and $Y=\mathbb{R}$, 
**Theorem 1** (permutation-invariant) A function $f(X)$ operating on a set $X$ having elements from a countable universe, is a valid set function, i.e., **invariant** to the permutation of instances in $X$, iff it can be decomposed in the form $\rho(\sum_{x\in \mathcal{X}}\phi(x))$, for suitable transformations $\phi$ and $\rho$.
Although the proofs for the case when $X$ is uncountable is difficult, the authors still conjecture that exact equality holds in general.

If $\mathcal{X} = Y = \mathbb{R}$ and $f$ is restricted to be a neural network layer. The standard neural network layer is represented as $f_\Theta(x) = \sigma(\Theta x)$ where $\Theta \in R^{M×M}$ is the weight vector and $\sigma : \mathbb{R} \to \mathbb{R}$ is a nonlinearity such as sigmoid function. The following lemma states the necessary and sufficient conditions for permutation-equivariance in this type of function.
**Lemma 1** (permutation-equivariant) The function $f_\Theta: X=\mathbb{R}^M \to \mathbb{R}^M$ defined above is permutation equivariant iff all the off-diagonal elements of $\Theta$ are tied together and all the diagonal elements are equal as well. That is $\Theta = \lambda \mathbf{I} + \gamma \cdot \mathbf{1}\mathbf{1}^T, \lambda, \gamma \in \mathbb{R}, \mathbf{1} = [1, . . . , 1]^T \in \mathbb{R}^M, \mathbf{I} \in R^{M×M}$ is the identity matrix

Similar constructions:
- de Finetti theorem,
- Representer theorem and kernel machines,
- Spectral methods.

## Architecture
**Invariant model.** Replacing $\phi$ and $\rho$ by universal approximators leaves matters unchanged, since, in particular, $\phi$ and $\rho$ can be used to approximate arbitrary polynomials.
- Each instance xm is transformed (possibly by several layers) into some representation $\phi(x_m)$. 
- The representations $\phi(x_m)$ are added up and the output is processed using the $\rho$ network in the same manner as in any deep network (e.g. fully connected layers, nonlinearities, etc.). 
- Optionally: If we have additional meta-information z, then the above mentioned networks could be conditioned to obtain the conditioning mapping $\phi(x_m|z)$.

**Equivariant model.**
- Variation 1: $f(x) = \sigma(\lambda \mathbf{I}x + \gamma \cdot \mathbf{1}\mathbf{1}^Tx$)
- Variation 1: $f(x) = \sigma(\lambda \mathbf{I}x + \gamma \cdot \text{maxpool}(x)\mathbf{1})$

## Applications
- 2D/3D Reconstructions
- 3D point clouds classification

## Discussion and comment
1. 