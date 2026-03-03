# CMOS Differential Amplifier – 180nm (LTspice)

## 📌 Project Overview

This project presents the design and simulation of a CMOS differential amplifier using generic 180nm MOS models in LTspice.

The circuit consists of:
- NMOS differential input pair
- PMOS current mirror active load
- NMOS tail current source
- 10pF load capacitor
- 1.8V supply voltage

AC and Transient analyses were performed to evaluate gain and frequency response.

---

## ⚙️ Technology & Device Models

### NMOS Model
.model NMOS180 NMOS (LEVEL=1 VTO=0.5 KP=200u LAMBDA=0.02 TOX=4n)

### PMOS Model
.model PMOS180 PMOS (LEVEL=1 VTO=-0.5 KP=80u LAMBDA=0.02 TOX=4n)

---

## 🔋 Circuit Parameters

| Parameter | Value |
|-----------|-------|
| VDD | 1.8 V |
| Tail Current (I_tail) | 50 µA |
| Current per branch | 25 µA |
| Load Capacitor | 10 pF |
| Input amplitude | 4 mV |
| Input frequency | 1 kHz |
| AC sweep | .ac dec 100 10 20Meg |
| Transient | .tran 10m |

---

## 🧮 DC Bias Calculations

Tail current:
I_tail = 50 µA

Current splits equally:
I_D1 = I_D2 = I_tail / 2  
I_D = 25 µA

---

## 📐 MOS Saturation Condition

For saturation:

V_DS ≥ V_OV

Where:

V_OV = V_GS - V_TH

---

## 📘 Small-Signal Parameters

### 1️⃣ Transconductance (gm)

For MOS in saturation:

gm = 2I_D / V_OV

Assume:
V_OV ≈ 0.2 V

Therefore:

gm = (2 × 25µA) / 0.2  
gm = 250 µS

---

### 2️⃣ Output Resistance (ro)

ro = 1 / (λ I_D)

Given:
λ = 0.02  
I_D = 25µA

ro = 1 / (0.02 × 25µA)  
ro = 2 MΩ

---

## 📈 Voltage Gain Calculation

For differential amplifier with active load:

A_v ≈ gm × (ro_n || ro_p)

Assuming ro_n ≈ ro_p ≈ 2 MΩ

Parallel combination:

R_out = (2M || 2M) = 1 MΩ

Thus:

A_v = 250µS × 1MΩ  
A_v ≈ 250 V/V

In dB:

Gain_dB = 20 log10(250)

Gain_dB ≈ 48 dB

✔ Matches AC plot (~48–54 dB)

---

## 📊 Frequency Response

Dominant pole:

f_p = 1 / (2π R_out C_L)

Where:
R_out ≈ 1MΩ  
C_L = 10pF

f_p = 1 / (2π × 1M × 10pF)

f_p ≈ 15.9 kHz

This corresponds to the -3dB drop observed in AC plot.

---

## 🔄 AC Analysis Results

Command used:
.ac dec 100 10 20000000

Observed:
- DC Gain ≈ 48–54 dB
- Gain rolls off at ~10–20 kHz
- Single dominant pole response
- Phase approaches -90° at high frequency

---

## 🌊 Transient Analysis

Command used:
.tran 10m

Input:
Vin+ = SINE(0.9 4m 1k)
Vin− = SINE(0.9 4m 1k 0 0 180)

Observed:
- Output swings between ~0.65V and ~1.7V
- Large-signal operation
- Output saturates due to current steering
- Square-like waveform due to full differential switching

Explanation:

When |Vdiff| > V_OV,
the differential pair fully steers tail current,
causing capacitor to charge/discharge rapidly.

---

## 🧠 Large-Signal Behavior

Capacitor charging equation:

I = C (dV/dt)

Therefore:

dV/dt = I / C

Given:
I ≈ 50µA  
C = 10pF

Slope:

dV/dt = 50µA / 10pF  
dV/dt = 5 V/ms

This explains steep transitions in transient waveform.

---

## 🎯 Key Performance Metrics

| Parameter | Value |
|-----------|-------|
| DC Gain | ~48–54 dB |
| Tail Current | 50 µA |
| Output Resistance | ~1 MΩ |
| Load Capacitance | 10 pF |
| Supply Voltage | 1.8 V |

---

## 📌 Conclusion

A CMOS differential amplifier was successfully designed and analyzed using 180nm generic models.

The amplifier achieved:

- ~50 dB voltage gain
- Single dominant pole behavior
- Stable frequency response
- Correct large-signal switching behavior

This project demonstrates:

- Analog bias design
- Small-signal modeling
- Gain calculation
- Frequency response analysis
- Transient large-signal understanding
