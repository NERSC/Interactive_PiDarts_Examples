# Monte Carlo π Estimation with MPI

This notebook demonstrates how to estimate π (pi) using the Monte Carlo "dart-throwing" method, 
and how to parallelize the computation using MPI (`mpi4py`) in a High-Performance Computing (HPC) environment.

## Overview

The Monte Carlo method approximates π by randomly generating points in a square and counting how many fall inside a quarter circle.
The ratio of points inside the quarter circle to the total number of points approaches π/4 as the number of points increases.

### Learning Goals

- Understand the Monte Carlo method for estimating π.
- Learn basic MPI concepts: **rank**, **size**, and **reduce** operations.
- See how to run Python MPI programs in an HPC environment using Slurm.

## Requirements

- Python 3
- `numpy`
- `mpi4py`
- (Optional) `matplotlib` for visualization

Install with:
```bash
pip install numpy mpi4py matplotlib
```

## Structure

1. **Serial Implementation**  
   Demonstrates the Monte Carlo method on a single process.

2. **MPI Implementation**  
   Parallelizes the computation across multiple ranks (processes) using `mpi4py`.

3. **HPC Job Submission**  
   Example of a Slurm job script to run the MPI version on an HPC cluster.

## Running the Code

### Locally with mpiexec
```bash
mpiexec -n 4 python pi_mpi.py
```

### On an HPC Cluster (Slurm)
Example `run_pi.slurm` script:
```bash
#!/bin/bash
#SBATCH -J pi
#SBATCH -N 1
#SBATCH -n 8
#SBATCH -t 00:02:00
#SBATCH -o pi-%j.out

module load python  # Load your environment/module as required
srun python pi_mpi.py
```

Submit with:
```bash
sbatch run_pi.slurm
```

## Key MPI Concepts in This Notebook

- **Rank**: The unique ID of a process in an MPI program.
- **Size**: Total number of processes in the MPI communicator.
- **Reduce**: Combines values from all processes to a single result on a designated root process.

## Output Example
```
π≈3.141592  (N=4000000, ranks=4)
```

## License
This material is for educational purposes as part of an Introduction to HPC Bootcamp.
