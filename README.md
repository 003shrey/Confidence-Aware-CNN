# Confidence-Aware CNN

 A small program that reads handwritten digits and guesses which number it is, but if it is shown something that is not a digit at all, it should say "I do not know" instead of making something up.

 **Why-:** I chose this because real software frequently needs to know when it can trust its response and when it should confess it doesn't have enough information, and I want to know what it takes to develop and test that behaviour 

## Current Status

In progress — Day 2: Baseline model setup is complete.

## Documentation

- [Requirements](REQUIREMENT.md) — problem, scope, and goals
- [Decisions](DECISIONS.md) — important choices and why they were made
- [Notebooks](notebooks/) — model exploration and experiments

## Current Flow

```text
Input Image
     ↓
Preprocessing
     ↓
CNN
     ↓
Prediction + Confidence

```

## Setup

```bash
pip install -r requirements.txt


