# Dynamic RLC Step Response Modeler

## Project Overview
This repository contains analytical verification scripts and hardware bench data validating the step-response transients of a second-order underdamped series RLC circuit. The physical model isolates non-ideal system parameters (internal source impedance and inductor wire resistance) to target an ideal resonant frequency ($\omega_o$) of $10^4\pi$ rad/s.

## Tech Stack & Instrumentation
* **Software:** MATLAB (Signal processing & numerical verification math)
* **Hardware Bench:** Rohde & Schwarz RTB2004 Digital Oscilloscope, Decade Substitution Boxes, Digital Multimeter (DMM)

## Core Engineering Tasks
* Derived foundational mathematical models for underdamped second-order differential equations.
* Accounted for circuit non-idealities by characterizing internal generator resistance and inductor coil parameters.
* Captured physical transient outputs across six unique damping ratios ($\zeta = 0.1$ to $1.0$).
* Verified that experimental transient local extrema sat within a strict $15\%$ convergence window of mathematical models.

## Methodology & Mathematical Derivation

### 1. Second-Order Governing Equation
Applying Kirchhoff's Voltage Law (KVL) to the series RLC branch with a unit step input $u(t)$ yields:

$$v_L(t) + v_R(t) + v_C(t) = u(t)$$

Substituting constituent relations ($i = C\frac{dv_C}{dt}$):

$$LC\frac{d^2v_C}{dt^2} + RC\frac{dv_C}{dt} + v_C(t) = u(t)$$

Dividing through by $LC$ forms the standard second-order linear differential voltage relation:

$$\frac{d^2v_C}{dt^2} + 2\alpha\frac{dv_C}{dt} + \omega_o^2v_C(t) = \omega_o^2u(t)$$

Where the damping factor $\alpha = \frac{R}{2L}$ and natural frequency $\omega_o = \frac{1}{\sqrt{LC}}$.

### 2. Underdamped Transient Analysis
For the initially quiescent underdamped configuration ($\alpha < \omega_o$), solving the characteristic equation yields complex conjugate roots $s = -\alpha \pm j\omega_d$. The final closed-form capacitor voltage profile is derived as:

$$v_C(t) = 1 + Ke^{-\alpha t}\cos(\omega_d t + \phi)$$

### 3. Local Extrema & Peak Bounds
Differentiating $v_C(t)$ with respect to time and solving for zero locates the signal maximums and minimums:

$$\frac{dv_C}{dt} = 0 \implies \tan(\omega_d t + \phi) = -\frac{\alpha}{\omega_d} \implies \omega_d t = k\pi$$

Thus, peaks map periodically at discrete time bounds:

$$t = \frac{k\pi}{\omega_d} \quad \text{for } k = 0, 1, 2, \dots$$

## Experimental Results & Hardware Verification

### 1. Transient Peak Data Table
The table below contrasts the measured peak voltages captured on the digital storage oscilloscope against the derived theoretical values across the variable damping factors ($\zeta$):

| Damping ($\zeta$) | 1st Max (Measured) | 1st Max (Theory) | 1st Min (Measured) | 1st Min (Theory) | 2nd Max (Measured) | 2nd Max (Theory) |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **0.1** | 2000 mV | 1.729 V | 400 mV | 0.468 V | 1275 mV | 1.342 V |
| **0.2** | 1750 mV | 1.527 V | 700 mV | 0.722 V | 1100 mV | 1.144 V |
| **0.4** | 1350 mV | 1.254 V | 920 mV | 0.935 V | 1000 mV | 1.021 V |
| **0.6** | 1100 mV | 1.045 V | 980 mV | 0.991 V | 990 mV | 1.001 V |
| **0.8** | 1000 mV | 1.015 V | 985 mV | 0.999 V | 992 mV | 1.000 V |

### 2. Oscilloscope Waveform Capture
Below is the transient step response captured on the Rohde & Schwarz RTB2004 during circuit validation:

![Oscilloscope Waveform](Oscilloscope%20Results.png)



