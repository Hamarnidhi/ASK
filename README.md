# ASK
# Aim
Write a simple Python program for the modulation and demodulation of ASK and FSK.
# Tools required
# Program
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, lfilter

def butter_lowpass_filter(data, cutoff, fs, order=5):
    nyquist = 0.5 * fs
    normal_cutoff = cutoff / nyquist
    b, a = butter(order, normal_cutoff, btype='low', analog=False)
    return lfilter(b, a, data)

fs = 1000
f_carrier = 50
bit_rate = 10
T = 1
t = np.linspace(0, T, int(fs * T), endpoint=False)

bits = np.random.randint(0, 2, bit_rate)
bit_duration = fs // bit_rate
message_signal = np.repeat(bits, bit_duration)
carrier = np.sin(2 * np.pi * f_carrier * t)
ask_signal = message_signal * carrier

demodulated = ask_signal * carrier
filtered_signal = butter_lowpass_filter(demodulated, f_carrier, fs)
decoded_bits = (filtered_signal[::bit_duration] > 0.25).astype(int)

plt.figure(figsize=(12, 8))
plt.subplot(4, 1, 1)
plt.plot(t, message_signal, color='b')
plt.title('Message Signal')
plt.grid(True)

plt.subplot(4, 1, 2)
plt.plot(t, carrier, color='g')
plt.title('Carrier Signal')
plt.grid(True)

plt.subplot(4, 1, 3)
plt.plot(t, ask_signal, color='r')
plt.title('ASK Modulated Signal')
plt.grid(True)

plt.subplot(4, 1, 4)
plt.step(np.arange(len(decoded_bits)), decoded_bits, color='r', marker='x')
plt.title('Decoded Bits')
plt.tight_layout()
plt.show()
```
```
# Output Waveform
```
<img width="1190" height="790" alt="download" src="https://github.com/user-attachments/assets/b0d119f6-863d-412f-bd01-d1ffdf38dbd7" />

# Results
```
Output Found and Waveform has been Generated
```
# Hardware experiment output waveform.
