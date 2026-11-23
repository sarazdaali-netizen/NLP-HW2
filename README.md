# NLP HW2 – Answer Position Bias in Multiple-Choice Question Answering

## Project Description

This project investigates whether the accuracy of Qwen2.5-3B-Instruct on multiple-choice questions depends on the position of the correct answer.

We evaluate the model on the ARC-Challenge dataset using four cyclic permutations of the answer options.

## Model and Dataset

- **Model:** Qwen/Qwen2.5-3B-Instruct
- **Dataset:** allenai/ai2_arc (ARC-Challenge, test split)
- **Questions evaluated:** 200
- **Permutations per question:** 4
- **Total evaluations:** 800
- **Random seed:** 4057
- **Fine-tuning:** None

## Requirements

- Python 3
- Google Colab
- NVIDIA T4 GPU (16 GB)
- Internet connection for downloading the model and dataset

The notebook installs the required Python packages.

## How to Run

1. Download `NLP_HW2_GPU_Colab.ipynb` from this repository.
2. Open [Google Colab](https://colab.research.google.com/).
3. Upload the notebook.
4. Select **Runtime → Change runtime type → T4 GPU**.
5. Click **Runtime → Run all**.
6. Once execution finishes, download `hw2_results.zip`.

## Experiment Method

For each selected question:

1. Present the question with four answer choices.
2. Evaluate the model using next-token answer-letter scores.
3. Rotate the answer choices through positions A, B, C, and D.
4. Record whether the model selects the correct answer for each permutation.
5. Calculate accuracy by answer position and identify position-sensitive questions.

## Results

| Correct Answer Position | Accuracy |
|---|---|
| A | 75.5% |
| B | 84.0% |
| C | 78.0% |
| D | 76.0% |

- **Position-averaged accuracy:** 78.38%
- **Original-order accuracy:** 78.5%
- **Position-sensitive questions:** 21.5%
- **Position-effect permutation-test p-value:** Approximately 0.0029

The results suggest that changing the position of the correct answer can affect model performance even when the question and answer contents remain unchanged.

## Statistical Analysis

- 2,000 paired bootstrap samples for uncertainty estimation
- 10,000 within-question permutations for the position-effect test
- Randomly sampled failure examples
- Position-wise accuracy comparisons

## Reproducibility

The random seed is fixed at `4057`.

The experiment uses deterministic next-token answer-letter scoring rather than free-form answer generation. Small differences between computing environments may still occur.

The experiment does not distinguish between answer-label bias and physical answer-position bias because answer labels always follow the order A–D.

## Output Files

The notebook generates:

- `results.json`
- `all_predictions.csv`
- `paired_differences.json`
- `random_failure_examples.json`
- Accuracy and consistency figures
- Environment and filtering information

## Academic Context

Hanyang University  
CSE4057 – Natural Language Processing  
Homework 2 – November 2026
