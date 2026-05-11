# Ex1 : Ideal Sampling, Natural Sampling and Flat-top Sampling
## AIM:
Write a simple Python program for the construction and reconstruction of ideal, natural, and flattop sampling.

## TOOLS REQUIRED:
Python IDE

## PROGRAM:

#### IDEAL SAMPLING:
```import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import resample

# Parameters
fs = 100      # Sampling frequency
f = 5         # Signal frequency

# Time vector
t = np.arange(0, 1, 1/fs)

# Continuous signal
x = np.sin(2 * np.pi * f * t)

# Impulse sampling
xs = x.copy()

# Reconstruction using resampling
xr = resample(xs, len(t))

# Plotting
plt.figure(figsize=(10, 8))

plt.suptitle(
    "NAME: VISHAL D\nREG NO: 212224060305",
    fontsize=12,
    fontweight='bold'
)

# Continuous Signal
plt.subplot(3, 1, 1)
plt.plot(t, x)
plt.title("Continuous Signal (fs = 100 Hz)")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)

# Sampled Signal
plt.subplot(3, 1, 2)
plt.stem(t, xs, basefmt=" ")
plt.title("Sampled Signal (Impulse Sampling)")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)

# Reconstructed Signal
plt.subplot(3, 1, 3)
plt.plot(t, xr, 'r--')
plt.title("Reconstructed Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)

plt.tight_layout(rect=[0, 0, 1, 0.93])
plt.show()
```

#### NATURAL SAMPLING:
```import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, lfilter

# Parameters
fs = 1000      # Sampling frequency
T = 1          # Time duration
fm = 5         # Message signal frequency
fp = 50        # Pulse frequency

# Time vector
t = np.arange(0, T, 1/fs)

# Message signal
m = np.sin(2 * np.pi * fm * t)

# Pulse train
pw = fs // (2 * fp)   # Pulse width

p = np.zeros_like(t)
p[::fs // fp] = 1
p = np.convolve(p, np.ones(pw), mode='same')

# Natural sampling
nat = m * p

# Reconstruction using Low Pass Filter
b, a = butter(4, 10 / (0.5 * fs), 'low')
rec = lfilter(b, a, nat)

# Plotting
plt.figure(figsize=(10, 9))

plt.suptitle(
    "NAME: VISHAL D\nREG NO: 212224060305",
    fontsize=12,
    fontweight='bold'
)

# Message Signal
plt.subplot(4, 1, 1)
plt.plot(t, m)
plt.title("Message Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)

# Pulse Train
plt.subplot(4, 1, 2)
plt.plot(t, p)
plt.title("Pulse Train")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)

# Natural Sampling
plt.subplot(4, 1, 3)
plt.plot(t, nat)
plt.title("Natural Sampling")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)

# Reconstructed Signal
plt.subplot(4, 1, 4)
plt.plot(t, rec, color='g')
plt.title("Reconstructed Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)

plt.tight_layout(rect=[0, 0, 1, 0.93])
plt.show()
```

#### FLAT-TOP SAMPLING:
```import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, lfilter

# Parameters
fs = 1000      # Sampling frequency
T = 1          # Time duration
fm = 5         # Message signal frequency
fp = 50        # Sampling frequency

# Time vector
t = np.arange(0, T, 1/fs)

# Message signal
m = np.sin(2 * np.pi * fm * t)

# Sampling
bd = fs // fp                  # Block duration
idx = np.arange(0, len(t), bd)

flat = np.zeros_like(t)

# Flat-top sampling
for i in idx:
    flat[i:i + bd//2] = m[i]

# Low-pass filter for reconstruction
b, a = butter(4, (2 * fm) / (0.5 * fs), 'low')
recon = lfilter(b, a, flat)

# Plotting
plt.figure(figsize=(10, 9))

plt.suptitle(
    "NAME: VISHAL D\nREG NO: 212224060305",
    fontsize=12,
    fontweight='bold'
)

# Message Signal
plt.subplot(4, 1, 1)
plt.plot(t, m)
plt.title("Message Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)

# Sampling Instants
plt.subplot(4, 1, 2)
plt.stem(t[idx], np.ones_like(idx), basefmt=" ")
plt.title("Sampling Instants")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)

# Flat-Top Sampled Signal
plt.subplot(4, 1, 3)
plt.plot(t, flat)
plt.title("Flat-Top Sampled Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)

# Reconstructed Signal
plt.subplot(4, 1, 4)
plt.plot(t, recon, color='g')
plt.title("Reconstructed Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)

plt.tight_layout(rect=[0, 0, 1, 0.93])
plt.show()
```

## OUTPUT WAVEFORM:
#### IDEAL SAMPLING:
<img width="989" height="788" alt="image" src="https://github.com/user-attachments/assets/f6bdb3e0-af14-437b-974d-de9f1c4581b1" />


#### NATURAL SAMPLING:
<img width="981" height="886" alt="image" src="https://github.com/user-attachments/assets/7d1d6ead-908d-4343-aa0a-e7ab3ff4b3d6" />


#### FLAT-TOP SAMPLING:
<img width="981" height="886" alt="image" src="https://github.com/user-attachments/assets/44fda3ad-0369-436c-ae78-17ab28477fc7" />


## RESULT:
Thus, the construction and reconstruction of Ideal, Natural and Flat-top sampling were successfully implemented using Python, and the corresponding waveforms were obtained.
