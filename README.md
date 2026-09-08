# Image-Based Lighting (IBL) in Ada 2023

## Project Overview
Image-Based Lighting (IBL) is an advanced rendering technique where omnidirectional photographic or synthetic environment maps serve as surrounding light sources for virtual 3D objects. This package provides an Ada 2023 (ISO/IEC 8652:2023) implementation of the standard lighting algorithms detailed in optical rendering literature and the Wikipedia article on Image-Based Lighting. The package implements mirror specular reflection, diffuse cosine-weighted hemisphere convolution, real-time irradiance estimation via 9-coefficient order-2 Spherical Harmonics (Ramamoorthi-Hanrahan model), and the modern split-sum Cook-Torrance/GGX approximation used in physically based rendering (PBR) pipelines.

## Features
- Strongly Typed Geometric and Color Primitives: Dedicated types for vectors, spherical coordinates, equirectangular matrices, and linear RGB photometric radiances.
- Contract-Based Subprogram Signatures: Rigorous Pre and Post contract aspects ensuring unit vector invariants, positive angular intervals, and valid array dimensions.
- Variant 1 — Mirror Reflection Mapping: Evaluates reflected view rays R = V - 2(V.N)N on latitude-longitude environment maps.
- Variant 2 — Diffuse Hemisphere Convolution: Numerically integrates cosine-weighted hemispherical irradiance E(N) = Integral (L(w) max(N.w, 0) dw).
- Variant 3 — Spherical Harmonics (Order 2, 9 Coefficients): Fast projection of 360-degree environment radiance into orthogonal SH basis functions, coupled with the closed-form analytic convolution formula for diffuse ambient light.
- Variant 4 — Split-Sum PBR Specular Approximation:
  - Importance-sampled GGX pre-filtered environment mapping using low-discrepancy 2D Hammersley sequences.
  - Precomputed 2D Bidirectional Reflectance Distribution Function (BRDF) integration Look-Up Table (LUT).
  - Integration of Fresnel-Schlick terms with scale-bias factors and pre-filtered color.
- Robust Error Handling: Explicit domain validation preventing division by zero on degenerate vectors and handling boundary constraints gracefully.

## Usage
The standalone test executable doubles as both an automated regression suite and an API usage demonstration.

```bash
# Build test suite
make

# Run tests
make test

# Clean artifacts
make clean
