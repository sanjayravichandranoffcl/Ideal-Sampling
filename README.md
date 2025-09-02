# Ideal, Natural, & Flat-top -Sampling

# Aim

Write a simple Python program for the construction and reconstruction of ideal, natural, and flattop sampling.

# Tools required

IDLE Python(3.12 64-bit)

# Program

**IDEAL SAMPLING CODE **

```python
import numpy as np
import matplotlib.pyplot as plt
fm = 5          
fs = 40         
t = np.arange(0, 1, 0.001)
m = np.sin(2*np.pi*fm*t)  
ts = np.arange(0, 1, 1/fs)
ms = np.sin(2*np.pi*fm*ts)
reconstructed = np.zeros(len(t))
for k in range(len(ts)):
    reconstructed += ms[k] * np.sinc((t - ts[k]) * fs)
plt.figure(figsize=(10,8))
plt.subplot(3,1,1)
plt.plot(t, m, 'b', label="Continuous Signal")
plt.title("Continuous Signal (fm=5 Hz)")
plt.xlabel("Time (s)"); plt.ylabel("Amplitude")
plt.grid(True); plt.legend()
plt.subplot(3,1,2)
plt.stem(ts, ms, linefmt='r-', markerfmt='ro', basefmt=" ", label="Sampled Signal")
plt.title("Ideal Sampling (fs=40 Hz)")
plt.xlabel("Time (s)"); plt.ylabel("Amplitude")
plt.grid(True); plt.legend()
plt.subplot(3,1,3)
plt.plot(t, reconstructed, 'r', label="Reconstructed Signal")
plt.title("Reconstructed Signal using sinc")
plt.xlabel("Time (s)"); plt.ylabel("Amplitude")
plt.grid(True); plt.legend()
plt.tight_layout()
plt.show()

```


**NATURAL SAMPLING CODE **

```python

import numpy as np
import matplotlib.pyplot as plt
fm = 5
fs = 40
t = np.arange(0, 1, 0.001)
m = np.sin(2*np.pi*fm*t)
pulse_width = 1/fs * 0.5
natural = np.zeros(len(t))
for ts in np.arange(0, 1, 1/fs):
    idx = (t >= ts) & (t < ts + pulse_width)
    natural[idx] = m[np.argmin(abs(t - ts))]
window = int(1/(fs*0.001))
reconstructed = np.convolve(natural, np.ones(window)/window, mode='same')
plt.figure(figsize=(10,8))
plt.subplot(3,1,1)
plt.plot(t, m, 'b', label="Original Message Signal")
plt.title("Original Message Signal")
plt.xlabel("Time (s)"); plt.ylabel("Amplitude")
plt.grid(True); plt.legend()
plt.subplot(3,1,2)
plt.plot(t, natural, 'c', label="Natural Sampled Signal")
plt.title("Natural Sampling")
plt.xlabel("Time (s)"); plt.ylabel("Amplitude")
plt.grid(True); plt.legend()
plt.subplot(3,1,3)
plt.plot(t, reconstructed, 'r', label="Reconstructed Signal (LPF)")
plt.title("Reconstructed Signal using Low-Pass Filter")
plt.xlabel("Time (s)"); plt.ylabel("Amplitude")
plt.grid(True); plt.legend()
plt.tight_layout()
plt.show()

```



**FLAT-TOP SAMPLING CODE**

```python
import numpy as np
import matplotlib.pyplot as plt
fm = 5
fs = 40
t = np.arange(0, 1, 0.001)
m = np.sin(2*np.pi*fm*t)
flat_top = np.zeros(len(t))
ts = np.arange(0, 1, 1/fs)
for k in range(len(ts)-1):
    idx1 = np.argmin(abs(t - ts[k]))
    idx2 = np.argmin(abs(t - ts[k+1]))
    flat_top[idx1:idx2] = m[idx1]
window = int(1/(fs*0.001))
reconstructed = np.convolve(flat_top, np.ones(window)/window, mode='same')
plt.figure(figsize=(10,8))
plt.subplot(3,1,1)
plt.plot(t, m, 'b', label="Original Message Signal")
plt.title("Original Message Signal")
plt.xlabel("Time (s)"); plt.ylabel("Amplitude")
plt.grid(True); plt.legend()
plt.subplot(3,1,2)
plt.plot(t, flat_top, 'm', label="Flat-Top Sampled Signal")
plt.title("Flat-Top Sampling (Sample-and-Hold)")
plt.xlabel("Time (s)"); plt.ylabel("Amplitude")
plt.grid(True); plt.legend()
plt.subplot(3,1,3)
plt.plot(t, reconstructed, 'g', label="Reconstructed Signal (LPF)")
plt.title("Reconstructed Signal using Low-Pass Filter")
plt.xlabel("Time (s)"); plt.ylabel("Amplitude")
plt.grid(True); plt.legend()
plt.tight_layout()
plt.show()

```


# Output Waveform

**IDEAL SAMPLING OUTPUT**

<img width="1860" height="942" alt="image" src="https://github.com/user-attachments/assets/fb1e5f8e-4021-4b9d-b964-95d94e8b6bb1" />


**NATURAL SAMPLING OUTPUT**

<img width="1846" height="948" alt="image" src="https://github.com/user-attachments/assets/c431447d-859c-44da-91ea-3cc5ea785370" />

**FLAT-TOP SAMPLING OUTPUT **

<img width="1866" height="934" alt="image" src="https://github.com/user-attachments/assets/7090a201-6539-446e-bef8-5bf2603d6429" />

# Results

Thus, the python programs for ideal sampling, natural sampling and flat-top sampling has been executed and verified successfully.

# Hardware experiment output waveform.
