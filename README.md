# ASK
# Aim
Write a simple Python program for the modulation and demodulation of ASK and FSK.
# Tools required
# Program:
# ASK:
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
# FSK:

```
import numpy as np
import matplotlib.pyplot as plt

# Message bits
bits = [0, 1, 0, 1, 0, 1, 0, 1, 0]
bit_duration = 0.1
fs = 1000
f1 = 50   # Frequency for bit 1
f0 = 10   # Frequency for bit 0

# Time axis
t_bit = np.arange(0, bit_duration, 1/fs)
t = np.arange(0, bit_duration * len(bits), 1/fs)

# Message signal
message = np.repeat(bits, len(t_bit))

# FSK Modulation
fsk_signal = []

for bit in bits:
    if bit == 1:
        carrier = np.sin(2 * np.pi * f1 * t_bit)
    else:
        carrier = np.sin(2 * np.pi * f0 * t_bit)
    fsk_signal.extend(carrier)

fsk_signal = np.array(fsk_signal)

# Demodulation (Zero-crossing method)
decoded_bits = []
samples_per_bit = len(t_bit)

for i in range(0, len(fsk_signal), samples_per_bit):
    segment = fsk_signal[i:i+samples_per_bit]
    zero_crossings = np.where(np.diff(np.sign(segment)))[0]
    
    if len(zero_crossings) > 15:
        decoded_bits.append(1)
    else:
        decoded_bits.append(0)

decoded_signal = np.repeat(decoded_bits, samples_per_bit)

# Plotting
plt.figure(figsize=(10, 8))

plt.subplot(4, 1, 1)
plt.plot(t, message)
plt.title("Message Signal")
plt.ylim(-0.2, 1.2)

plt.subplot(4, 1, 2)
plt.plot(t, fsk_signal)
plt.title("FSK Modulated Signal")

plt.subplot(4, 1, 3)
plt.plot(t, decoded_signal)
plt.title("Decoded Bits")
plt.ylim(-0.2, 1.2)

plt.subplot(4, 1, 4)
plt.plot(t[:len(t_bit)], np.sin(2*np.pi*f1*t_bit))
plt.title("Carrier Example (Bit 1 Frequency)")

plt.tight_layout()
plt.show()
```
# Output Waveform
# ASK:
<img width="989" height="790" alt="image" src="https://github.com/user-attachments/assets/56d228c9-5842-4b7a-a463-d38709273af6" />

# FSK:
<img width="989" height="790" alt="image" src="https://github.com/user-attachments/assets/5f011dff-430f-4493-84b0-fca0d91760a6" />

# Results:
Experiment has been concluded successfully.
# Hardware experiment output waveform.
