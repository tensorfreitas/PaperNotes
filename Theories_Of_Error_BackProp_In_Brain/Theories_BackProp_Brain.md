# Theories of Error Back-Propagation in the Brain

Review article of theories on how brain neural circuits can be seen as neural nets error back-propagation algorithm. 

## Introduction and context

- It has been demonstrated that artificial neural networks (ANN) when trained to perform tasks such as image classification, learn representations in their neurons similar representations to those seen in the brain in areas related to those tasks. This suggests that the brain may use similar algorithms.
- Despite the ANNs were inspired in the brain, the weight learning process during training seems biologically unplausible. 
- Some authors propose an efficient learning algorithm with simple plasticity rules (synaptic plasticity is the ability of synapses to strengthen or weaken over time, in response to increases or decreases in their activity).
- Over the past 30 years, it has been defended that Error back-propagation is hard for the brain to implement.

### Biologically Questionable Aspects of the Back-Propagation Algorithm

1. No Local Error Representation: without local representation, each synaptic weight depends on the activity and computations of all downstream errors. Biological neurons change their connection strength solely on local signals.
2. The symmetry of forwards and backwards weights don't always make sense: in ANNs the backpropagated errors use the same weights as the forward pass, suggesting identical connections in both directions. In biological neurons, this bidirectional connections are common but not always present!
3. Outputs are not biological plausible: ANNs have neurons with continuous output, whereas biological neurons use spikes. Using this spike patterns in backpropagation is non-trivial since it is unclear how to compute the gradients.

## References
- Whittington, James CR, and Rafal Bogacz. "Theories of error back-propagation in the brain." Trends in cognitive sciences (2019).