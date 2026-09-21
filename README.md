# Spontaneous Synchronization: Kuramoto Model

An optimised Python simulation of the Kuramoto Model that visualises the non-linear dynamics of large populations of interacting entities, such as metronomes, flashing fireflies, or oscillating power grids. By implementing Mean-Field Approximation, this project bypasses computational bottlenecks of all-to-all interaction models, successfully demonstrating the large shift from uncontrolled chaos to spontaneous synchronization.

## Architecture

* **Compute Engine:** Python 3 and `scipy.integrate.solve_ivp`. Utilizes the RK45 (Runge-Kutta 4(5)) method to solve non-linear ordinary differential equations over continuous time scales.
* **Vectorization Layer:** `numpy`. Handles complex number transformations and matrix operations to process population-wide phase derivatives without slow, iterative Python loops.
* **Visualization Layer:** `matplotlib.pyplot`. Generates high-quality data visualizations comparing simulated steady-state order parameters against theoretical critical thresholds.

## Key Methodologies

* **The Mean-Field Approximation:** In a system of 1,200 oscillators, computing individual pull dynamics requires over 1.4 million operations per time step. This algorithm calculates a single global complex order parameter, extracting its magnitude and average phase. Oscillators update trajectories based solely on this global mean field, transforming complexity from O(N²) to O(N) and enabling real-time simulation.
* **Forward Continuation:** The final, settled integration state of a previous coupling strength is roped in as the initial state of the next. This reduces the integration time required for the system to reach equilibrium across 120 different coupling strengths.
* **Isolating the Macroscopic Steady State:** To ensure the phase transition curve strictly reflects stable configurations, the extraction logic discards the first 75% of simulated time steps (the chaotic transient window). The complex order parameter is averaged over the final 25% of the data array.
* **Theoretical Calibration:** The critical coupling strength required for synchronization is defined by the natural frequency distribution. By tightly coupling these assumptions with NumPy random seed generation, the simulated order parameter climbs exactly as the coupling strength crosses the mathematically predicted threshold.

<img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/cf566399-a29d-4a9c-8844-ad08a87056be" />


## Prerequisites

The script relies on external scientific computing and data visualization libraries.
* Python 3.10
* `numpy`
* `scipy`
* `matplotlib`

## Usage Instructions

1. Install the required dependencies:
   ```bash
   pip install numpy scipy matplotlib
