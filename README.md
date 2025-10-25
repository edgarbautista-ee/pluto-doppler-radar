# Doppler Radar with ADALM-PLUTO SDR

Measure motion via Doppler shift using the ADALM-PLUTO. This project logs I/Q data, detects frequency shifts around the transmit tone, and converts them into **radial velocity** estimates.

> Status: **Scaffold created** — wiring + capture script next, then plots and a short demo video.

---

## 🗺️ System Overview

- **TX:** Continuous wave near 2.4 GHz (or another license-free band)
- **Target:** Moving object (hand wave, fan, person walking)
- **RX:** Reflected signal mixed with LO ⇒ Doppler frequency \( f_d \)
- **Baseband processing:** FFT / peak picking ⇒ velocity

**Block Diagram**  
*(add an image `docs/block-diagram.png` later and link it here)*

---

## 🧠 Theory (TL;DR)

For a monostatic CW radar (same antenna/LO for TX/RX), the Doppler shift is:

<p align="center">

$$
f_d = \frac{2 v}{\lambda} = \frac{2 v f_c}{c}
$$

</p>


Solving for velocity:

<p align="center">
  
$$
v = \frac{f_d \* c}{2 f_c}
$$

</p>

Where \( v \) is radial velocity, \( lambda \) is wavelength, \( fc \) is carrier, and \( c \) is speed of light.

We estimate \( fd \) by locating the dominant tone in the baseband FFT around DC (positive/negative bins indicate approach/retreat).

---

## 🧩 Bill of Materials

- ADALM-PLUTO SDR
- 1–2 antennas (TX/RX; start with simple dipoles)
- Optional: directional antenna for RX to improve SNR
- Tripod or fixed mount
- Laptop with USB

---

## 🛠️ Software

- **Capture/Control:**  
  - Option A: **GNU Radio** flowgraph (`/gnuradio/pluto_doppler.grc`)  
  - Option B: **Python** with libiio (or `pyadi-iio`) (`/python/capture.py`)
- **Processing/Visualization:**  
  - **MATLAB** scripts (`/matlab/*.m`) or **Python** (`/python/process.py`)

> Pick one path first (GNU Radio or MATLAB/Python). I’ll start with MATLAB to get FFTs and spectrograms quickly.

---

## 🚀 Quick Start (placeholder – will update as code lands)

1. Install drivers & tools for PLUTO (Analog Devices).  
2. Clone this repo:
   ```bash
   git clone https://github.com/edgar-bautista/pluto-doppler-radar
   cd pluto-doppler-radar
