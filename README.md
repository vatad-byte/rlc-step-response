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

Substituting constituent relations ($i = C \frac{dv_C}{dt}$):
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

## Experimental Data & Validation Metrics
System calibrations isolated non-ideal physical parameters to reconcile the hardware setup with mathematical constraints. The internal function generator source impedance ($R_{in}$) and inductor wire internal winding resistance ($R_L$) were quantified using a digital multimeter (DMM) and a matching voltage divider framework:
$$R_{total} = R_{DecadeBox} + R_{in} + R_L$$

* Experimental values compiled across varying damping coefficients converged with the derived theoretical models within a **$15\%$ maximum variance tolerance window**.
