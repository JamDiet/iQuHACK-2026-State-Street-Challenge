# iQuHACK-2026-State-Street-Challenge
California Gurls team project for the State Street challenge at MIT iQuHACK 2026

**Summary:** We benchmarked Iterative Quantum Amplitude Estimation (IQAE) against Classical Monte Carlo for Value at Risk (VaR) estimation, demonstrating a quadratic speedup ($O(1/\epsilon)$ vs $O(1/\epsilon^2)$), and developed a novel "Soft-CVaR" architecture using Variational Quantum Signal Processing to bypass standard discontinuity bottlenecks.

## ⚡️ Quick Repo Tour

### 📄 The Writeup
* **[Read the Full Submission Report (PDF)](./submission.pdf)** *(Note: This is the compiled version of the LaTeX source provided)*

### 📊 Key Results
* **[Quantum vs Classical Error Scaling](./Graphs/estimation_error_IQAEvsmc.png)**: The core result demonstrating the $1/\epsilon$ scaling advantage of IQAE.
* **[15-Qubit Distribution Analysis](./Extension-New-Algo/15_qubit_analysis.png)**: Visualizing the smoothness of the encoded distribution at high qubit counts.
* **[Quantum Advantage Zones](./Graphs/quantum_advantage.png)**: Where IQAE beats Monte Carlo.

### ⚛️ Quantum Implementation (Classiq)
* **[IQAE with Bisection Search & Shot Scaling Analysis](./IQAE/IQAE_shot_sizes_comparison.ipynb)**: The main algorithm implementation connecting Classiq's IQAE to a classical search routine, and analysis code used to generate the error scaling plots.

### 🧠 Classical Benchmarks
* **[Monte Carlo Theory Guide](./Classical-MC/classical-monte-carlo.pdf)**: A brief overview of the $1/\sqrt{N}$ scaling derivation.
* **[Classical VaR Notebook](./Classical-MC/mc_classical_var.ipynb)**: The baseline Monte Carlo implementation.
* **[Classical MC w/ Real Data](./Classical-MC/mc_with_real_data.ipynb)**: Analysis of some real
data.

### 🚀 Novel Extension: Soft-CVaR
* **[Soft-CVaR Theoretical Framework](./Extension-New-Algo/Revised%20Variational%20Quantum%20Signal%20Processing%20for%20Smoothed%20Risk%20Measures.pdf)**: Our proposal for using Fenchel-Moreau smoothing and V-QSP to engineer risk functions with logarithmic polynomial degree requirements.