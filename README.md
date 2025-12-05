# Error-Mitigation and Fidelity Analysis of a 5-Qubit GHZ State on IBM Runtime

A comprehensive quantum computing project analyzing the performance of a **5-qubit GHZ (Greenberger-Horne-Zeilinger) state** on IBM Quantum hardware, comparing ideal simulation, noisy hardware execution, and error-mitigated results.

[![Qiskit](https://img.shields.io/badge/Qiskit-1.0+-purple.svg)](https://qiskit.org/)
[![IBM Quantum](https://img.shields.io/badge/IBM_Quantum-Runtime-blue.svg)](https://quantum.ibm.com/)
[![Python](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/)

---

## Project Overview

This project explores quantum entanglement and noise characterization by:

1. **Building** a 5-qubit GHZ quantum circuit
2. **Simulating** on noise-free AerSimulator (ideal baseline)
3. **Executing** on real IBM quantum hardware (observing noise)
4. **Applying** error mitigation techniques
5. **Measuring** fidelity to quantify quantum state quality
6. **Visualizing** comparative results across all scenarios

### Key Results

| Experiment               | Expected Fidelity | Interpretation                |
| ------------------------ | ----------------- | ----------------------------- |
| **Simulator (Ideal)**    | ~0.99-1.00        | Perfect quantum state         |
| **Hardware (Raw)**       | ~0.65-0.85        | Significant noise degradation |
| **Hardware (Mitigated)** | ~0.75-0.92        | Partial noise suppression     |

**Improvement from mitigation:** 15-30% fidelity recovery

---

## What is a GHZ State?

A GHZ state is a **maximally entangled quantum state** involving multiple qubits:

```
|GHZ₅⟩ = (|00000⟩ + |11111⟩) / √2
```

### Properties:

- When measured, only two outcomes should appear: `00000` or `11111` (each ~50%)
- Extremely sensitive to quantum noise
- Perfect for benchmarking quantum hardware
- Scales exponentially in complexity

---

## Physics & Quantum Computing Concepts

### 1. Quantum Entanglement

The GHZ circuit creates a state where all 5 qubits are entangled. Measuring one qubit instantly determines all others.

### 2. Quantum Noise Sources

Real quantum computers suffer from:

- **Decoherence**: Qubits lose quantum information (~100 µs)
- **Gate Errors**: Imperfect quantum operations (~0.1-1% error)
- **Readout Errors**: Measurement mistakes (~1-5% error)

### 3. Fidelity Metric

Quantifies how close experimental results match the ideal state:

```
F = (Σ √(P_measured × P_ideal))²
```

- **F = 1.0**: Perfect quantum state
- **F < 0.8**: Heavily degraded by noise

### 4. Error Mitigation

IBM Runtime applies techniques to reduce noise impact:

- **Measurement Error Mitigation**: Corrects readout bias
- **Gate Twirling**: Averages coherent errors
- **Zero-Noise Extrapolation**: Estimates ideal results

---

## Repository Structure

```
GHZ_5Q_Project/
├── GHZ_5Q_Project.ipynb          # Main Jupyter notebook with full analysis
├── README.md                      # This file
├── requirements.txt               # Python dependencies
└── results/                       # Output directory (generated after running)
    ├── simulator_histogram.png
    ├── hardware_raw_histogram.png
    ├── hardware_mitigated_histogram.png
    ├── ghz_5_comparison.png
    ├── ghz_5_fidelity_comparison.png
    └── fidelity_results.json
```

---

## Installation & Setup

### Prerequisites

- Python 3.8 or higher
- IBM Quantum account (free): https://quantum.ibm.com/

### Step 1: Clone Repository

```bash
git clone https://github.com/yourusername/ghz-5-qubit-analysis.git
cd ghz-5-qubit-analysis
```

### Step 2: Install Dependencies

```bash
pip install -r requirements.txt
```

Or install individually:

```bash
pip install qiskit qiskit-aer qiskit-ibm-runtime matplotlib numpy jupyter
```

### Step 3: Configure IBM Quantum Access

1. Sign up at [IBM Quantum](https://quantum.ibm.com/)
2. Copy your API token from your account page
3. In the notebook, run the token-saving cell:

```python
from qiskit_ibm_runtime import QiskitRuntimeService

QiskitRuntimeService.save_account(
    channel='ibm_quantum',
    token='YOUR_API_TOKEN_HERE',
    overwrite=True
)
```

---

## Usage

### Quick Start

```bash
jupyter notebook GHZ_5Q_Project.ipynb
```

Then execute cells sequentially:

1. **Import libraries** - Load all required packages
2. **Build GHZ circuit** - Construct the 5-qubit entangled state
3. **Define fidelity functions** - Set up quality metrics
4. **Run simulator** - Get ideal baseline (< 1 second)
5. **Save IBM token** - One-time authentication setup
6. **Run on quantum hardware** - Execute on real quantum computer (5-30 minutes)
7. **Compare results** - Generate plots and analysis

### Expected Runtime

- **Simulator**: < 1 second
- **IBM Hardware**: 5-30 minutes (depends on queue)

## Results Interpretation

### Simulator Results

- **Fidelity ≈ 1.0** (perfect)
- Only `00000` and `11111` appear
- Confirms circuit design is correct

### Raw Hardware Results

- **Fidelity drops** to 0.65-0.85
- Many incorrect states emerge
- Demonstrates real-world quantum noise

### Error-Mitigated Results

- **Fidelity improves** to 0.75-0.92
- Incorrect states suppressed
- Shows mitigation effectiveness

## References & Further Reading

### Academic Papers

- **GHZ State**: Greenberger, D. M., Horne, M. A., & Zeilinger, A. (1989). _Going Beyond Bell's Theorem_
- **Error Mitigation**: Temme, K., et al. (2017). _Error Mitigation for Short-Depth Quantum Circuits_. Physical Review Letters, 119(18)

### Documentation

- [Qiskit Textbook](https://qiskit.org/learn)
- [IBM Quantum Documentation](https://docs.quantum.ibm.com/)
- [Qiskit Runtime Guide](https://docs.quantum.ibm.com/api/qiskit-ibm-runtime)

### Tutorials

- [Building Entangled States](https://qiskit.org/textbook/ch-gates/multiple-qubits-entangled-states.html)
- [Error Mitigation Techniques](https://qiskit.org/ecosystem/ibm-runtime/tutorials/error-mitigation.html)

## Contributing

Contributions are welcome! Areas for improvement:

1. **Test on different backends**: Compare hardware generations
2. **Increase qubit count**: Study scalability (6, 7, 8 qubits)
3. **Implement state tomography**: Full density matrix reconstruction
4. **Add more error metrics**: Entanglement witness, concurrence
5. **Optimize transpilation**: Reduce circuit depth

### How to Contribute

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-analysis`)
3. Commit changes (`git commit -am 'Add new analysis'`)
4. Push to branch (`git push origin feature/new-analysis`)
5. Open a Pull Request

---

_This project demonstrates fundamental quantum computing concepts and is ideal for students, researchers, and quantum computing enthusiasts._
