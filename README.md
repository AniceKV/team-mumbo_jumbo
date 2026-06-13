# 🧬 NSOC COMMAND: THE MODEL RECONSTRUCTION CHALLENGE
### 🌌 Operation: Rebuild from Chaos

Welcome, Operative, to the **NSOC Model Reconstruction Grid**! 

A database corruption event has fragmented a deep residual network. Its **$N$ constituent linear layers and block parameters** have been shattered into an unlabeled collection of weights (`piece_0.pth` to `piece_N.pth`). 

Your mission is to **perfectly reassemble the network's topology** and restore the model grid to achieve a Mean Squared Error (MSE) of **exactly 0.0** against the original intact model's classification predictions.

---

> [!IMPORTANT]  
> **OPERATIONAL BRIEFING**  
> The official guidelines, evaluation parameters, and scoring grids are documented in the [Official Rules Manual](file:///Users/chocopie/OPERATION-REBUILD_FROM_CHAOS/RULES.md). Please review them before deploying solutions.

---

## 🧩 THE SCRAMBLED COMPONENTS & MATRIX SHAPES

All $N$ weight fragments are isolated inside `data/pieces/`. To begin reassembly, you must classify each piece based on its **weight tensor dimensions**:

1.  **Front Projection Layer (`proj`):** Maps the input space dimension ($D_{\text{in}}$) to the intermediate latent space ($D_{\text{latent}}$).
2.  **Output Classification Layer (`last`):** Maps intermediate latent features ($D_{\text{latent}}$) to output classes ($D_{\text{classes}}$).
3.  **Block Input Projections ($W_{\text{in}}$):** Maps latent space dimensions to sub-block projection features ($D_{\text{sub}}$).
4.  **Block Output Projections ($W_{\text{out}}$):** Projects sub-block features back down to the latent space dimension ($D_{\text{latent}}$).

### 📐 The Deep Architecture
The original network consists of:
*   A front projection layer (`proj`).
*   **$K$ sequential residual blocks**. Each block $k$ maps intermediate latent features $x$ as:
    $$\text{Block}_k(x) = x + W_{\text{out}}^{(k)} \operatorname{ReLU}\left(W_{\text{in}}^{(k)} x + b_{\text{in}}^{(k)}\right) + b_{\text{out}}^{(k)}$$
*   A final output classification layer (`last`).

### 🔍 The Combinatorial Challenge
With a massive search space of potential combinations, brute-forcing is mathematically impossible. 

You must perform mathematical and structural analysis on the raw weight matrices to uncover indicator signals left behind during model training that allow you to:
1.  **Pair:** Match each input projection ($W_{\text{in}}$) to its corresponding output projection ($W_{\text{out}}$) for all $K$ blocks.
2.  **Sequence:** Order the $K$ reassembled blocks in their original sequential sequence ($0 \dots K-1$).

---

## 📦 COMPILER REPOSITORY TOPOLOGY

This workspace is structured as a self-contained local development environment:

```text
model-reconstruction-chaos/
├── data/
│   ├── pieces/                    # Scrambled weight fragments (piece_0.pth to piece_N.pth)
│   ├── historical_data.csv        # Calibration alignment telemetry
├── samples/
│   ├── sample_submission.csv      # Standard configuration layout
│   └── random_submission.csv      # Example randomized baseline mapping
├── starter_kit.ipynb              # Guided interactive forensic starter notebook
├── requirements.txt               # Required package dependencies
├── README.md                      # This main guide
└── RULES.md                       # Comprehensive Rule Book
```

---

## 🚀 GETTING STARTED (DEPLOYMENT GUIDE)

### 1. Synchronize the Repository
Operatives should establish their local working environment branch:
```bash
# Clone the central NSOC challenge grid
git clone https://github.com/chocopie247/OPERATION-REBUILD_FROM_CHAOS.git
cd model-reconstruction-chaos

# Spawn your dedicated team branch
git checkout -b team-[your_team_name]
```

### 2. Launch the Analytics Starter Notebook
We recommend opening the notebook first to understand how to load and parse the raw tensors:
```bash
jupyter notebook starter_kit.ipynb
```

### 3. Format Your Submission Payload
Save your optimal reassembled configuration as `submission.csv` containing a header `block_index,inp_piece,out_piece`. You only need to submit the block sequence mapping for indices $0 \dots K-1$:

```csv
block_index,inp_piece,out_piece
0,piece_A.pth,piece_B.pth
1,piece_C.pth,piece_D.pth
...
K-1,piece_Y.pth,piece_Z.pth
```
*(Refer to the files in `samples/` for concrete layout formats).*
---

## 🏆 LEADERBOARD JUDGING & TIE-BREAKERS

Submissions will be ranked on the leaderboard using the following sequential tie-breakers:
1.  **Prediction Logits MSE (Primary Metric):** Target: Exactly `0.0`.
2.  **Pairing Accuracy:** Target: $K/K$ correct connections.
3.  **Exact Sequence Match:** Target: Perfect sequential alignment.
4.  **Forward Evaluations (Efficiency Tie-Breaker):** Total number of model evaluations. The most computationally efficient solver wins.
5.  **Submission Timestamp:** Earliest transmission wins!

---

```
[OPERATIONAL DIRECTIVE]
RESTORE ALIGNMENT. REBUILD FROM CHAOS.
```
