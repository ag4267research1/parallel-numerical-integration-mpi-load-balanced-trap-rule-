# MPI Parallel Numerical Integration

This repository contains an MPI-based parallel implementation of the trapezoidal rule for numerical integration. The project focuses on improving a basic MPI example by adding detailed output, robust input handling, dynamic load balancing, and performance evaluation across multiple processes and nodes.

*This project was developed as part of a university course on parallel computing.

## Project Overview

This implementation expands the classical parallel trapezoidal rule program with several major improvements:

- **Baseline MPI trapezoidal rule implementation**  
  Compiled and ran the original program to verify correctness and behavior.

- **Identified and documented limitations**  
  Noted issues such as fixed inputs, minimal output, and incorrect behavior when the number of processes does not divide the number of subintervals.

- **Enhanced formatted output**  
  Added printing of:  
  - True value of the integral  
  - True error  
  - Step size `h` and `h²`  
  - Number of intervals `n`  
  - Number of processes `p`  
  Output is aligned and readable for clarity and correctness checks.

- **Command-line parameter input**  
  Added user-provided input for:  
  - `a` (start of interval)  
  - `b` (end of interval)  
  - `n` (number of subintervals)

- **Robust error checking**  
  Validates input parameters, prints informative messages from process 0, and uses `MPI_Abort` for invalid cases.

- **Dynamic load balancing**  
  Implemented a generalized strategy so that the number of processes **no longer needs** to divide `n`.  
  Ensures each process receives nearly equal work with at most a one-interval difference.

- **Load distribution verification**  
  Optional output where each process prints:  
  `Process id: local_n subintervals from node ia to ib`  
  Confirms complete and correct coverage of the full interval.

- **Accurate performance timing**  
  Uses `MPI_Barrier` and `MPI_Wtime` to measure true wall-clock time.

- **Performance testing with multiple functions**  
  Included experiments using:  
  - `f(x) = x²`  
  - `f(x) = π sin(πx)`  
  Analyzed runtime differences and speedup behavior.

## How to Compile

```bash
mpicc -o trap trap.c -lm
