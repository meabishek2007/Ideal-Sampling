# Ideal, Natural, & Flat-top -Sampling
# Aim
Write a simple Python program for the construction and reconstruction of ideal, natural, and flattop sampling.
# Tools required
Google Colab

# Theory:

1. Impulse Sampling (Ideal Sampling)

Impulse sampling is a method in which the continuous-time signal is multiplied by a train of impulses (Dirac delta functions). The output consists of instantaneous samples taken at discrete time intervals.

In this method, each sample has zero width and infinite amplitude, making it an ideal and theoretical model. It is mainly used for analysis purposes and cannot be implemented practically.

2. Natural Sampling

Natural sampling is obtained by multiplying the input signal with a periodic train of rectangular pulses. The output consists of portions of the signal during the pulse duration.

The amplitude of the sampled signal varies according to the input signal within each pulse. It is more practical than impulse sampling and preserves the original signal shape within each sampling interval.

3. Flat Top Sampling (Sample and Hold)

Flat top sampling is a practical method where the signal is sampled and the value is held constant until the next sampling instant. It is also known as sample-and-hold method.

The output appears as a staircase waveform. This method is widely used in analog-to-digital conversion but introduces a small distortion called the aperture effect.

# Program

1. IMPULSE SAMPLING:
~~~
import numpy as np
import matplotlib.pyplot as plt

# Parameters (correct values)
f = 5            # signal frequency (Hz)
fs = 100         # sampling frequency (Hz) → must be >= 2*f
t = np.linspace(0, 1, 1000)     # continuous time
ts = np.arange(0, 1, 1/fs)      # sampled time

# Signals
x = np.sin(2 * np.pi * f * t)
xs = np.sin(2 * np.pi * f * ts)

# Plot
plt.figure(figsize=(10,5))

plt.subplot(2,1,1)
plt.plot(t, x)
plt.title("Original Signal")

plt.subplot(2,1,2)
plt.stem(ts, xs)
plt.title("Impulse Sampled Signal")

plt.tight_layout()
plt.show()
~~~
2. NATURAL SAMPLING:
~~~
import numpy as np
import matplotlib.pyplot as plt

# Parameters
f = 5            # signal frequency (Hz)
fs = 50          # sampling frequency (Hz)
tau = 0.01       # pulse width
t = np.linspace(0, 1, 1000)

# Original signal
x = np.sin(2 * np.pi * f * t)

# Create pulse train (sampling signal)
sampling_signal = np.zeros_like(t)

for i in np.arange(0, 1, 1/fs):
    sampling_signal[(t >= i) & (t < i + tau)] = 1

# Natural sampled signal
xs = x * sampling_signal

# Plot
plt.figure(figsize=(10,5))

plt.subplot(3,1,1)
plt.plot(t, x)
plt.title("Original Signal")

plt.subplot(3,1,2)
plt.plot(t, sampling_signal)
plt.title("Sampling Pulse Train")

plt.subplot(3,1,3)
plt.plot(t, xs)
plt.title("Natural Sampled Signal")

plt.tight_layout()
plt.show()
~~~
3. FLAT TOP SAMPLING:
~~~
import numpy as np
import matplotlib.pyplot as plt

# Parameters
f = 5
fs = 50
t = np.linspace(0, 1, 1000)

# Original signal
x = np.sin(2 * np.pi * f * t)

# Sampling instants
ts = np.arange(0, 1, 1/fs)
xs = np.sin(2 * np.pi * f * ts)

# Pulse train
pulse = np.zeros_like(t)
for i in ts:
    pulse[(t >= i) & (t < i + 0.01)] = 1   # small pulse width

# Flat-top (sample and hold)
x_flat = np.zeros_like(t)
for i in range(len(ts)-1):
    x_flat[(t >= ts[i]) & (t < ts[i+1])] = xs[i]

# Plot
plt.figure(figsize=(10,8))

plt.subplot(4,1,1)
plt.plot(t, x)
plt.title("Original Signal")

plt.subplot(4,1,2)
plt.plot(t, pulse)
plt.title("Sampling Pulse Train")

plt.subplot(4,1,3)
plt.stem(ts, xs)
plt.title("Sampled Signal")

plt.subplot(4,1,4)
plt.step(t, x_flat, where='post')
plt.title("Flat Top Sampled Signal")

plt.tight_layout()
plt.show()
~~~

# Output Waveform:

1. IMPULSE SAMPLING:
   
<img width="989" height="690" alt="image" src="https://github.com/user-attachments/assets/e148926b-277a-4145-91db-f4f107737af8" />




2. NATURAL SAMPLING:
   
<img width="990" height="690" alt="image" src="https://github.com/user-attachments/assets/f3117138-6844-48eb-a41c-bda4178481df" />




3. FLAT TOP SAMPLING:

<img width="989" height="790" alt="image" src="https://github.com/user-attachments/assets/8bfc185f-3d81-47a8-a725-0772646eb1b3" />




# Results:

Thus, the impulse sampling, natural sampling and flat top sampling of the given continuous time signal are obtained and verified successfully.

