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
