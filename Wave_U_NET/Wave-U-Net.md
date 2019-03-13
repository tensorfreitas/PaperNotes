# Wave-U-Net: A Multi-scale Neural Network for End-to-End Audio Source Separation



Proposes an adaptation of U-Net to the one-dimensional domain (time-domain) to perform audio source separation. 

Why time-domain?

- Most models operate on magnitude spectrum with a fixed spectral transformation and they ignore phase information
- In time domain the model should be able to model phase information without using a fixed sepctral transformation.

## Introduction

Most methods almost exclusevely operate on frequency domain :

1. Apply Short-Time Fourier Transform (STFT) to input signal, generating a complex-valued spectrogram
2. The spectogram is split into its magnitude and phase components
3. Model only uses magnitude and predicts the output magnitude spectogram for the individual sound sources
4. Then the magnitudes are combined with the mixture phase information
5. An inverse STFT is applied to the spectrogram to generate the individual audio signals

Some authors also recover the individual phase information using the Griffin-Lim algorithm.

The frequency domain has several limiations:

- It is dependent on parameters as the size and overlap of audio frames, affecting time and frequency resolution.
- These parameters need to be optimized as an additional hyperparameter of the model, since they will affect the perfomance (although generally these are fixed to specific values).
- Since phase estimation is not included, the phase is assumed incorrectly to be the same as the initial mixture (which is incorrect for overlapping partials)
- Even if Griffin-Lim algorithm is used, this method is slow and often no such signal exists. 

These reasons are behind why the authors claim that the phase information should be included in the model separation.

## References

- Stoller, Daniel, Sebastian Ewert, and Simon Dixon. "Wave-u-net: A multi-scale neural network for end-to-end audio source separation." arXiv preprint arXiv:1806.03185 (2018).