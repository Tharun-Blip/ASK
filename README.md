# ASK
# Aim
Write a simple Python program for the modulation and demodulation of ASK and FSK.
# Tools required
# Program:
# ASL:
```
import numpy as np
import matplotlib.pyplot as plt

# Parameters
bit_stream = [1, 0, 1, 1, 0]
bit_duration = 1
fs = 1000
fc = 5

t = np.arange(0, bit_duration, 1/fs)
ask_signal = []

# ASK Modulation
for bit in bit_stream:
    if bit == 1:
        carrier = np.sin(2 * np.pi * fc * t)
    else:
        carrier = np.zeros(len(t))
    ask_signal.extend(carrier)

ask_signal = np.array(ask_signal)

# ASK Demodulation
demod_bits = []
for i in range(0, len(ask_signal), len(t)):
    segment = ask_signal[i:i+len(t)]
    if np.max(segment) > 0.5:
        demod_bits.append(1)
    else:
        demod_bits.append(0)

print("Original Bits:", bit_stream)
print("Demodulated Bits:", demod_bits)

plt.plot(ask_signal)
plt.title("ASK Modulated Signal")
plt.show()
```
```
Attach the program
```
# Output Waveform
```
Attach the output waveform
```
# Results
```
Attach the output waveform
```
# Hardware experiment output waveform.
