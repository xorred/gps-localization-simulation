# GPS User Localization — Mini Experiment

A small simulation study of **GPS-based user localization** and the effect of **signal timing errors on localization accuracy**.

## Overview

This mini experiment investigates how a user's position can be estimated using the known positions of multiple satellites and their signal travel times.

The experiment consists of four stages:

1. Calculate signal travel times from five fixed satellites to a known user.
2. Recover the user's position from the satellite locations and measured signal travel times.
3. Introduce random timing errors and observe their effect on localization accuracy.
4. Increase the timing-error standard deviation, repeat the experiment multiple times, and study the relationship between timing uncertainty and localization error.

The actual user position is fixed at:

```text
(100, 100, 100)
```

---

## Files

| File | Description |
|---|---|
| `gps_localization.tex` | Source code for the GPS localization experiment |
| `README.md` | Documentation and instructions |

---

## Experiment

### 1. Signal Travel Time

The distance between the user and each satellite is calculated using the Euclidean distance:

$$
d_i = \|s_i-u\|_2
$$

The signal travel time is then calculated as:

$$
t_i = \frac{d_i}{c}
$$

where

$$
c = 299792458\ \text{m/s}
$$

is the speed of light.

The calculated travel times are reported in microseconds ($\mu s$).

---

### 2. User Localization

The measured signal travel times are converted back into distances:

$$
d_i = t_i c
$$

The unknown user position is then estimated using **nonlinear least-squares optimization** based on the satellite positions and measured distances.

For the error-free case, the estimated position is approximately:

```text
[100. 100. 100.]
```

which matches the actual user position:

```text
[100, 100, 100]
```

This verifies that the localization procedure works correctly when there is no measurement noise.

---

### 3. Adding Timing Errors

Random timing errors are added to the signal travel times using a **zero-mean Gaussian distribution**.

The noisy measurements are converted into distances and used again for position estimation.

The localization error is calculated as:

$$
\text{Localization Error}
=
\|\hat{x} - x_{\text{actual}}\|_2
$$

where:

- $\hat{x}$ is the estimated user position.
- $x_{\text{actual}}$ is the actual user position.

As timing errors increase, the estimated distances become less accurate, which results in larger errors in the recovered user position.

---

### 4. Effect of Increasing Timing Errors

Different timing-error standard deviations are tested.

For each standard deviation, the experiment is repeated multiple times and the **average localization error** is calculated.

A graph is generated showing:

- **X-axis:** Timing Error Standard Deviation ($\mu s$)
- **Y-axis:** Average Localization Error

The experiment demonstrates that increasing timing uncertainty generally leads to increasing localization error.

---

## Requirements

The experiment uses:

- Python
- NumPy
- SciPy
- Matplotlib

Install the required packages using:

```bash
pip install numpy scipy matplotlib
```

---

## How to Run

Clone the repository:

```bash
git clone https://github.com/xorred/gps-localization-simulation.git
cd gps-localization-simulation
```

Install the required dependencies:

```bash
pip install numpy scipy matplotlib
```

The complete source code is available in:

[`gps_localization.tex`](https://github.com/xorred/gps-localization-simulation/blob/main/gps_localization.tex)

Open the file in a suitable environment and **run all cells from beginning to end** to execute the complete experiment.

> **Note:** The file contains Python code in a notebook-style format. If using an environment such as VS Code or Jupyter-compatible tools, execute the cells sequentially.

---

## Reproducibility

The timing errors are randomly generated, so the exact numerical results of the noisy experiments may vary between executions.

The results presented in the report correspond to the particular execution used for this mini experiment.

For reproducible results, a fixed random seed can be added to the Python code.

---

## Results

The experiment shows the following general behavior:

```text
Timing Error ↑
      ↓
Distance Estimation Error ↑
      ↓
Localization Error ↑
```

Therefore, accurate signal timing is important for obtaining accurate GPS-based position estimates.

---

## Author

**Sagar Sanjay Pawar**  
Indian Institute of Technology Kanpur

### Course

**CS724 — Sensing, Communications and Networking for Smart Wireless Devices**

**Assignment 1 — Mini Experiment**
