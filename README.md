# Confidence-Aware CNN

A CNN trained on MNIST, used to investigate whether model confidence
can support safe abstention when encountering out-of-distribution
inputs such as CIFAR-10.

## Status

In progress — Day 1: repository setup and baseline model.

## Core Question

Is confidence calibration (temperature scaling) sufficient for safe
abstention under distribution shift, or does it mainly improve
confidence reliability on in-distribution data?

## Experimental Setup

The model will be evaluated under four conditions:

- Raw confidence on MNIST
- Calibrated confidence on MNIST
- Raw confidence on CIFAR-10
- Calibrated confidence on CIFAR-10

## Setup

```bash
pip install -r requirements.txt
