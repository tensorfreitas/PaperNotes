# End-To-End Music Source Separation: Is it possible in the waveform domain?

Explores the time-domain by arguing that spectrum based techniques ignore the phase of the signal, studying the viability of having a time end-to-end model for music source separation. 

They propose a Wavenet-based model and benchmark it against other models like DeepConvSep and a Wave-U-net to prove this is possible. 

## Introduction

- Waveform domain preserves all the information available in the raw signal, but it is rare to find identical waveforms by the same sound source (since phase information is unpredictable).
- If we consider solely the magnitude or power spectrograms the phase related problems disappear (since similar realizations of the same sound, although different on phase, have similar representation in the time-frequency plane).
- Even using frequency information the phase is still needed to reconstruct the waveforms in the time-domain (generally the original mixture phase is used). 
- Power spectrograms are additive and can approximate time domain summation, but magnitude ones don't.
- There is discarded information in the phase domain and also the use of the original mixture phase can theoretically limit performance and introduce artifacts.
- In the waveform domain, we have high dimensionality, making it hard to model.