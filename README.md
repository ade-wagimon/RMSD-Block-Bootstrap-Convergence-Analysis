# RMSD-Block-Bootstrap-Convergence-Analysis

This repository provides a Python implementation to analyze the convergence of molecular dynamics (MD) simulations using block bootstrap resampling. The primary goal is to assess the equilibration time and convergence of RMSD (Root Mean Square Deviation) data from simulation steps.

## Features

- **Block Bootstrap Resampling**: Implements block bootstrap to resample data with specified block sizes.
- **RMSD Data Analysis**: Reads RMSD data from a file and performs convergence analysis using block bootstrap.
- **Convergence Detection**: Determines the equilibration time based on bootstrap confidence intervals.

## Prerequisites

- Python 3.x
- NumPy
- Matplotlib

You can install the required Python packages using pip:

```sh
pip install numpy matplotlib
```

## Installation

1. Clone the repository:

```sh
git clone https://github.com/yourusername/block-bootstrap-convergence.git
cd block-bootstrap-convergence
```

2. Install the required dependencies:

```sh
pip install numpy matplotlib
```

## Usage

1. Prepare your RMSD data file (`rmsd.dat`), where each line contains a single RMSD value.

2. Use the provided functions to read the RMSD data, perform block bootstrap convergence analysis, and plot the results.

### Example

```python
import numpy as np
import matplotlib.pyplot as plt

# Import the functions
from block_bootstrap_convergence import read_rmsd_data, block_bootstrap_convergence

# Read RMSD data from file
filename = "rmsd.dat"
rmsd_data = read_rmsd_data(filename)

# Perform block bootstrap convergence analysis
converged, equilibration_time, block_means, bootstrapped_means = block_bootstrap_convergence(rmsd_data)

if converged:
    print("Simulation converged at step:", equilibration_time)
else:
    print("Simulation might not be converged yet.")

# Plot block means and confidence intervals
plt.plot(block_means, label="Block Means")
alpha = 0.05
percentiles = np.percentile(bootstrapped_means, [alpha * 100, (1 - alpha) * 100], axis=0)

# Shade the confidence interval area
plt.fill_between(range(len(block_means)), percentiles[0], percentiles[1], alpha=0.2, label="Confidence Interval")
plt.legend()
plt.xlabel("Block Index")
plt.ylabel("Block Mean RMSD")
plt.title("Block Means and Confidence Interval")
plt.show()
```

## Functions

### `block_bootstrap(data, block_size)`

Performs block bootstrap on a given data array.

- **Args**:
  - `data (np.ndarray)`: The data array.
  - `block_size (int)`: The size of blocks for resampling.

- **Returns**:
  - `np.ndarray`: A 2D array of bootstrapped samples.

### `read_rmsd_data(filename)`

Reads RMSD data from a file.

- **Args**:
  - `filename (str)`: Path to the file containing RMSD data.

- **Returns**:
  - `np.ndarray`: Array of RMSD values.

### `block_bootstrap_convergence(rmsd_data, block_size=10, n_bootstraps=100, alpha=0.05)`

Analyzes convergence of MD simulation using block bootstrap.

- **Args**:
  - `rmsd_data (np.ndarray)`: Array of RMSD values for each simulation step.
  - `block_size (int, optional)`: Size of blocks for bootstrapping. Defaults to 10.
  - `n_bootstraps (int, optional)`: Number of bootstrap replicates. Defaults to 100.
  - `alpha (float, optional)`: Significance level for convergence check. Defaults to 0.05.

- **Returns**:
  - `tuple`: (bool, float, np.ndarray) - Whether converged (True), equilibration time (int), block means of original data

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgements

- This project was inspired by the need to analyze molecular dynamics simulation data for convergence and equilibration time.
- Thanks to the NumPy and Matplotlib libraries for providing powerful tools for data analysis and visualization.
```

You can save this content as `README.md` in your GitHub repository. Adjust the project title, repository link, and any other details as needed.
