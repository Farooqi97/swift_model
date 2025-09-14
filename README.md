# The SWIFT Model of Eye Movements  
**Simulation-Based Inference for Cognitive Parameter Estimation**

## 📖 Overview
This project applies **Simulation-Based Inference (SBI)** techniques, using the **BayesFlow** framework, to estimate parameters of a **SWIFT-inspired model of eye movements during reading**. The aim is to infer hidden cognitive parameters from observable eye fixation sequences (fixation durations and word positions), which can help test and refine mechanistic models of reading behavior.

The project implements two inference approaches:

- **Model 1:** Manual (handcrafted) summary statistics as features.
- **Model 2:** Learned summary embeddings via a BayesFlow neural summary network.

Additionally, it compares inference performance across different generative model variants:
- **Full Saliency Model**
- **No Saliency Model**
- **Random Model**

---

## 🧠 Background
The SWIFT model (Engbert et al., 2005) provides a dynamical account of how readers allocate attention and generate saccades (eye movements) while reading. It describes how **lexical activation** and **spatial attention gradients** influence **fixation durations** and **saccade targets**.

In this project, the main latent parameters are:

| Parameter | Description |
|-----------|-------------|
| **ν (nu)** | Attention spread (spatial extent of lexical activation) |
| **r** | Maximum lexical activation (peak activation level) |
| **µT (mu_T)** | Mean fixation duration (temporal scale of word processing) |

The generative model simulates fixation sequences (word indices and durations) using a gamma-distributed timing component and saliency-driven spatial selection mechanism.

---

## 📂 Project Structure
```
.
├── sbi_code.ipynb        # Main implementation notebook
├── sbi_report.pdf        # Full project report and results
├── requirements.txt      # Python dependencies
└── README.md              # This file
```

---

## ⚙️ Installation
1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/swift-eye-movements.git
   cd swift-eye-movements
   ```

2. **Create and activate a virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate      # on Linux/Mac
   venv\Scripts\activate         # on Windows
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

---

## 🧪 Usage
Launch Jupyter Notebook and run the main implementation file:

```bash
jupyter notebook sbi_code.ipynb
```

The notebook will:

1. Define priors for ν, r, µT.
2. Simulate fixation sequences from a SWIFT-like model.
3. Compute summary features (manual or learned).
4. Train a BayesFlow CouplingFlow network on 10,000 (θ, x) pairs.
5. Infer posterior distributions from real or held-out simulated fixation data.
6. Evaluate parameter recovery and calibration (posterior predictive checks, SBC).

---

## 📊 Data
- **Simulated fixation data:** 10,000 sequences for training and validation.
- **Real fixation data:** 40 observations used as test input.
- Each fixation record contains:
  - `TrialID`, `WordID`, `FixationStart`, `FixationEnd`, `WordFrequency`, `WordLength`, `SaccadeDirection`
- **Derived variable:**  
  `FixationDuration = FixationEnd - FixationStart`

---

## 📈 Results Summary
- **Model 1 (manual summaries)** recovered `r` and `µT` accurately, but `ν` poorly.
- **Model 2 (BayesFlow summaries)** showed similar performance with slightly improved calibration but not better accuracy.
- **Full saliency model** gave the best recovery performance, confirming the importance of saliency-based saccade targeting.
- Removing saliency greatly degraded recovery accuracy, especially for `µT`.

---

## 📚 References
- Engbert, R., Nuthmann, A., Richter, E. M., & Kliegl, R. (2005). SWIFT: A dynamical model of saccade generation during reading. *Psychological Review, 112*(4), 777.
- Radev, S. T. et al. (2023). BayesFlow: Amortized Bayesian workflows with neural networks. *JOSS, 8*(89):5702.
- Tejero-Cantero, A. et al. (2020). sbi–a toolkit for simulation-based inference. *arXiv preprint arXiv:2007.09114*.
- Engbert, R., & Rabe, M. M. (2024). A tutorial on Bayesian inference for dynamical modeling of eye-movement control during reading. *Journal of Mathematical Psychology, 119*.

---

## 📌 Future Work
- Combine handcrafted and learned summaries (hybrid approach).
- Extend model to heterogeneous readers and variable text difficulty.
- Improve recovery of ν via richer input features or longer sequences.

---

## 👤 Author
**Abdul Muqsit Farooqi**  
TU Dortmund University, 2025
