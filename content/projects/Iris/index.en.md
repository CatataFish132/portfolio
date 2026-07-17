+++
title = "Shapley Value-Driven Optimization of Gabor Filters for Iris Recognition"
description = ""
weight = 1
date = 2025-10-08

[extra]
local_image = "/projects/Iris/0.webp"
tags = ["opencv", "python", "biometric", "iris", "numpy", "Shapley Value"]
github = "https://github.com/CatataFish132/iris_recognition"
mathjax = true
+++
![Iris](0.webp)

You can read the full paper here: [Download PDF (Iris.pdf)](Iris.pdf)
# Introduction
Developed an advanced biometric iris recognition system that uses cooperative game theory to optimize John Daugman’s traditional feature extraction pipeline. By applying Shapley value-based feature importance, the system mathematically evaluates the individual contribution of 2D Gabor filters to eliminate redundancy. This data-driven approach yields a highly compressed, computationally efficient, and state-of-the-art filter set that achieves an Equal Error Rate (EER) as low as **0.05%**.
# Project Details
- **Core Tech:** Python, OpenCV, NumPy, Shapley Value Optimization, USIT SDK.
- **Algorithms Used:** 2D Complex Gabor Filters, Hamming Distance with Binary Masking.
- **Target Datasets:** CASIA-IrisV1, IrisV3, and MMU.
- **My Role:** Solo Researcher & Computer Vision Engineer.
# The Challenge
- **Proprietary & Lack of Transparency:** John Daugman’s classic iris code remains the industry benchmark, but the specific optimal configuration of Gabor filters used in modern commercial systems is proprietary and unpublished.
- **Combinatorial Search Space:** Manually finding the optimal parameters (envelope size, wave orientation, wavelength, and strides) across different Gabor filter combinations creates an exponentially complex search space.
- **Extreme Alignment Sensitivity:** Minor rotational misalignments or vertical offsets (introduced during imperfect eye segmentation) cause dramatic, false mismatches.
# Key Features & Actions
- **Easy to use Library:** Packaged the entire pipeline into an intuitive, clean, and easy to understand Python library, allowing other students to run end-to-end iris encoding and matching with just a few lines of code.
- **Cooperative Game Theory Integration:** Modeled Gabor filters as "players" in a cooperative game, calculating their marginal contribution (Shapley values) to systematically keep high-impact filters and prune redundant ones.
- **Robust Rotational Alignment:** Developed a dynamic pixel-shifting correction system on the normalized iris band to simulate and find the optimal matching rotation angle.
# Results

![results](7.png)

- **State-of-the-Art Accuracy:** Achieved an outstanding Equal Error Rate (EER) of **0.05%** on the CASIA-IrisV1 dataset, outperforming the benchmark Kong et al. IrisCode implementation.
- **Outperformed Deep Learning Methods:** Reached an EER of **0.67%** on the IrisV3 dataset, surpassing the benchmark Deep CNN approach (0.76% EER) and all standard algorithms in the USIT SDK.