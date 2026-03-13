# ASK
# Aim
Write a simple Python program for the modulation and demodulation of ASK and FSK.
# Tools required

1.Personal Computer

2.Google Colab
# Program

# 1.ASK
~~~

import numpy as np
import matplotlib.pyplot as plt

# Parameters
fs = 1000
fc = 50
bit_rate = 10
t = np.arange(0, 1, 1/fs)

# Binary data
bits = np.random.randint(0, 2, bit_rate)
msg = np.repeat(bits, fs//bit_rate)

# Carrier
carrier = np.sin(2*np.pi*fc*t)

# ASK Modulation
ask = msg * carrier

# Simple Demodulation
demod = ask * carrier
decoded = (demod[::fs//bit_rate] > 0).astype(int)

# Plotting
plt.figure(figsize=(10,8))

plt.subplot(4,1,1); plt.plot(msg); plt.title("Message Signal")
plt.subplot(4,1,2); plt.plot(carrier); plt.title("Carrier Signal")
plt.subplot(4,1,3); plt.plot(ask); plt.title("ASK Modulated Signal")
plt.subplot(4,1,4); plt.step(range(len(decoded)), decoded); plt.title("Decoded Bits")

plt.tight_layout()
plt.show()
~~~~

# 2.FSK
~~~
import numpy as np
import matplotlib.pyplot as plt

# Parameters
fs = 1000
f1 = 50      # Frequency for bit 1
f0 = 20      # Frequency for bit 0
bit_rate = 10
t = np.arange(0, 1, 1/fs)

# Binary data
bits = np.random.randint(0, 2, bit_rate)
bit_samples = fs // bit_rate
msg = np.repeat(bits, bit_samples)

# FSK Modulation
carrier1 = np.sin(2*np.pi*f1*t)
carrier0 = np.sin(2*np.pi*f0*t)
fsk = np.where(msg == 1, carrier1, carrier0)

# Simple Demodulation (Energy detection)
demod1 = fsk * carrier1
demod0 = fsk * carrier0

bit1_energy = demod1.reshape(bit_rate, bit_samples).sum(axis=1)
bit0_energy = demod0.reshape(bit_rate, bit_samples).sum(axis=1)

decoded = (bit1_energy > bit0_energy).astype(int)

# Plot
plt.figure(figsize=(10,8))

plt.subplot(5,1,1)
plt.plot(msg)
plt.title("Message Signal")

plt.subplot(5,1,4)
plt.plot(fsk)
plt.title("FSK Signal")

plt.subplot(5,1,2)
plt.plot(carrier1)
plt.title("Carrier f1")
plt.subplot(5,1,3)
plt.plot(carrier0)
plt.title("Carrier f0")

plt.subplot(5,1,5)
plt.step(range(len(decoded)), decoded)
plt.title("Decoded Bits")

plt.tight_layout()
plt.show()

~~~

# Output Waveform
# ASK
<img width="1271" height="1011" alt="DC EXP 4" src="https://github.com/user-attachments/assets/3ebbb92d-5db0-4d17-ba7f-d467ae996aea" />

# FSK

<img width="1268" height="1008" alt="DC EXP 4 2" src="https://github.com/user-attachments/assets/f62cd952-0a77-4af9-9fc6-7339c9385e00" />



# Results
Thus, the ASK and FSK performed using colab.
