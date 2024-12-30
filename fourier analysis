# Date Written: August 21st, 2023
# The purpose of this code is to compute discrete fourier series given data points

# Importing libraries
import matplotlib.pyplot as plt
import numpy as np
import math
from math import sin
from math import cos
from numpy import arctan
from scipy.io.wavfile import write

# Initializing all the variables
samples = [0.00, 0.10, 0.30, 0.50, 0.60, 0.50, 0.35, 0.16, 0.15, 0.22, 0.25, \
0.25, 0.20, 0.11, -0.01, -0.12, -0.22, -0.20, -0.15, -0.20, -0.30, \
-0.45, -0.40, -0.26, -0.10, 0.02, 0.13, 0.15, 0.11, 0.08, 0.10, \
0.13, 0.12, 0.02, -0.07, -0.14, -0.18, -0.13, -0.09, -0.17, -0.27, \
-0.47, -0.45, -0.14, -0.08, -0.07, -0.09, -0.10, -0.10, -0.05]

point = 0
sample_rate = 261
duration = 5
magnitudes = []
phase_shifts = []

while point < 50:
    plt.scatter(point / (50 * 261), samples[point], color = "black")
    point += 1
plt.xlim(0, 0.004)
plt.ylim(-0.75, 0.75)
plt.grid()
plt.show()
k = 0
n = 0
N = 50

# "a" represents sum of real number values
a = 0
# "b" represents sum of imaginary number values
b = 0
# "m" represents magnitude of sample size
m = 0
# "deg" represents phase shift of the sample
deg = 0

# Computing/calculating all values
while k <= (N - 1):
    while n <= (N - 1):
        a += (samples[n] * cos(-2 * 3.1415 * k * n/50))
        b += (samples[n] * sin(-2 * 3.1415 * k * n/50))
        n += 1

    # Calculating phase shift values
    if a != 0:
        deg = arctan(b/a)
    else:
        deg = 0
    m = math.sqrt(a**2 + b**2)
    a = round(a, 3)
    b = round(b, 3)
    m = round(m, 3)
    deg = round(deg, 3)
    magnitudes.append(m)
    phase_shifts.append(deg)
    print("Index: " + str(k) + ", Real: " + str(a) + \
          ", Imaginary: " + str(b) + ", Magnitude: " + str(m) + \
          ", Phase shift: " + str(deg))
    print(format(a, ".2f") + " + " + format(b, ".2f") + "i" + "\n")
    n = 0
    a = 0
    n = 0
    m = 0
    deg = 0
    k += 1

print("Magnitudes: " + str(magnitudes) + "\n")
print("Phase Shifts: " + str(phase_shifts) + "\n")

# Graphing initial amplitude vs frequency graph
i = 0
while i <= len(magnitudes) - 1:
    plt.scatter(i * 261, magnitudes[i], color = "black")
    i += 1
plt.xlim(0, 13000)
plt.ylim(0, 5)
plt.grid()
plt.show()
sample_rate = 44100
duration = 5

def generate_cosine_wave(freq, sample_rate, duration, shift):
    x = np.linspace(0, duration, sample_rate * duration, endpoint = False)
    frequencies = x * freq
    print(frequencies)
    y = np.cos(frequencies * (2 * np.pi) + shift)
    return x, y

phase_shifts = [-0.0, -0.81, -1.382, -1.401, -1.544, 0.164, 0.703, 0.075, \
                -0.079, 1.197, 1.507, 1.111, 0.364, -1.069, -1.024, 0.412, \
                1.03, 1.48, 0.454, 0.953, -0.711, 0.3, 1.512, 1.149, -0.65, \
                -0.0, 0.656, -1.144, -1.508, -0.26, 0.72, -0.948, -0.448, \
                -1.473, -1.023, -0.405, 1.035, 1.077, -0.358, -1.108, -1.502, \
                -1.191, 0.088, -0.072, -0.7, -0.161, 1.545, 1.411, 1.385, 0.812]

single_side_magnitudes = [0.018, 0.15, 0.256, 0.039, 0.057, 0.051, 0.074, \
                          0.082, 0.039, 0.028, 0.037, 0.006, 0.017, 0.009, \
                          0.005, 0.009, 0.009, 0.009, 0.009, 0.008, 0.005, \
                          0.001, 0.008, 0.004, 0.004]

_, sound = generate_cosine_wave(0, sample_rate, duration, phase_shifts[0])
_, add_sound = generate_cosine_wave(0, sample_rate, duration, phase_shifts[0])
sound = sound * single_side_magnitudes[0]
i = 1
while i < 10: #len(single_side_magnitudes) - 1:
    _, add_sound = generate_cosine_wave(261 * i, sample_rate, duration, phase_shifts[i])
    add_sound = add_sound * single_side_magnitudes[i]
    sound += add_sound
    i += 1

print(len(single_side_magnitudes))

plt.plot(sound)
plt.axhline(y=0, color = "black", linestyle = '-')
plt.title("Figure 10: Final soundwave")
plt.xlabel("Time (sec, x50000)")
plt.ylabel("Volume (dB)")
plt.xlim(0, 250)
plt.ylim(-0.6, 0.6)
plt.show()
tone = np.int16((sound / sound.max()) * 32767)
plt.plot(tone[:1000])
plt.show()
write("soundwave.wav", sample_rate, tone)