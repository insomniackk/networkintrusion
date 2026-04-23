# Network Intrusion Detection System

A machine learning pipeline that detects DDoS attacks in real network traffic using Random Forest classification and UMAP dimensionality reduction. Built on the CICIDS2017 dataset — the same unsupervised anomaly detection methodology I applied to ultrasound image filtering in medical imaging research, extended to a cybersecurity context.

---

## What it does

- Loads any CICIDS2017 CSV file via an interactive file picker
- Cleans and preprocesses 79 network traffic features
- Trains a Random Forest classifier to detect DDoS attacks vs normal traffic
- Visualizes results with an interactive 3D UMAP projection
- Outputs a styled performance report and feature importance breakdown

---

## Results

> Results generated using `Friday-WorkingHours-Afternoon-DDos.pcap_ISCX.csv`

| Metric | BENIGN | ATTACK |
|--------|--------|--------|
| Precision | 99.98% | 100.00% |
| Recall | 100.00% | 99.98% |
| F1 Score | 99.99% | 99.99% |
| Samples | 19,419 | 25,724 |
| **Overall Accuracy** | **99.99%** | |

**Top discriminative feature:** `init_win_bytes_forward` (initial TCP window size) — consistent with known DDoS attack behavior where attackers manipulate TCP handshake parameters to flood connections.

---

## Why the model works

DDoS attacks are repetitive by nature — thousands of machines doing the exact same thing simultaneously creates a distinct mathematical fingerprint in network traffic. The UMAP projection confirms this: attack traffic (red) and normal traffic (blue) occupy completely separate regions in feature space with no overlap, which is why the classifier achieves perfect separation.

Normal traffic is more spread out because browsing, streaming, and downloading all produce different network signatures. Attack traffic clusters tightly because it's fundamentally repetitive flooding behavior.

---

## Tech Stack

- **Python** — core language
- **Pandas** — data loading and preprocessing
- **Scikit-learn** — Random Forest classifier, train/test split, evaluation metrics
- **UMAP** — dimensionality reduction for visualization
- **Plotly** — interactive 3D visualization
- **Matplotlib** — feature importance chart
- **IPython Display** — styled HTML output in notebook

---

## Dataset

**CICIDS2017** — Canadian Institute for Cybersecurity Intrusion Detection System dataset.  
Download: https://www.unb.ca/cic/datasets/ids-2017.html

The dataset contains real network traffic captured over 5 days with labeled attack types including DDoS, Brute Force, DoS, Heartbleed, and Web Attacks. Each row represents one network connection with 79 features.

Files with attack traffic:
- `Friday-WorkingHours-Afternoon-DDos.pcap_ISCX.csv` — DDoS
- `Tuesday-WorkingHours.pcap_ISCX.csv` — Brute Force
- `Wednesday-WorkingHours.pcap_ISCX.csv` — DoS, Heartbleed
- `Thursday-WorkingHours-Morning-WebAttacks.pcap_ISCX.csv` — Web Attacks

---

## How to Run

1. Clone the repo and install dependencies:
```bash
pip install pandas scikit-learn umap-learn matplotlib plotly
```

2. Open `intrusion_detection.ipynb` in VS Code or Jupyter

3. Run all cells — a file picker will prompt you to select a CICIDS CSV

4. The notebook will automatically detect whether the file contains attack traffic and display a colored banner indicating the result

---

Contact nkmar@bu.edu for any questions.
