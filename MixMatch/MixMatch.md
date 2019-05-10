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

## MixMatch

MixMatch is presented as a holistic approach with all the previously referred paradigms. 
Given a batch of size N with N/2 labeled samples and N/2 unlabeled samples, it applies augmentations to all the batch:
1. Each labeled sample is augmented in the batch
2. For each unlabeled sample, K augmented samples are generated
3. A guess label for the unlabeled sample is done by averaging the model predictions across the K augmented samples. 
4. After having an average prediction, a sharpening function is applied to reduce the entropy of the label distribution (probability calibration).
5. The final step of MixMatch is done by using MixUp to both labeled and unlabeled samples (and their calibrated guesses). The authors claim that mixing labeled and unlabeled samples improve the performance of the system. The authors modify MixUp forcing the generated samples to be closer to an original sample. 


The used loss tries to minimize the cross-entropy between the labeled samples ground truth and the predictions and also minimize the squared L2 loss between the augmented unlabeled samples. The gradients are not propagated through the guessed unlabeled samples. 

## Experiments

- Wide ResNet-28 model used.
- Exponential Moving Average of the model parameters. 
- The parameter T of the probability calibration is fixed and the number of augmentations per unlabeled samples is also set at 2.
- The MixUp parameters are changed on a per-dataset basis. 
- Weight Decay used for regularization.
- CIFAR-10, CIFAR-100, SVNH and STL-10 datasets used with variations of the number of labeled examples used. 

## Results

- MixMatch outperforms all the other approaches. 
- On CIFAR-10 it obtains an error rate of 11.08% with only 250 labels vs 36.03% of VAT with 250 labels.
- On CIFAR-100 it outperforms or matches the SOTA. 
- On SVNH the performance is quite consistent with a different number of labeled samples. MixMatch nearly matches the fully-supervised performance on the same
training set almost immediately.
- On STL-10, it surpasses both the state-of-the-art for 1000 examples as well as the state-of-the-art using all 5000 labeled examples.

## Ablation Study

The authors show that all components contribute to the decrease of the error rate on CIFAR-10, especially with fewer labels. 

## Privacy-Preserving Learning, and Generalization

MixMatch can help achieve a dramatically better accuracy-privacy trade-off for differential privacy.