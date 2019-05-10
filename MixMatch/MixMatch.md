# MixMatch: A Holistic Approach to Semi-Supervised Learning

Proposes a new SOTA for Semi-Supervised Learning that guesses low-entropy labels for data-augmented unlabeled samples and using Mixup to combine label and unlabeled data. 

## Introduction

A lot of recent of Semi-supervised Learning try to add a loss term that operates on unlabeled data and enables the model to generalize better to unseen data. This loss term can fall into one of three classes: 
- Entropy Minimization: encourages the model to predict confidently on unlabeled data.
- Consistency Regularization: the model should produce the same output distribution when inputs are perturbed.
- Generic Regularization: avoid overfitting.

**MixMatch introduces a single loss that unifies all these classes of losses**: reduces entropy while maintaining consistency and remaining compatible with traditional regularization techniques.