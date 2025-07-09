# trotter-methods-quantum-simulation
Quantum simulation of spin chains using Trotter-Suzuki decomposition methods (1st- and 2nd-order), built with Python and NumPy/Scipy.

# Theory: Trotter Methods in Quantum Simulation

In quantum mechanics, time evolution is governed by the Schrödinger equation:

$$
i\hbar \frac{d}{dt} |\psi(t)\rangle = H |\psi(t)\rangle
\quad \Rightarrow \quad
|\psi(t)\rangle = e^{-i H t / \hbar} |\psi(0)\rangle
$$

When the Hamiltonian can be written as the sum of two **non-commuting** parts, \( H = A + B \), where \( [A, B] \ne 0 \), the exponential cannot be split directly:

$$
e^{-i (A + B) t} \ne e^{-i A t} e^{-i B t}
$$

---

## Trotter-Suzuki Decomposition

### First-Order Approximation

$$
e^{-i (A + B) \Delta t} \approx e^{-i A \Delta t} e^{-i B \Delta t} + \mathcal{O}(\Delta t^2)
$$

Applied over time \( t = N \Delta t \):

$$
e^{-i H t} \approx \left( e^{-i A \Delta t} e^{-i B \Delta t} \right)^N + \mathcal{O}(\Delta t)
$$

---

### Second-Order (Strang Splitting)

$$
e^{-i (A + B) \Delta t} \approx e^{-i A \Delta t / 2} e^{-i B \Delta t} e^{-i A \Delta t / 2} + \mathcal{O}(\Delta t^3)
$$

This is more accurate and time-reversible.

---

## Application to the Transverse-Field Ising Model (TFIM)

We simulate:

$$
H = -J \sum_i \sigma^z_i \sigma^z_{i+1} - h \sum_i \sigma^x_i
$$

Split into:

- \( H_Z = -J \sum \sigma^z_i \sigma^z_{i+1} \)
- \( H_X = -h \sum \sigma^x_i \)

Then evolve using Trotter steps:

- **First-Order:**

$$
|\psi(t + \Delta t)\rangle \approx e^{-i H_Z \Delta t} e^{-i H_X \Delta t} |\psi(t)\rangle
$$

- **Second-Order:**

$$
|\psi(t + \Delta t)\rangle \approx e^{-i H_X \Delta t / 2} e^{-i H_Z \Delta t} e^{-i H_X \Delta t / 2} |\psi(t)\rangle
$$

---

## 📉 Error Scaling

| Method           | Formula                                                      | Error per step      |
|------------------|---------------------------------------------------------------|----------------------|
| First-Order      | \( e^{-i A \Delta t} e^{-i B \Delta t} \)                     | \( \mathcal{O}(\Delta t^2) \) |
| Second-Order     | \( e^{-i A \Delta t/2} e^{-i B \Delta t} e^{-i A \Delta t/2} \) | \( \mathcal{O}(\Delta t^3) \) |
| Exact            | \( e^{-i (A + B) \Delta t} \)                                 | None (exact)         |

---

## Summary

Trotter decomposition is a foundational technique in quantum simulation. It enables efficient approximation of time evolution in systems with non-commuting Hamiltonian terms, using only the exponentials of simpler components.

Use first-order for fast simulations, and second-order (Strang) for improved fidelity with limited overhead.
