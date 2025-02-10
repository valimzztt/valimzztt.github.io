---
layout: post
title:  "Split Operator Method"
date:   2024-12-25 20:44:51 +0100
categories: post
---
# Split Operator Method for Wavefunction Evolution

## Introduction
The **Split Operator Method** is a numerical technique used to solve the **time-dependent Schrödinger equation (TDSE)**:

\[
i \hbar \frac{\partial \Psi(x,t)}{\partial t} = \hat{H} \Psi(x,t)
\]

where the Hamiltonian \( \hat{H} \) consists of kinetic and potential energy terms:

\[
\hat{H} = \hat{T} + \hat{V} \, , \quad \text{where} \quad \hat{T} = \frac{-\hbar^2}{2m} \nabla^2, \quad \hat{V} = V(x)
\]

The **Split Operator Method** utilizes the **Lie-Trotter formula** to approximate the time evolution operator \( e^{-i \hat{H} \Delta t / \hbar} \) by splitting it into kinetic and potential contributions.

## Method
The evolution of the wavefunction over a small time step \( \Delta t \) is given by:

\[
\Psi(x, t + \Delta t) = e^{-i \hat{H} \Delta t / \hbar} \Psi(x, t)
\]

Using the **second-order Trotter approximation**:

\[
 e^{-i \hat{H} \Delta t / \hbar} \approx e^{-i \hat{V} \Delta t / 2\hbar} e^{-i \hat{T} \Delta t / \hbar} e^{-i \hat{V} \Delta t / 2\hbar}
\]

This means the evolution consists of three steps:

1. **Half-step potential evolution:**
   \[ \Psi'(x,t) = e^{-i \hat{V} \Delta t / 2 \hbar} \Psi(x,t) \]

2. **Full kinetic evolution (Fourier domain):**
   \[ \tilde{\Psi}(k,t) = \mathcal{F} \{ \Psi'(x,t) \} \]
   \[ \tilde{\Psi}'(k,t) = e^{-i \hat{T} \Delta t / \hbar} \tilde{\Psi}(k,t) \]
   \[ \Psi''(x,t) = \mathcal{F}^{-1} \{ \tilde{\Psi}'(k,t) \} \]

3. **Another half-step potential evolution:**
   \[ \Psi(x,t+\Delta t) = e^{-i \hat{V} \Delta t / 2 \hbar} \Psi''(x,t) \]

where \( \mathcal{F} \) and \( \mathcal{F}^{-1} \) are the Fourier Transform and its inverse.

## Numerical Implementation
### 1D Wavefunction Evolution (Python Code)

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.fft import fft, ifft, fftfreq

# Define parameters
hbar = 1.0  # Reduced Planck's constant
m = 1.0     # Mass of particle
N = 256     # Number of spatial points
L = 10.0    # Spatial domain size
dx = L / N  # Spatial step size
dt = 0.01   # Time step

# Define spatial and momentum grids
x = np.linspace(-L/2, L/2, N, endpoint=False)
k = fftfreq(N, d=dx) * 2 * np.pi

# Define potential (e.g., harmonic oscillator V = (1/2) * x^2)
V = 0.5 * x**2

# Initial wavefunction (Gaussian wave packet)
x0 = -2.0  # Initial position of the wave packet
sigma = 0.5  # Width of the wave packet
p0 = 2.0  # Initial momentum
psi = np.exp(-((x - x0) ** 2) / (2 * sigma**2)) * np.exp(1j * p0 * x / hbar)
psi /= np.linalg.norm(psi)  # Normalize

# Precompute evolution operators
expV = np.exp(-1j * V * dt / (2 * hbar))
expT = np.exp(-1j * (hbar**2 * k**2) / (2 * m) * dt / hbar)

# Time evolution
n_steps = 500  # Number of time steps
for _ in range(n_steps):
    psi *= expV  # Half-step potential
    psi_k = fft(psi)  # Fourier transform
    psi_k *= expT  # Kinetic evolution in k-space
    psi = ifft(psi_k)  # Inverse Fourier transform
    psi *= expV  # Half-step potential

# Plot final wavefunction
plt.plot(x, np.abs(psi)**2, label='Final |Ψ(x)|²')
plt.xlabel('x')
plt.ylabel('|Ψ(x)|²')
plt.legend()
plt.show()
```

## Advantages of the Split Operator Method
- **Efficiency:** Only requires fast Fourier transforms (FFT), making it computationally efficient.
- **Unitarity Preservation:** Ensures wavefunction normalization is maintained.
- **Simple Implementation:** Requires only basic matrix operations and FFTs.
- **Scalability:** Can be extended to higher dimensions and different potential landscapes.

## Applications
- Quantum dynamics simulations
- Optical wave propagation
- Bose-Einstein condensate studies
- Electronic structure calculations

## References
1. Feit, M. D., Fleck, J. A., & Steiger, A. (1982). Solution of the Schrödinger equation by a spectral method. *Journal of Computational Physics*, 47(3), 412-433.
2. Press, W. H., Teukolsky, S. A., Vetterling, W. T., & Flannery, B. P. (2007). *Numerical Recipes: The Art of Scientific Computing*. Cambridge University Press.

---

This guide provides an overview of the **Split Operator Method** and its numerical implementation. Let me know if you need modifications or further explanations!
