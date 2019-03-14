# Wave-U-Net: A Multi-scale Neural Network for End-to-End Audio Source Separation

Proposes an adaptation of U-Net to the one-dimensional domain (time-domain) to perform audio source separation. 

Why time-domain?

- Most models operate on magnitude spectrum with a fixed spectral transformation and they ignore phase information
- In time-domain, the model should be able to model phase information without using a fixed spectral transformation.

## Introduction

Most methods almost exclusively operate on frequency domain :

1. Apply Short-Time Fourier Transform (STFT) to input signal, generating a complex-valued spectrogram
2. The spectrogram is split into its magnitude and phase components
3. The model only uses magnitude and predicts the output magnitude spectrogram for the individual sound sources
4. Then the magnitudes are combined with the mixture phase information
5. An inverse STFT is applied to the spectrogram to generate the individual audio signals

Some authors also recover the individual phase information using the Griffin-Lim algorithm. This iterative algorithm works as follows:

1. Start with a complex-valued spectrogram with the desired magnitude but with the imaginary part with uniform noise (no phase information)
2. Perform Inverse STFT (ISTFT) to obtain an audio signal based on magnitude information
3. Apply STFT to the generated audio signal, getting a spectrogram with some imperfect phase information.
4. On the generated spectrogram replace the real part with the original magnitude spectrogram.
5. Redo Step 2

The process is done several times until some end criteria. The phase information will iteratively be more relevant.


The frequency domain has several limitations:

- It is dependent on parameters as the size and overlap of audio frames, affecting time and frequency resolution.
- These parameters need to be optimized as an additional hyperparameter of the model since they will affect the performance (although generally these are fixed to specific values).
- Since phase estimation is not included, the phase is assumed incorrectly to be the same as the initial mixture (which is incorrect for overlapping partials)
- Even if Griffin-Lim algorithm is used, this method is slow and often no such signal exists. 

These reasons are behind why the authors claim that the phase information should be included in the model separation.

## References

- Stoller, Daniel, Sebastian Ewert, and Simon Dixon. "Wave-u-net: A multi-scale neural network for end-to-end audio source separation." arXiv preprint arXiv:1806.03185 (2018).