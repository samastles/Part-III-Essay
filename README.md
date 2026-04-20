# Part-III-Essay

This repository contains the code and experiments for my Part III essay on score-based generative models. The notebooks explore various aspects of score matching objectives, including their computational efficiency and performance in different data-density regions, as well as an analysis of noise schedules for diffusion models.

## Repository Contents

*   `Experiment for Computation Time.ipynb`: Benchmarks the computational cost of different score matching objectives against varying data dimensions.
*   `Experiment for Low Data Density Regions.ipynb`: Visually compares the performance of score matching methods in capturing the score function of a 2D Mixture-of-Gaussians distribution.
*   `Schedules.ipynb`: Analyses and visualises different noise schedules for diffusion models and demonstrates the forward noising process on an image.

## Notebook Summaries

### Experiment: Computation Time
**File:** `Experiment for Computation Time.ipynb`

This notebook compares the wall-clock time per training step for four different score matching objectives:
- **Classical Score Matching**: Requires computing the full Jacobian trace, leading to O(d) complexity.
- **Denoising Score Matching (DSM)**: A scalable alternative that avoids trace computation.
- **Sliced Score Matching (SSM-VR)**: Uses random projections to estimate the trace.
- **Finite Difference Score Matching (FDSM)**: An alternative scalable method using directional derivatives.

The experiment measures performance across data dimensions ranging from 10 to 500. The generated plot shows that the computation time for Classical Score Matching increases linearly with dimension, making it impractical for high-dimensional data. In contrast, DSM, SSM-VR, and FDSM exhibit nearly constant and significantly lower computation times, highlighting their scalability.

### Experiment: Low Data Density Regions
**File:** `Experiment for Low Data Density Regions.ipynb`

This notebook investigates how well different score matching objectives estimate the score of a 2D Mixture-of-Gaussians distribution, particularly in areas where data is sparse.

It trains a score network using:
- **Sliced Score Matching (SSM)**
- **Finite Difference Score Matching (FDSM)**
- **Denoising Score Matching (DSM)** with two different noise levels (σ=0.4 and σ=1.0)

The notebook produces a series of quiver plots that visualize the learned score fields and compare them against the true score field. These plots illustrate how each method's estimated vector field behaves, especially in the regions between the Gaussian modes. The results allow for a qualitative comparison of how accurately each method captures the underlying data distribution's score function, even in challenging low-density areas.

### Analysis: Noise Schedules for Diffusion Models
**File:** `Schedules.ipynb`

This notebook explores various noise schedules that are critical to the performance and behavior of diffusion models. It plots and compares three different scheduling functions:
- **Linear**
- **Cosine**
- **Sigmoid**

Additionally, the notebook includes a practical demonstration of the forward noising process. It applies a fixed level of diffusion noise to an image at various resolutions (from 64x64 to 2048x2048), providing a visual intuition for how noise is added in diffusion models.
