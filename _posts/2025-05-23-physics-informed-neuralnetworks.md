---
layout: post
title: "Physics-Informed Neural Networks (PINNs)"
date: 2025-04-04
categories: [projects]
author: Valentina Mazzotti
tags: [neural-networks, machine-learning]
---


Recently, I explored the concept of **Physics-Informed Neural Networks (PINNs)**, a framework that merges neural networks with differential equations. Unlike traditional machine learning models, PINNs do not require labeled training data. Instead, they rely entirely on the governing **physical laws**, encoded as a **loss function** derived from the underlying differential equation and its boundary and initial conditions.

The goal of a PINN is not to classify or regress from examples but to solve a partial differential equation (PDE) over a specified domain. During training, the network adjusts its weights to minimize the residual of the PDE as well as any violations of initial and boundary constraints.

---

## Solving the 1D Wave Equation

As a first experiment, I implemented a PINN to solve the 1D wave equation:

$$ 
\frac{\partial^2 u}{\partial t^2} = c^2 \frac{\partial^2 u}{\partial x^2}
$$ 

with initial condition $$u(x, 0) = \frac{1}{2} \sin(2\pi x)$$, and zero initial time derivative. The boundary conditions were Dirichlet (\( u(0, t) = u(1, t) = 0 \)).

I used a fully connected feedforward neural network with three hidden layers. Initially, I used **leaky ReLU (or “sneaky ReLU”)** as the activation function. However, I quickly discovered that it was **not well-suited for this task**: the resulting solution lacked the smoothness and periodic structure expected of a wave equation, and the network struggled to converge.

Switching to **Tanh** activations improved the performance significantly. The Tanh nonlinearity better captured the smooth, sinusoidal nature of the solution and allowed the network to approximate second derivatives more accurately.

---

## Why Use a PINN?

Even though this particular PDE has a known analytical solution, using a PINN here serves to demonstrate a few key advantages:

### 1. Generalizability to Non-Analytical Systems

Many physically relevant PDEs do not have closed-form solutions. In such cases, PINNs can approximate solutions while maintaining consistency with known physical laws.

### 2. Error Accumulation in Numerical Methods

Traditional finite difference or finite element methods integrate forward in time and accumulate discretization errors. By contrast, PINNs **learn the entire solution domain simultaneously**, minimizing a global loss function that reflects the PDE and boundary conditions throughout the domain. This can lead to more stable solutions, particularly over long time intervals.

### 3. Continuous Interpolation

Once trained, a PINN acts as a smooth function approximator. It can provide the solution at arbitrary points within the spatial and temporal domain without the need to interpolate between discrete mesh points, which is often a limitation in classical solvers.

---

## Next Steps

## Network Architecture

The neural network I used is a fully connected feedforward model with the following configuration:

- **Input layer:** 2 neurons (space and time)
- **Hidden layers:** 3 layers
  - Layer 1: 50 neurons, Tanh activation
  - Layer 2: 50 neurons, Tanh activation
  - Layer 3: 50 neurons, Tanh activation
- **Output layer:** 1 neuron (solution \( u(x, t) \))

```{python}


self.linear_tanh_stack = nn.Sequential(
    nn.Linear(2, 50),
    nn.Tanh(),
    nn.Linear(50, 50),
    nn.Tanh(),
    nn.Linear(50, 50),
    nn.Tanh(),
    nn.Linear(50, 1)
)
```

Initially, I tried using leaky ReLU (sometimes humorously referred to as "sneaky ReLU") as the activation function, but it produced poor results for this problem—likely due to the lack of smoothness and periodicity required for wave-like solutions.

Switching to Tanh improved the model's ability to approximate derivatives and match the true physical behavior of the wave equation.