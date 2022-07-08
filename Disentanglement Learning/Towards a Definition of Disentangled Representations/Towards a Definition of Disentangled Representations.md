# Towards a Definition of Disentangled Representations
Authors: [Irina Higgins](https://arxiv.org/search/cs?searchtype=author&query=Higgins%2C+I), [David Amos](https://arxiv.org/search/cs?searchtype=author&query=Amos%2C+D), [David Pfau](https://arxiv.org/search/cs?searchtype=author&query=Pfau%2C+D), [Sebastien Racaniere](https://arxiv.org/search/cs?searchtype=author&query=Racaniere%2C+S), [Loic Matthey](https://arxiv.org/search/cs?searchtype=author&query=Matthey%2C+L), [Danilo Rezende](https://arxiv.org/search/cs?searchtype=author&query=Rezende%2C+D), [Alexander Lerchner](https://arxiv.org/search/cs?searchtype=author&query=Lerchner%2C+A)
Venue: Arxiv

## Comments
This paper gives a formal definition of disentangled representation by connecting **symmetry transformation** to **vector representation** using group and representation theory.  It also builds a framework to establish a formal connection between symmetry groups and vector representations, which in turn helps resolve many outstanding points of contention surrounding disentangled representation learning.

## Summary

## Background
Until now, there is **NO** formal definition of disentangling, because there is no clear formal notion of world structure beyond toy datasets with a known ground truth generative process.

## Problem

## Definition
**Preliminaries**: 
- group ($G$), binary operator ($\circ : G × G \to G$), group decomposition into a direct product of subgroups ($G = G_1 × G_2$), set $X$, group action on $X\ (\cdot : G \times X \to X)$.
- vector space ($V$), tensor product of vector spaces ($V \bigotimes W$), group action on a vector space ($\cdot : G \times V \to V$), group representation ($\rho : G \to GL(V )$), direct sum of representations ($\rho_1 \bigoplus \rho_2$), irreducible representation, tensor product representation ($\rho_1 \bigoplus \rho_2 : G \to GL(V \bigotimes W )$).
 
### Disentangled group action
The action is disentangled (with respect to the decomposition of $G$) if there is a decomposition $X = X_1 \times X_2$, and actions $·_i : G_i \times X_i \to X_i, i \in\{1,2\}$ such that 
$$(g_1, g_2) · (v_1, v_2) = (g_1 ·_1 v_1, g_2 ·_2 v_2).$$
### Linear Disentangled group representation
a group representation $\rho : G \to GL(V )$ is linearly disentangled with respect to the group decomposition $G = G_1 × G_2$ if there exists a decomposition $V = V_1 \bigoplus V_2$ and representations $\rho_i : G_i \to GL(V_i), i \in \{1,2\}$ such that $rho = ρ_1 \bigoplus ρ_2$, that is 
$$\rho(g_1, g_2)(v_1, v_2) = (\rho_1(g_1)v_1, \rho_2(g_2)v_2).$$
All of the above extends in an obvious way to decompositions $G = G_1 \times ... \times G_n$. In that case, the irreducible representations of G will be of the form $\rho_1 \bigotimes ... \bigotimes \rho_n$, where each $\rho_i, i \in \{1..n\}$ is an irreducible representation of $G_i$, and any representation $\rho$ of $G$ will be a direct sum of such representations.

### Disentangled representation
Let $W$ be the set of world-states (semantic space). We suppose that there is a generative process $b : W \to O$ leading from world-states to observations (these could be pixel, retinal, or any other potentially multi-sensory observations), and an inference process $h : O \to Z$ leading from observations to an agent’s representations. At times we will assume that $Z$ is a vector space (whereas $W$ is assumed only to be a set). We consider the composition $f : W \to Z, f = h \circ b$.

We want the action on $Z$ to correspond to the action on $W$ . This can be achieved if the following diagram commutes:
$$ 
\begin{CD} 
	G \times W @>\cdot_W>> W\\ 
	@VVid_G \times fV @VVfV\\
	G \times Z @>\cdot_Z>> Z
\end{CD} 
$$
Or the following condition is satisfied: 
$$g \cdot_Z f(w)= f(g \cdot_W w), \forall g \in G, w \in W.$$ and
$$
\forall i \in [1, m], g_i \cdot_Z f_i(w_i)=f_i(g_i \cdot_W w_i)
$$
But there are some limitation in practice,
1. Such disentangled actions $\cdot_W$ and $\cdot_Z$  exist,
2. $f$ is bijective.
If $f$ is injective but not surjective, then this recipe does not tell us how to define the action on the part of $Z$ which is not in the image $f (W)$. However, this does not matter: we do not care about all of $Z$, but only about the action of $G$ on the parts of $Z$ that are mapped to by $f (W )$. If $f$ is not injective, then there exist $w_1$, $w_2$ such that $f (w_1) = f (w_2)$. For example, this may happen because different world states give rise to the same observations, because of occlusion. In theory this can be a problem, however, such non-invertible mappings can be made invertible in practice through active sensing, as discussed in the paper[^1].

In other words, a representation $Z$ is disentangled with respect to the decomposition $G = G_1 \times ... \times G_n$ if 
1. There is an action $\cdot : G \times Z \to Z$, 
2. The map $f : W \to Z$ is equivariant between the actions on $W$ and $Z$, and
3. There is a decomposition $Z = Z_1 \times ... \times Z_n$ or $Z = Z_1 \bigotimes ... \bigotimes Z_n$ such that each $Z_i$ is fixed by the action of all $G_j, j\neq i$ and affected only by $G_i$.

### Linear disentangled representation
Then a linear disentangled representation is just an $f : W \to Z$ that admits such an action, and is disentangled with respect to a decomposition $G = G_1 \times G_2$. From the previous section, we see that this means that there is a decomposition $Z = Z_1 \bigoplus ... \bigoplus Z_m$, where each factor $Z_j$ is a representation either of $G_1$ or of $G_2$ alone. Specifically, what is excluded is factors of the form $\rho_1 \bigotimes \rho_2$, where $\rho_i$ is an action of $G_i$, unless at most one of the $\rho_i$ is a non-trivial representation.
$$\rho(g)f(w)= f(\rho(g)w), \forall g \in G, w \in W$$
and
$$
\forall i \in [1, m], \rho_i(g_i)f_i(w_i)=f_i(\rho_i(g_i)w_i).
$$
## Approach

## Experiment

[^1]: S. Soatto. Steps toward a theory of visual information. Technical Report UCLACSD100028, 2010.