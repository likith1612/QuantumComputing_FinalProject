# Grover's Search Algorithm — Qiskit Implementation

A from-scratch implementation of **Grover's Quantum Search Algorithm** using the [Qiskit](https://qiskit.org/) framework, demonstrating quadratic speedup over classical unstructured search (O(√N) vs O(N)).

---

## Overview

This project (`Likith_final_project.ipynb`) builds and simulates a complete Grover's algorithm circuit on a 4-qubit system. It searches a space of **2⁴ = 16** possible states for two marked target states and visualizes the probability amplification across multiple iteration counts.

### What Is Grover's Algorithm?

Grover's algorithm is a quantum search algorithm that finds a marked item in an unsorted database of *N* items using only **O(√N)** queries, compared to the **O(N)** required classically. It works by repeatedly applying two operations:

1. **Oracle** — flips the phase of the target states.
2. **Diffusion** — amplifies the probability amplitude of the marked states (inversion about the mean).

---

## Key Components

| Component | Function | Description |
|---|---|---|
| `create_oracle(n, target_states)` | Phase-Flip Oracle | Marks the target states by flipping their phase (\|ψ⟩ → −\|ψ⟩) using multi-controlled X gates and auxiliary qubits. |
| `create_diffusion(n)` | Diffusion Operator | Implements the Grover diffuser: H → X → multi-controlled Z → X → H, amplifying marked state amplitudes. |
| Main Circuit | Full Grover Iteration | Applies Hadamard initialization followed by repeated oracle + diffusion iterations, then measures all qubits. |

---

## Experiment Configuration

| Parameter | Value |
|---|---|
| Number of Qubits | 4 |
| Search Space Size | 16 states |
| Target States | `'1010'`, `'0101'` |
| Iteration Counts | 1, 5, 10 |
| Measurement Shots | 4096 |
| Simulator | Qiskit Aer (`AerSimulator`) |

---

## How It Works

1. **Initialization** — All qubits begin in |0⟩. Hadamard gates create an equal superposition across all 16 basis states.
2. **Oracle** — The oracle circuit flips the phase of the target states `1010` and `0101`.
3. **Diffusion** — The diffusion operator inverts amplitudes about the mean, boosting the probability of measuring a target state.
4. **Repeat** — Steps 2–3 are repeated for the configured number of Grover iterations.
5. **Measurement** — All qubits are measured and results are collected over 4096 shots.
6. **Visualization** — A histogram displays the measurement outcome distribution for each iteration count.

---

## Expected Results

- **1 iteration** — Target states show noticeably higher probability than non-target states, but the contrast is moderate.
- **~3 iterations** (optimal for 4 qubits, 2 targets) — Target states dominate the histogram with near-maximal probability.
- **Too many iterations** (e.g., 10) — Probability "overshoots" and begins to decrease due to the periodic nature of the algorithm, demonstrating why choosing the correct number of iterations matters.

---

## Requirements

- Python 3.8+
- [Qiskit](https://pypi.org/project/qiskit/)
- [Qiskit Aer](https://pypi.org/project/qiskit-aer/)
- [Matplotlib](https://pypi.org/project/matplotlib/)
- [NumPy](https://pypi.org/project/numpy/)
- [SciPy](https://pypi.org/project/scipy/)
- [pylatexenc](https://pypi.org/project/pylatexenc/)

### Install

```bash
pip install -r requirements.txt
```

Or manually:

```bash
pip install qiskit qiskit-aer matplotlib numpy scipy pylatexenc
```

---

## Usage

```bash
jupyter notebook Likith_final_project.ipynb
```

Run all cells sequentially. The notebook will:
1. Define the oracle and diffusion operator circuits.
2. Build and simulate Grover's algorithm with 1, 5, and 10 iterations.
3. Display measurement histograms for each configuration.

---

## Project Structure

```
Quantum Computing/
├── Likith_final_project.ipynb   # Grover's Algorithm implementation
├── requirements.txt             # Python dependencies
└── README.md                    # This file
```

---

## References

- Grover, L. K. (1996). *A fast quantum mechanical algorithm for database search.* Proceedings of the 28th Annual ACM Symposium on Theory of Computing.
- [Qiskit Textbook — Grover's Algorithm](https://learning.quantum.ibm.com/course/fundamentals-of-quantum-algorithms/grovers-algorithm)