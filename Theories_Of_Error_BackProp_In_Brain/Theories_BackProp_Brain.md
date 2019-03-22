# Theories of Error Back-Propagation in the Brain

Review article of theories on how brain neural circuits can be seen as neural nets error back-propagation algorithm. 

## Introduction and context

- It has been demonstrated that artificial neural networks (ANN) when trained to perform tasks such as image classification, learn representations in their neurons similar representations to those seen in the brain in areas related to those tasks. This suggests that the brain may use similar algorithms.
- Despite the ANNs were inspired in the brain, the weight learning process during training seems biologically unplausible. 
- Some authors propose an efficient learning algorithm with simple plasticity rules (synaptic plasticity is the ability of synapses to strengthen or weaken over time, in response to increases or decreases in their activity).
- Over the past 30 years, it has been defended that Error back-propagation is hard for the brain to implement.

### Biologically Questionable Aspects of the Back-Propagation Algorithm

1. **No Local Error Representation**: without local representation, each synaptic weight depends on the activity and computations of all downstream errors. Biological neurons change their connection strength solely on local signals.
2. **The symmetry of forwards and backwards weights don't always make sense**: in ANNs the backpropagated errors use the same weights as the forward pass, suggesting identical connections in both directions. In biological neurons, this bidirectional connections are common but not always present!
3. **Outputs are not biological plausible**: ANNs have neurons with continuous output, whereas biological neurons use spikes. Using this spike patterns in backpropagation is non-trivial since it is unclear how to compute the gradients.

## Models of Biological Back-Propagation

- Early theories suggested that synaptic plasticity is driven by a global error signal carried by neuromodulators (Neuromodulators are neurotransmitters that diffuse through neural tissue to affect slow-acting receptors of many neurons. Examples are dopamine, serotonin, etc.). The problem with this approach is that learning in these models is slow and does not scale with bigger networks.
- More recently biological models that represent local error have been proposed and perform similarly in MNIST for examples.
- Some authors addressed the question of symmetry of weights by proving that even if the errors in ANNs are back-propagated by random connections a good performance can be achieved.
- It has been proven that spike neural networks can use a generalized backpropagation algorithm. 
- Another study proposed that when biologically realistic neurons are used, they may approximate small ANNs in their dendritic structure.
  
The paper reviews some biologically plausible models:
1. They work without minimal external control since they can compute local errors through the dynamics of the network. 
2. They consider spike time-dependent plasticity of neurons.
3. They consider the properties of pyramidal neurons and cortical microcircuits. 
4. They include both feedforward and feedback connections (that allow them not to require an external program to calculate the errors).
5. They use energy-minimization models.

## References
- Whittington, James CR, and Rafal Bogacz. "Theories of error back-propagation in the brain." Trends in cognitive sciences (2019).