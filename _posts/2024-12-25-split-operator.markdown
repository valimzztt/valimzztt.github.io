---
layout: post
title:  "Split Operator Method"
date:   2024-12-25 20:44:51 +0100
categories: post
---
# Split Operator Method for Wavefunction Evolution

## Introduction
Imagine you need to solve the Schroedinger Equation with a Hamiltonian that contains non linear terms. The **Split Operator Method** is a numerical technique used to solve the **time-dependent Schrödinger equation (TDSE)**:

$$
i \hbar \frac{\partial \Psi(x,t)}{\partial t} = \hat{H} \Psi(x,t)
$$

where the Hamiltonian $\hat{H}$ consists of kinetic and potential energy terms:

$$
\hat{H} = \hat{T} + \hat{V} \, , \quad \text{where} \quad \hat{T} = \frac{-\hbar^2}{2m} \nabla^2, \quad \hat{V} = V(x)
$$

The core of the Split Operator Method is that it uses the Lie-Trotter formula to approximate the time evolution operator 
The **Split Operator Method** utilizes the **Lie-Trotter formula** to approximate the time evolution operator $e^{-i \hat{H} \Delta t / \hbar}$ by splitting it into kinetic and potential contributions.

## Method
The evolution of the wavefunction over a small time step \( \Delta t \) is given by:

$$
\Psi(x, t + \Delta t) = e^{-i \hat{H} \Delta t / \hbar} \Psi(x, t)
$$ 

Using the **second-order Trotter approximation**:

\[
 e^{-i \hat{H} \Delta t / \hbar} \approx e^{-i \hat{V} \Delta t / 2\hbar} e^{-i \hat{T} \Delta t / \hbar} e^{-i \hat{V} \Delta t / 2\hbar}
\]

This means the evolution consists of three steps:

1. **Half-step potential evolution:**
   $$ \Psi'(x,t) = e^{-i \hat{V} \Delta t / 2 \hbar} \Psi(x,t) $$

2. **Full kinetic evolution (Fourier domain):**
   $$ \tilde{\Psi}(k,t) = \mathcal{F} \{ \Psi'(x,t) \} $$
   $$ \tilde{\Psi}'(k,t) = e^{-i \hat{T} \Delta t / \hbar} \tilde{\Psi}(k,t) $$
   $$ \Psi''(x,t) = \mathcal{F}^{-1} \{ \tilde{\Psi}'(k,t) \} $$

3. **Another half-step potential evolution:**
   \[ \Psi(x,t+\Delta t) = e^{-i \hat{V} \Delta t / 2 \hbar} \Psi''(x,t) \]

where \( \mathcal{F} \) and \( \mathcal{F}^{-1} \) are the Fourier Transform and its inverse.


I used the Split Operator Method when I was investigating 

## Advantages of the Split Operator Method
The main advantage of the SOM method is its efficiency, as it only requires the fast Fourier transform (FFT), as well as unitary preservation (it ensures that at each step the wavefunction is properly normalized) and its scalability, as it can be extended to different potential landscapes. 

If you are curious to know how it can be implemented, I have a GitHub repository that collects different simulations of wavefunctions for different potential landscapes. 

One problem I was interested was to study the evolution of a wavefunction that can be decoupled in the center of mass motion that obeys the free electron motion and the internal motion that instead is coupled to the center of mass via an harmonic potential. 
