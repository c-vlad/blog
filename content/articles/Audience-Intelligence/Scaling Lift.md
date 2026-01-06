---
title: 'Scaling Lift'
categories: ['audience intelligence']
tags: ['essai']
weight: 2
---

# Estimating Overlap in Scaled Audiences: A Principled Approach Using I-Projection

## Introduction

In Audience Intelligence, we often rely on observed data from a panel-collected via social media platforms, user devices, surveys, or third-party measurement providers-to understand behaviors and affinities across different audience segments. 

Suppose we observe:

- **A**: An audience segment of interest (e.g. people who follow a brand or visited a website)
- **B**: A second audience (e.g. people who engaged with a product, followed an influencer, or purchased a category)
- **I**: The observed overlap between A and B in the panel

From other data sources (e.g. CRM systems, census data, digital reach estimates), we might know:

- **A′**: The estimated true size of audience A in the full population
- **B′**: The estimated true size of audience B in the full population

We then wish to estimate:

- **I′**: The *expected intersection* between A′ and B′ in the full population, consistent with the original observed relationship between A and B.

This extrapolation is not straightforward: naive methods (like linear scaling or assuming independence) can produce invalid results (e.g. \(I′ > \min(A′, B′)\)) or ignore the statistical dependencies in the observed data.

We propose a **principled**, **smooth**, and **closed-form** solution based on **information theory**-specifically, the **I-projection** or **minimum-KL divergence projection**.


## Problem Definition

Let:

- \( P \): Total population size
- \( A \), \( B \), \( I \): Observed sizes in a panel  
- \( A′ \), \( B′ \): Target (known or estimated) population sizes
- \( I′ \): Unknown intersection to estimate

We assume that the joint distribution of the binary variables "in A" and "in B" is preserved in a certain statistical sense when we move from the panel to the full population.


## Method: KL-Minimizing I-Projection

The I-projection seeks the **distribution closest (in KL divergence)** to the original panel joint distribution that matches the new marginals \( A′ \), \( B′ \).

For 2 binary variables, this projection has a unique and interpretable property:

> **It preserves the original odds ratio**, while adjusting the marginals.

### Step 1: Compute the observed odds ratio

\[
\theta = \frac{I \cdot (P - A - B + I)}{(A - I)(B - I)}
\]

### Step 2: Solve for the new intersection \( I′ \)

Let \( N′ = P - A′ - B′ + I′ \). We want:

\[
\frac{I′ \cdot N′}{(A′ - I′)(B′ - I′)} = \theta
\]

This yields a quadratic equation in \( I′ \):

\[
(1 - \theta) I′^2 + [P - A′ - B′ + \theta(A′ + B′)] I′ - \theta A′ B′ = 0
\]

### Step 3: Choose the valid root

Define:

\[
a = 1 - \theta, \quad b = P - A′ - B′ + \theta(A′ + B′), \quad c = -\theta A′ B′
\]

Then:

\[
I′ = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
\]

Pick the root within the valid bounds:

\[
\max(0, A′ + B′ - P) \le I′ \le \min(A′, B′)
\]


## Why This Works

This method:

- Guarantees a valid estimate \( I′ \) within known logical bounds
- Is **nonlinear** but **smooth**, avoiding sharp jumps
- **Preserves statistical dependence** (via the odds ratio)
- Has a **closed-form solution** via a single quadratic

This approach is equivalent to finding the **maximum entropy** estimate under fixed marginals and interaction, or solving for the **I-projection** in a log-linear model with fixed marginals.


## Example

Suppose:

- \( P = 1,000,000 \)
- \( A = 10,000 \), \( B = 20,000 \), \( I = 2,000 \)
- \( A′ = 50,000 \), \( B′ = 80,000 \)

Then:

1. Compute the odds ratio:

\[
\theta = \frac{2,000 \cdot (1,000,000 - 10,000 - 20,000 + 2,000)}{(10,000 - 2,000)(20,000 - 2,000)} = \cdots
\]

2. Plug into the quadratic to find \( I′ \)


## Applications

- Estimating affinities in large audiences (e.g. affinity between brand audiences and interest groups)
- Adjusting panel-based co-occurrence data to population-scale insights
- Media planning and reach overlap estimation
- Lookalike modeling or campaign targeting evaluation


## Conclusion

By modeling audience intersection scaling as an **I-projection**, we achieve a principled, mathematically sound, and interpretable method for estimating audience overlaps. This approach respects observed statistical structure while adjusting for new population marginals, critical for accurate, large-scale Audience Intelligence.

