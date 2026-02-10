# Advance_Mathematics_Assignment

Learning Probability Density Functions Using Data Only
GAN-Based Non-Parametric Density Estimation
1. Overview

This project demonstrates a purely data-driven approach to learning an unknown probability density function (PDF) using Generative Adversarial Networks (GANs).
No analytical or parametric assumptions are made about the underlying distribution. Instead, the PDF is learned implicitly from data samples through adversarial training.

The study uses NO₂ (Nitrogen Dioxide) concentration data from Indian cities and applies a roll-number-dependent non-linear transformation before training a GAN to model the resulting distribution.

2. Methodology Pipeline

The complete workflow followed in this assignment is:

Data Collection → Data Pre-processing → Non-Linear Transformation → GAN Training → Sample Generation → PDF Approximation → Result Analysis

Each stage contributes to learning the target probability distribution solely from observed samples.

3. Dataset Information

Dataset Name: India Air Quality Dataset

Source: Kaggle

Dataset Link: https://www.kaggle.com/datasets/shrutibhargava94/india-air-quality-data

Selected Feature: NO₂ (Nitrogen Dioxide) concentration

Description:
The dataset contains air quality measurements collected from multiple cities across India. The NO₂ feature is chosen as the random variable for learning the probability density function using adversarial learning.

4. Objective

The primary objective of this assignment is to:

Learn an unknown probability density function directly from data samples

Avoid assuming any parametric or analytical form of the distribution

Use a Generative Adversarial Network to implicitly model the data distribution

Approximate the learned distribution through Kernel Density Estimation (KDE) on generated samples

5. Mathematical Formulation
Non-Linear Transformation

