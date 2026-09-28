# Confidence-Aware CNN

 A small program that reads handwritten digits and guesses which number it is, but if it is shown something that is not a digit at all, it should say "I do not know" instead of making something up.

 **Why-:** I chose this because real software frequently needs to know when it can trust its response and when it should confess it doesn't have enough information, and I want to know what it takes to develop and test that behaviour 

## Current Status

Experiment complete — documentation and handoff are finalized.

## Documentation and Code

- [Requirements](REQUIREMENT.md) — problem, scope, and goals
- [Decisions](DECISIONS.md) — important choices and why they were made
- [SDD](SDD.pdf) — model's system design and handover guide
- [Notebooks](notebooks/) — experiment and model implementation
- [Artifacts](artifacts/) — saved model and calibration parameters
- [Evaluation Log](logs/day5_evaluation.jsonl) — full evaluation records

## Current Flow

```text
Input Image
     ↓
Preprocessing
     ↓
CNN
     ↓
Confidence
     ↓
Answer / I don't know

```

## Project Structure

```text
Confidence-Aware-CNN/
├── artifacts/        # saved model and calibration parameters
├── notebooks/        # experiment work and results
├── logs/              # inference records and evaluation evidence
├── README.md          # project overview
├── REQUIREMENT.md     # problem, scope, and goals
├── DECISIONS.md       # decisions and reasoning
├── SDD.pdf            #  model's system design and handover guide
└── requirements.txt   # project dependencies

```
## Setup

```bash
pip install -r requirements.txt


