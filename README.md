# trotter-methods-quantum-simulation
Quantum simulation of spin chains using Trotter-Suzuki decomposition methods (1st- and 2nd-order), built with Python and NumPy/Scipy.

# Trotter Methods for Quantum Simulation

This repository explores **Trotter-Suzuki decomposition** for simulating the quantum dynamics of **spin chains**, specifically the **1D transverse-field Ising model (TFIM)**.

We implement both:
-  **First-order Trotter approximation**
- **Second-order (Strang splitting)**
- Comparison to exact unitary evolution
- Fidelity tracking between methods

All code is written in **pure Python**, using `NumPy` and `SciPy` — no Qiskit required.


## 📓 Included Notebooks

| Notebook | Description |
|----------|-------------|
| `1_trotter_first_order.ipynb` | First-order Trotter decomposition and magnetization tracking |
| `2_trotter_second_order.ipynb` | More accurate Strang splitting version |
| `3_fidelity_comparison.ipynb` | Compare fidelity of Trotter-evolved vs exact states |
| `4_first_vs_second_order_fidelity.ipynb` | Side-by-side fidelity of 1st vs 2nd-order methods |


## Physics Background

We simulate time evolution under the **1D transverse-field Ising Hamiltonian**:

\[
H = -J \sum_{i} \sigma_i^z \sigma_{i+1}^z - h \sum_i \sigma_i^x
\]

Trotter decomposition allows us to split evolution under non-commuting terms:

\[
e^{-i H \Delta t} \approx e^{-i H_Z \Delta t} e^{-i H_X \Delta t} \quad \text{(1st order)}
\]
\[
e^{-i H \Delta t} \approx e^{-i H_X \Delta t/2} e^{-i H_Z \Delta t} e^{-i H_X \Delta t/2} \quad \text{(2nd order)}
\]

We track observables like:
- Average magnetization ⟨σᶻ⟩ per site
- Fidelity to exact evolution

