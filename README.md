# Ideal, Natural, & Flat-top -Sampling
# Aim
Write a simple Python program for the construction and reconstruction of ideal, natural, and flattop sampling.
# Tools required
Google Colab
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
   
<img width="989" height="490" alt="image" src="https://github.com/user-attachments/assets/f90f6aa2-73c0-426b-987e-9b6d944ee65c" />



2. NATURAL SAMPLING:
   
<img width="990" height="490" alt="image" src="https://github.com/user-attachments/assets/111694f0-d5ed-469f-b3b4-8cd2a933b2ba" />



3. FLAT TOP SAMPLING:

<img width="989" height="790" alt="image" src="https://github.com/user-attachments/assets/8bfc185f-3d81-47a8-a725-0772646eb1b3" />




# Results:

Thus, the impulse sampling, natural sampling and flat top sampling of the given continuous time signal are obtained and verified successfully.

