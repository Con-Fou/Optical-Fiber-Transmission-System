# Coherent Optical Receiver

### Purpose
The purpose is to develop an algorithm to counterbalance for the chromatic dispersion by means of an FIR filter with an appropriate transfer function to suppress the chromatic dispersion.

### Simulation

##### Step 1: Creating a modulated signal for transmission

* First we generate a random sequence of digits-symbols.
* We generate pulses using 16 samples/symbol and encode the generated sequence with **Unipolar-NRZ**. These pulses correspond to the envelope of the modulated signal, as the signal passes through the photodiode.

	_Unipolar_: for bit '0' we send 0, otherwise for bit '1' we send +A V (we choose A = 1).

	_NRZ_: the pulse lasts the entire symbol period.
* We modulate the pulses to have rise and fall times. (The pulses have expanded, after being modulated by convolution, so they are cut into the eyediagram).


<img src="/plots/1.png" alt="1st plot" width=800 />

##### Step 2: Import chromatic dispersion
We calculate the original signal in the frequency domain using the Discrete Fourier Transform (DFT). Let <img src="https://latex.codecogs.com/gif.latex?s_n "/>
 to be the initial sequence of pulses, which has length M. Then in the frequency field can be computed as:

<img src="https://latex.codecogs.com/gif.latex?S_k=\sum_{n=0}^{M-1}s_ne^{-j\frac{2π}{M}kn},~~ k=0,1,...,M-1"/>

<img src="https://latex.codecogs.com/gif.latex?SS=H\odot S "/>
<img src="https://latex.codecogs.com/gif.latex?ss_n = \frac{1}{M}\sum_{k=0}^{M-1}{X_ke^{j2πkn/M}},~~n=0,1,...,M-1 "/>
<img src="https://latex.codecogs.com/gif.latex?h(z,t)=\sqrt{\frac{c}{jDλ^2z}}e^{j\frac{πc}{Dλ^2z}t^2} "/>
<img src="https://latex.codecogs.com/gif.latex?H(z,ω)=e^{-j\frac{β_2z}{2}ω^2} = e^{j\frac{Dλ^2z}{4πc}ω^2} "/>

<img src="/plots/2.png" alt="2nd plot" width=800 />


<img src="https://latex.codecogs.com/gif.latex?P=\frac{|S|^2}{M^2} "/>
<img src="https://latex.codecogs.com/gif.latex?P_{CD} = \frac{|SS|^2}{M^2} "/>
<img src="https://latex.codecogs.com/gif.latex?|H(z,ω)|=1 "/>

<img src="/plots/3.png" alt="3rd plot" width=800 />

##### Step 3: Apply the filter to counterbalance the chromatic dispersion
<img src="/plots/fir.png" alt="FIR filter" width=800 />


<img src="https://latex.codecogs.com/gif.latex?b_k = \sqrt{\frac{jcT_s^2}{Dλ^2z}}e^{-j\frac{πcT_s^2}{Dλ^2z}k^2} "/>
<img src="https://latex.codecogs.com/gif.latex?\left\lfloor -\frac{N}{2} \right\rfloor ≤ k≤ \left\lfloor \frac{N}{2} \right\rfloor "/>
<img src="https://latex.codecogs.com/gif.latex?N=2* \left\lfloor\frac{|D|λ^2z}{2cT_s^2}\right\rfloor+1 "/>

<img src="/plots/4.png" alt="4th plot" width=800 />

<img src="https://latex.codecogs.com/gif.latex?filtered_{ss}[n]=(ss *b)[n] = \sum_{m=0}^{N-1}ss[n-m]b[m],~~n = N+M-1 "/>

<img src="/plots/5.png" alt="5th plot" width=800 />

<img src="/plots/optic_fiber.png" alt="Optic fiber" width=800 />

<img src="https://latex.codecogs.com/gif.latex? "/>
