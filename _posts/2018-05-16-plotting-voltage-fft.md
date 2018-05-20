---
title: 'Plotting the FFT of a voltage signal'
date: 2018-04-06
permalink: /posts/2018/05/plotting-voltage-fft
mathjax: true
tags:
  - measurements
  - MATLAB
---

Plotting a signal in the frequency domain is a fundamental analysis tool which can provide great insight into the signal's behaviour. Something I have struggled with in the past is getting the units correct such that the frequency-domain representation has physical significance. In this blog post I aim to outline how to properly find useful units with which to represent voltage signals.

## Decibel Volts (dBV)

Typically in modelling analogue circuits the signals of interest are voltages, with the units volts (V). When plotting the amplitude response of a signal it is useful to convert the amplitudes into decibels as this captures the large change in amplitudes that are often present in the amplitude response of signals. It should be noted that for voltages to be represented as decibels there is the unit dBV or decibel volts, which gives the voltage amplitude with respect to 1 V. This metric is only defined for RMS levels, given by

$$
\bar{v} = 20 \cdot \text{log}_{10}\left(\sqrt{\sum_{n=0}^{N-1} v[n]^2}\right)
$$

where \\(v[n]\\) is the voltage at a given timestep \\(n\\) of length \\(N\\), and \\(\bar{v}\\) notates the RMS value of the signal in dBV. Prior to finding the result in decibels, common values of the RMS value of a signal are: \\(\bar{v} = A/\sqrt{2}\\) for a sine wave with a peak amplitude of \\(A\\), and for DC the RMS value is the DC voltage itself.

These results will be used in the derivation of the amplitude response of a voltage signal in dBV.

## The DFT

The DFT or Discrete Fourier Transform converts a discrete time-domain signal into a discrete frequency-domain signal. One notable algorithm for calculating the DFT is the the [Fast Fourier Transform or FFT](https://en.wikipedia.org/wiki/Fast_Fourier_transform) which utilises the symmetry of the DFT to optimise performance, and is typically the algorithm implemented by numerical software packages e.g. MATLAB. The general DFT algorithm is given by

$$
V(m) = \frac{1}{N}\sum_{n=0}^{N-1}v[n] \cdot \mathrm{e}^{\frac{-2\pi j}{N} m\cdot n},\quad m=0,\ldots,N-1,
$$

where \\(V\\) is the DFT of the discrete time domain signal \\(v\\), each of length \\(N\\). The amplitude response in decibels is then given by \\(20 \cdot \text{log}_{10}(\lvert V \rvert)\\) or equivalently \\(10 \cdot \text{log}_{10}(\lvert V \rvert^2)\\). Though equivalent, the latter representation illustrates where **deci**bel comes from, as the logarithm is multiplied by 10. Further, the signal is converted such that the result is proportional to the power of the signal as the voltage is squared. (If the load impedance were known then the exact power could be found). This originates from how the decibel was first used as a method to compare the power of signals.

As the DFT calculates the integral of the signal over time, without scaling the output of the DFT by \\(1/N\\), \\(V\\) is actually proportional to the energy of signal.

## Plotting the magnitude of the DFT in dBV

The DFT works by comparing the measured signal to sinusoidal signals at frequencies relative to the sample rate and enumerating their similarity. This yields a set of values which indicate the sinusoidal components that are present in a signal and their amplitudes (and phases). As well as the sinusoidal components, the DFT also covers the case of DC, i.e. when the signal is constant, which is when \\(m=0\\).

To convert the DFT amplitude response into dBV then there is a scaling factor that accounts for the RMS of the two types of signals: DC and sinusoidal. This is given by

$$
k(m) =
\begin{cases}
\sqrt{2}, & m \neq 0\\
1, & m=0
\end{cases}
,\quad m=0,\ldots,N-1.
$$

For the DFT bins are scaled by the peak to RMS ratio. This results in a scaled DFT output

$$
\bar{V}(m) = k(m)V(m).
$$

## Numerical example

This can be written in MATLAB as shown this gist:

<script src="https://gist.github.com/bencholmes/19c0edaab1499162be45d9c274cee8e4.js"></script>

This can be tested by trying different amplitudes and frequencies. The following illustration uses a test signal with two sine waves (1 Vpeak @ 50 Hz, \\(\sqrt{2}\\) Vpeak @ 100 Hz) and a DC offset of 1 V.

![Two-tone and DC signal example](/images/plotting-voltages-example.png)

## Further resources

For testing the algorithm I have used [this calculator from Analog Devices](www.analog.com/en/design-center/interactive-design-tools/dbconvert.html).
