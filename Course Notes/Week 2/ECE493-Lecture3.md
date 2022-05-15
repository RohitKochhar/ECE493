# ECE493 Lecture 3: Physical Layer

(May 12th, 2022)

- [ECE493 Lecture 3: Physical Layer](#ece493-lecture-3-physical-layer)
  - [Source Encoding](#source-encoding)
  - [Channel Encoding](#channel-encoding)
  - [Modulation](#modulation)
  - [Signal Propagation](#signal-propagation)
  - [Power Saving Mechanisms](#power-saving-mechanisms)
  - [Data Link Layer](#data-link-layer)

## Source Encoding
- Source encoding transforms an analog signal into a digital sequence.
- The process consists of sampling, quantizing and encoding.
- Most often done using an ADC.

## Channel Encoding
- The main purpose of a channel encoder is to produce a sequence of data that is robust to noise and to provide error detection and forward error correction mechanisms.
- In simple and cheap transceivers, forward error correction is costly and therefore the task of channel encoding is limited to the detection of errors in packet transmission.

## Modulation
- Modulation is a process by which the characteristics (amplitude, frequency and phase) of a carrier signal are modified according to the message signal.
- Modulation has several advantages
  - The message signal will become resilient to noise
  - The channel's spectrum can be used efficiently
  - Signal detection will be simple.

## Signal Propagation
- WSNs operate in the license-free ISM spectrum, so they must share the spectrum with other devices operating in the same spectrum, such as phones, WLAN, Bluetooh, Microwave ovens and more.
- Simple channel models ignore the effect of interference and considers the surrounding noise as the predominant factor affecting the transmitted signal.
- Noise can be modeled as an *Additive White Gaussian Noise (AWGN)* that has a constant spectral density over the entire operating spectrum and a normal amplitude distribution. Therefore with this model, the noise distorts the amplitude of the transmitted signal.
- To deal with noise, we can increase the received power so that the signal-to-noise ratio is significantly high and the channel becomes agnostic to noise.

## Power Saving Mechanisms
- Energy consumption minimization is very important when designing the physical layer for WSN, along with the usual effects such as:
  - Scattering
  - Shadowing
  - Reflection
  - Diffraction
  - Multipath
  - Fading
- The amount of time and power needed to wake-up a radio is not negligible and thus just turning off the radio whenever not in use is not necessarily efficient.
- The energy characteristics of the start-up time shojuld also be taken into account when designing the size of the data link packets. 

## Data Link Layer