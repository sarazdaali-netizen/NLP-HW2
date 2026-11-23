# NLP HW2 experiment reproducibility

## Task
Assess Qwen2.5-3B-Instruct answer-position sensitivity on the four-choice portion of ARC-Challenge (test split). Four cyclic rotations are evaluated per item using the same prompt and model. No fine-tuning.

## Requirements
Google Colab with NVIDIA T4 GPU (16 GB); Python 3; Hugging Face model/dataset downloads require internet access. Execute the notebook's installation cell first; package versions are printed and saved in the results.

## How to reproduce
1. Upload `NLP_HW2_Experiment.ipynb` to Colab.
2. Runtime > Change runtime type > T4 GPU.
3. Runtime > Run all.
4. Download `hw2_results.zip`, containing `results.json`, `all_predictions.csv`, `paired_differences.json`, `random_failure_examples.json`, figures, filtering counts, and environment information.

## Configuration
- Model: `Qwen/Qwen2.5-3B-Instruct`
- Dataset: `allenai/ai2_arc`, configuration `ARC-Challenge`, split `test`
- Random seed: `4057`; sampling: up to 200 eligible test questions
- Four cyclic permutations per sampled question
- Position uncertainty: 2,000 paired item bootstraps
- Position null test: 10,000 within-item shuffles; max-pairwise-difference statistic
- Flip threshold: lower 95% bootstrap bound > 0.10

## Interpretation
Use measured results, never template values, in the paper. The design **cannot distinguish label-token bias from serial-position bias**, because labels A–D always appear in physical order. The automatic filtering only catches some referential option text; manually inspect the sampled questions and disclose any remaining issues. The permutation test assesses position association, not causal mechanism.

## Reproducibility note
This experiment uses deterministic next-token letter logit comparison (not generated answer text). GPU/kernel nondeterminism is possible across machines; the notebook re-scores 16 prompts and checks for identical decisions.
