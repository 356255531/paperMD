# Supervised Dimension Contrastive Learning
This paper integrates supervised learning with dimension-wise contrastive learning to address limitations in feature diversity and high cross-correlation between representation dimensions. The key contributions include:
  1. Discriminativeness Loss: A loss function combining class correlation loss and orthogonal regularization to maximize mutual information between learned representations and class labels, ensuring that each embedding dimension contributes independently and meaningfully to class discriminability.
  2. Reduction in Redundancy: Inspired by techniques like Barlow Twins, the method reduces inter-dimensional correlations, enhancing feature diversity and generalizability.
  3. Generalization Focus: The framework explicitly targets improving out-domain transfer learning performance while maintaining competitive in-domain accuracy.
### Theoretical Concerns:
  1. Gaussian Assumption: Assuming Gaussian-distributed class variables in theoretical analysis raises validity concerns, as class variables are discrete.
  2. Orthogonal Regularization: Lack of clarity on why enforcing orthogonality is essential for improving supervised learning. Some reviewers question its reliance on full-rank assumptions for injectivity.
  3. Class Correlation Loss: Limited theoretical justification or references supporting its role in enhancing discriminative and decorrelated embeddings.
