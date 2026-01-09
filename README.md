# Generative Models

Refer to the notes in this repository.

This repository contains structured notes on **generative models**, focusing on approaches based on **stochastic differential equations (SDEs)** and **ordinary differential equations (ODEs)**. The notes closely follow the structure of the original document and preserve its subsection hierarchy, while presenting the material in a concise, repository-friendly format.

The emphasis is on **conceptual understanding and modeling intuition**, rather than detailed derivations or implementations.

---

## Table of Contents

- Introduction  
- Stochastic Calculus  
  - Discrete Random Walk  
  - Brownian Motion  
  - Stochastic Differential Equations  
  - Ito’s Lemma  
  - Fokker–Planck Equation  
  - Random Walk as a Markov Process  
  - Forward Kolmogorov Equation  
  - Backward Kolmogorov Equation  
  - Reversing the Diffusion Process  
- Diffusion Models  
- Score Matching  
- Poisson Flow Generative Models  
- Continuous Flow Models  
- Citation  

---

## Introduction

We study two broad (non-exhaustive) classes of generative models:

- Models based on **stochastic differential equations (SDEs)**  
- Models based on **ordinary differential equations (ODEs)**  

Both approaches describe how probability distributions evolve over time and provide principled ways to generate samples from complex data distributions.

---

## Stochastic Calculus

This section builds the mathematical intuition required for diffusion-based generative models by starting from simple stochastic processes and progressively moving toward continuous-time descriptions.

### Discrete Random Walk

A discrete random walk models a particle that moves randomly at each time step. Key observations include:

- The expected position remains zero
- The variance grows linearly with the number of steps
- Differences over time intervals depend only on the interval length

These properties motivate a continuous-time limit.

---

### Brownian Motion

Brownian motion is the continuous limit of a discrete random walk. Its defining properties are:

- Gaussian-distributed increments
- Zero mean displacement over infinitesimal time intervals
- Variance proportional to elapsed time

Brownian motion serves as the canonical noise process in continuous-time stochastic models.

---

### Stochastic Differential Equations

Stochastic differential equations combine:

- A **drift term**, representing deterministic evolution
- A **diffusion term**, representing stochastic noise

SDEs describe how systems evolve under uncertainty and form the foundation of diffusion-based generative modeling.

---

### Ito’s Lemma

Ito’s Lemma is the stochastic analogue of the chain rule. It explains how functions of stochastic processes evolve over time.

A key insight is that second-order terms in the stochastic increment contribute at first order in time, a phenomenon unique to stochastic calculus.

---

### Fokker–Planck Equation

Rather than tracking individual stochastic trajectories, one can study how **probability densities** evolve.

The Fokker–Planck equation governs the time evolution of the probability density associated with an SDE and provides a bridge between microscopic dynamics and macroscopic distributions.

---

### Random Walk as a Markov Process

Both discrete random walks and Brownian motion are examples of **Markov processes**, where the future state depends only on the present state.

Transition probabilities fully characterize the dynamics, and composition rules allow probabilities to be propagated across time intervals.

---

### Forward Kolmogorov Equation

The forward Kolmogorov equation (another name for the Fokker–Planck equation) describes how transition probabilities evolve forward in time.

It can be derived directly from the Markov property by expanding transition probabilities over infinitesimal time intervals.

---

### Backward Kolmogorov Equation

The backward Kolmogorov equation describes how transition probabilities evolve backward in time with respect to the initial condition.

This equation plays a crucial role in analyzing reverse-time dynamics and conditioning on future states.

---

### Reversing the Diffusion Process

Diffusion processes gradually destroy information by injecting noise. However, if the probability density at each time is known, a **reverse-time process** can be defined.

The reverse dynamics depend on the gradient of the log-probability density, often called the **score function**. This idea underpins modern diffusion-based generative models.

---

## Diffusion Models

Diffusion models generate data using two complementary processes:

1. **Forward process**: data is progressively corrupted by noise until it becomes pure noise  
2. **Reverse process**: noise is gradually removed to recover structured samples  

The forward process is fixed, while the reverse process is learned using neural networks.

---

## Score Matching

Score matching provides a way to learn the gradient of the log-density without explicitly modeling the density itself.

Key advantages:

- Avoids computing normalization constants
- Learning the score uniquely determines the distribution

Training involves sampling data, adding noise at random times, and fitting a neural network to predict the score of the noisy data.

---

## Poisson Flow Generative Models

Poisson Flow Generative Models (PFGM) are **ODE-based** generative models inspired by electrostatics.

Core ideas:

- Data points act as electric charges
- The induced electric field defines a flow
- Samples are generated by following this flow backward

### Avoiding Mode Collapse

Naive backward flow leads to collapse of samples. PFGM addresses this by:

- Introducing an additional dimension
- Starting samples from a high-dimensional surface
- Flowing deterministically back to the data manifold

This guarantees coverage of the full data distribution.

---

## Continuous Flow Models

Continuous flow models learn a **deterministic vector field** that transforms a simple base distribution (such as a Gaussian) into the data distribution.

Key characteristics:

- Deterministic dynamics
- Exact likelihood computation
- Continuous-time transformations using ODEs

A neural network parameterizes the flow, and both data and probability density evolve jointly over time.

---

## Citation

If you use this work, please cite:

```bibtex
@article{nagaraj2023genmodels,
  title={Generative Models},
  author={Nagaraj, Balakrishnan},
  year={2023}
}
