# MixMatch: A Holistic Approach to Semi-Supervised Learning

Proposes a new SOTA for Semi-Supervised Learning that guesses low-entropy labels for data-augmented unlabeled samples and using Mixup to combine label and unlabeled data. 

## Introduction

A lot of recent of Semi-supervised Learning try to add a loss term that operates on unlabeled data and enables the model to generalize better to unseen data. This loss term can fall into one of three classes: 
- Entropy Minimization: encourages the model to predict confidently on unlabeled data.
- Consistency Regularization: the model should produce the same output distribution when inputs are perturbed.
- Generic Regularization: avoid overfitting.

**MixMatch introduces a single loss that unifies all these classes of losses**: reduces entropy while maintaining consistency and remaining compatible with traditional regularization techniques.

## Related Work

### Consistency Regularization

Data Augmentation is frequently used with the idea of a classifier should output the same class distribution for unlabeled example, even after it has been augmented. 

Examples of works of these techniques are the Π-Model by Nvidia, Temporal Ensembling for semi-supervised learning and Mean Teacher (exponential moving average of model parameters values). The problem with these works is that they use domain-specific augmentations. VAT (Virtual Adversarial Training) tries to address this by computing an additive perturbation to the inputs which will maximally change the output class distributions. 

### Entropy Minimization

These methods assume that the decision boundary should not pass through high-density regions of the marginal data distribution. One way to encourage this is to add a loss term that forces the model to predict low-entropy prediction on unlabeled data (Semi-Supervised Learning by entropy minimization). VAT, combined with this also improves the results. Pseudo-Label does entropy-minimization by creating "hard-labels" from high-confidence predictions on unlabeled data that are used as training targets to improve the model. 

### Traditional Regularization

An example of this type of methods is applying a _L_2_ penalization of the model parameters, that with gradient descent will correspond to exponentially decay the weight values to zero. 

More recently MixUp regularizer that proposes convex combinations of both inputs and labels. This tries to encourage the model to have linear behavior between examples while requiring that by requiring that the model’s output for a convex combination of two inputs is close to the convex combination of the output for each individual input.