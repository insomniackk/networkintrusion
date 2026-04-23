# Network Intrusion Detection System

A machine learning pipeline that detects DDoS attacks in real network traffic using Random Forest classification and UMAP dimensionality reduction. Built on the CICIDS2017 dataset.

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

**Top discriminative feature:** `init_win_bytes_forward` (initial TCP window size), which is consistent with known DDoS attack behavior where attackers manipulate TCP handshake parameters to flood connections.

---

## Why the model works

DDoS attacks are repetitive by nature. Thousands of machines doing the exact same thing simultaneously creates a distinct mathematical fingerprint in network traffic. The UMAP projection confirms this: attack traffic (red) and normal traffic (blue) occupy completely separate regions in feature space with no overlap, which is why the classifier achieves perfect separation.

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

## Real World Impact

DDoS attacks are one of the most disruptive and frequently used cyberattack vectors in both civilian and defense contexts. In 2023 alone, DDoS attacks increased by over 200% globally, targeting critical infrastructure including power grids, military networks, financial systems, and government communications.

In defense contexts specifically, the ability to automatically detect and flag anomalous network traffic in real time is vital. A compromised military network or overwhelmed command-and-control system can have direct operational consequences. Manual detection is not viable at scale when dealing with millions of network connections per hour.

This system addresses that gap by:

Automating threat detection — no manual review needed, the model flags attacks instantly

Generalizing across attack types — the same pipeline works on DDoS, Brute Force, DoS, and Web Attacks by loading different CICIDS files

Providing explainability — the feature importance breakdown tells operators exactly which network signals triggered the detection, important in high stakes environments where decisions need to be justified

Scaling to large datasets — tested on 225,000+ real network connections with sub-minute inference time

The UMAP visualization adds an additional layer of value for defense analysts — rather than a black box prediction, operators can visually confirm that attack traffic is structurally distinct from normal traffic.

--
Contact nkmar@bu.edu for any questions.
