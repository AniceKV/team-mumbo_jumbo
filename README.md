# NSOC COMMAND: THE MODEL RECONSTRUCTION CHALLENGE

## Operation: Rebuild from Chaos

Welcome, Operative, to the **NSOC Model Reconstruction Grid**.

A catastrophic database corruption event has fragmented a trained deep residual network into an unlabeled collection of weight components. The model's **N constituent linear layers and block parameters** have been scattered across files named:

```text
piece_0.pth ... piece_N.pth
```

Your mission is to reverse-engineer the network, reconstruct its original topology, and restore the model with **perfect fidelity**.

The final objective is to recover the exact architecture and block ordering such that the reconstructed model achieves a **Mean Squared Error (MSE) of exactly 0.0** when compared against the original model's classification logits.

---

## Mission Objectives

Your reconstruction process must:

1. Identify the role of every weight fragment.
2. Correctly pair residual block components.
3. Recover the original sequential block ordering.
4. Reconstruct the complete network.
5. Achieve an exact prediction match with the original model.

---

> **IMPORTANT**
>
> Official evaluation details, scoring methodology, submission rules, and challenge constraints are described in **RULES.md**.
>
> Please read the rules carefully before attempting reconstruction.

---

# The Scrambled Components

All weight fragments are stored inside:

```text
data/pieces/
```

Each file contains one isolated parameter component from the original network.

Your first task is to classify every piece according to its tensor dimensions and structural properties.

The components belong to one of the following categories:

| Component | Description                                                          |
| --------- | -------------------------------------------------------------------- |
| `proj`    | Front projection layer mapping input features into latent space      |
| `last`    | Final classification layer mapping latent features to output classes |
| `W_in`    | Residual block input projection                                      |
| `W_out`   | Residual block output projection                                     |

---

# The Deep Architecture

The original model consists of:

1. A front projection layer (`proj`)
2. **K sequential residual blocks**
3. A final classification layer (`last`)

The overall forward pass is:

```text
Input
  │
  ▼
proj
  │
  ▼
Block₀
  │
  ▼
Block₁
  │
  ▼
...
  │
  ▼
Blockₖ₋₁
  │
  ▼
last
  │
  ▼
Output Logits
```

Each residual block transforms latent features `x` according to:

```math
Block_k(x)
=
x
+
W_{out}^{(k)}
ReLU
\left(
W_{in}^{(k)}x+b_{in}^{(k)}
\right)
+
b_{out}^{(k)}
```

where:

* `W_in^(k)` projects latent features into a hidden subspace.
* `ReLU` introduces non-linearity.
* `W_out^(k)` projects features back into latent space.
* The residual connection preserves information flow.

---

# Reconstruction Challenge

Simply identifying layer types is not enough.

You must solve two difficult forensic tasks:

## 1. Pairing

Determine which input projection belongs to which output projection.

Recover all pairs:

```text
(W_in^(0), W_out^(0))
(W_in^(1), W_out^(1))
...
(W_in^(K-1), W_out^(K-1))
```

A single incorrect pairing prevents perfect reconstruction.

---

## 2. Sequencing

After recovering valid block pairs, determine their original order:

```text
Block₀ → Block₁ → Block₂ → ... → Blockₖ₋₁
```

Since residual blocks are not labeled, the original sequence must be inferred through mathematical analysis of the weights and training-induced signatures.

---

# Why Brute Force Fails

The search space grows factorially with the number of blocks:

```math
K! \times (possible\ pairings)
```

Even for moderate values of `K`, exhaustive search becomes computationally infeasible.

Successful solutions will require:

* Weight matrix analysis
* Statistical signatures
* Spectral properties
* Correlation structures
* Learned feature alignment
* Training-induced fingerprints

rather than brute-force enumeration.

---

# Repository Structure

```text
model-reconstruction-chaos/
├── data/
│   ├── pieces/
│   │   ├── piece_0.pth
│   │   ├── piece_1.pth
│   │   └── ...
│   │
│   └── historical_data.csv
│
├── samples/
│   ├── sample_submission.csv
│   └── random_submission.csv
│
├── starter_kit.ipynb
├── requirements.txt
├── README.md
└── RULES.md
```

---

# Getting Started

## 1. Clone the Repository

```bash
git clone https://github.com/chocopie247/OPERATION-REBUILD_FROM_CHAOS.git

cd OPERATION-REBUILD_FROM_CHAOS
```

---

## 2. Create Your Team Branch

```bash
git checkout -b team-[your_team_name]
```

---

## 3. Launch the Starter Notebook

The provided notebook demonstrates how to:

* Load fragments
* Inspect tensor dimensions
* Analyze weight statistics
* Generate candidate pairings

Launch it with:

```bash
jupyter notebook starter_kit.ipynb
```

---

# Submission Format

Create a file named:

```text
submission.csv
```

with the following structure:

```csv
block_index,inp_piece,out_piece
0,piece_A.pth,piece_B.pth
1,piece_C.pth,piece_D.pth
...
K-1,piece_Y.pth,piece_Z.pth
```

where:

* `block_index` = recovered block position
* `inp_piece` = corresponding `W_in`
* `out_piece` = corresponding `W_out`

Only residual block mappings need to be submitted.

---

# Evaluation Criteria

Submissions are ranked using the following criteria:

## 1. Prediction Logits MSE (Primary)

Target:

```text
0.0
```

Perfect reconstruction yields an exact match with the original model.

---

## 2. Pairing Accuracy

```text
K / K Correct Pairings
```

---

## 3. Sequence Accuracy

Exact recovery of the original block ordering.

---

## 4. Computational Efficiency

Measured by:

```text
Total Forward Evaluations
```

Fewer evaluations rank higher.

---

## 5. Submission Timestamp

Earlier submissions win remaining ties.

---

# Recommended Strategy

Successful teams typically follow this workflow:

```text
Tensor Inspection
       │
       ▼
Role Classification
       │
       ▼
Pair Recovery
       │
       ▼
Block Ordering
       │
       ▼
Model Reconstruction
       │
       ▼
Prediction Validation
       │
       ▼
Final Submission
```

---

# Final Directive

```text
[OPERATIONAL DIRECTIVE]

RESTORE ALIGNMENT.
REBUILD THE NETWORK.
RECOVER THE TRUTH.

GOOD LUCK, OPERATIVE.
```
