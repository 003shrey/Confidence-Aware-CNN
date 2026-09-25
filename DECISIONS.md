# Decisions Log

## Day 1:- Basic Repo set and Dataset selection

**Decision:** 

I will use handwritten digits[MNSIT Dataset] and clearly non-digit inputs[CIFAR-10] as the
first test case for this problem.

**Why:** 

I'm looking for a straight forward scenario, in which the program clearly distinguishes between "what it is meant to recognize" and "what it is not".
Instead of attempting to handle every kind of input, this keeps theis small enough to test correctly.

**What I am purposefully not trying to solve:** 

I am not trying to make the program recognize every kind of unknown
input. For now, the test will stay limited to these two clearly
different cases.

**Starting guess:**  

I do not think making the program less confident will be enough to spot
something it has never seen before. I may need a separate check for
that.

**Status:**  

Untested as of day 1.

---

## Day 2 — First Baseline and Evaluation Check
**What I did:**

Started with a simple CNN for handwritten-digit recognition. Rather
than treat "final accuracy" alone as enough evidence, I compared it
against a Perceptron and a simple ANN(Artificial Nueral Network), and looked at individual
predictions where they disagreed.

**What I found:**

- Perceptron: 91.67%
- ANN: 97.35%
- CNN: 99.14%

In one example, the Perceptron predicted "7" for an actual "1", while
the ANN and CNN both gets it right.

**What I learned from this:**

A **single accuracy number**, doesn't show how models actually differ.
Models can have different overall performance and still make different
mistakes on individual examples.

**I discovered a problem:**

I had been utilizing the same data I intended to use for the final test to track the model's development during training. Those initial results could not be relied upon as the **true baseline** because the test was no longer a fair, unaltered check.

**What I change to tackle this:**

Reran the CNN, but this time split off a chunk of the training data to check progress on instead, and left the test set completely untouched until the very end.

**New Baseline:**

Validation accuracy: 98.95%  
Test accuracy: 98.93%        

- Validation accuracy measures how well it performs on completely new, unseen data.
- Accuracy measures how well a model performs on the data it has already seen.
  
The model performed roughly as well on data it never saw as it did on data it verified itself against along the road, and the fact that these two figures are nearly identical is a positive early indicator.This gives a cleaner starting point for the next step.

**Final Decision:**

Using this second run as the project baseline going forward.
The first notebook stays in the project history because it records
the initial exploration and why the evaluation setup was changed.

**Status:**

Initial exploration complete. Clean baseline complete.

---

## Day 3 -  Checking Model Confidence

**What I did:**

Added a calibration (adjusting how confident the model sounds) step to check whether the model's confidence could be made more reliable, then compared it before and after on familiar digits and on unfamiliar images.

- Calibration can be understand as "If a model says there is an 80% chance of rain, it should actually rain 80 out of 100 times you hear that prediction."

**What I found:**

- Calibration didn't change predictions. On digits, it didn't clearly improve ECE (a score for how trustworthy the confidence is), slightly worse in this run and also confidence itself dropped a little.

- Confidence was already much lower on unfamiliar inputs than on familiar ones, and calibration lowered it further.

**What this made me realise:**

Changing confidence does not automatically make it more reliable.
However, the difference between familiar and unfamiliar inputs made
confidence worth testing as a possible signal for when the model should
**"answer"** or **"abstain"**.

**Decision**

Move forward with a confidence-threshold experiment to test whether
confidence can support an "I don't know" decision.

**Status**

Checking completed

---

## Day 4:- 
