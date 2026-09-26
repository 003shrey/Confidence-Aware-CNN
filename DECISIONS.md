# Decisions Log

## Day 1:- Basic Repo setup and Dataset selection

**Decision on Dataset selection:-** 

I will use handwritten *digits[MNSIT Dataset]* and *clearly non-digit inputs[CIFAR-10]* as the
first test case for this problem.

**Why:-** 

I'm looking for a straight forward scenario, in which the program clearly distinguishes between "what it is meant to recognize" and "what it is not".
Instead of attempting to handle every kind of input, this keeps theis small enough to test correctly.

**What I am purposefully not trying to solve:-** 

I am not trying to make the program recognize every kind of unknown
input. For now, the test will stay limited to these two clearly
different cases.

**Starting guess:-**  

I do not think making the program less confident will be enough to spot
something it has never seen before. I may need a separate check for
that.

**Alternative dataset considered:-**

I considered picking two similar looking dataset like, *digits vs letters* instead of *digits vs. clearly non-digit inputs*. I chose not to do this since it is easier to determine whether the system is working as intended when there is a clear distinction between what is "known" and what is "unknown".

**Status:-**  

Untested as of day 1.

---

## Day 2 — First Baseline and Evaluation Check
**What I did:-**

Started with a simple CNN for handwritten-digit recognition. Rather
than treat "final accuracy" alone as enough evidence, I compared it
against a Perceptron and a simple ANN(Artificial Nueral Network), and looked at individual
predictions where they disagreed.

**What I found:-**

- Perceptron: 91.67%
- ANN: 97.35%
- CNN: 99.14%

In one example, the Perceptron predicted "7" for an actual "1", while
the ANN and CNN both gets it right.

**What I learned from this:-**

A **single accuracy number**, doesn't show how models actually differ. Models can have different overall performance and still make different mistakes on individual examples.

**I discovered a problem:-**

I had been utilizing the same data I intended to use for the final test to track the model's development during training. Those initial results could not be relied upon as the **true baseline** because the test was no longer a fair, unaltered check.

**What I change to tackle this:-**

Reran the CNN, but this time split off a chunk of the training data to check progress on instead, and left the test set completely untouched until the very end.

**New Baseline:-**

Validation accuracy: 98.95%  
Test accuracy: 98.93%        

- Validation accuracy measures how well it performs on completely new, unseen data.
- Accuracy measures how well a model performs on the data it has already seen.
  
The model performed roughly as well on data it never saw as it did on data it verified itself against along the road, and the fact that these two figures are nearly identical is a positive early indicator.This gives a cleaner starting point for the next step.

**Why I stopped here:-**

At this point, the objective was to establish a clean, reliable baseline upon which the remainder of the experiment could be built, not to achieve the highest level of accuracy.
It was sufficient to proceed once validation and test accuracy were almost similar and within the typical range for this type of model. Spending more time tuning the model further would have
used up time without changing the actual question being tested.

**Final Decision:-**

Using this second run as the project baseline going forward.
The first notebook stays in the project history because it records
the initial exploration and why the evaluation setup was changed.

**Status:-**

Initial exploration complete. Clean baseline complete.

---

## Day 3 -  Checking Model Confidence (Temperature Scaling)

**Why temperature scaling:-**

A few different methods exist for this kind of adjustment. I picked temperature scaling because it's the simplest, it doesn't require retraining the model, just tuning one number afterward. Given theproject is meant to stay small, this was the natural first method to try, before considering anything more involved.

**What I did:-**

Added a calibration (adjusting how confident the model sounds) step to check whether the model's confidence could be made more reliable, then compared it before and after on familiar digits and on unfamiliar images.

- Calibration can be understand as "If a model says there is an 80% chance of rain, it should actually rain 80 out of 100 times you hear that prediction."
- Confidence  is a number showing how sure a model is about a single prediction it just made.
  
**What I found:-**

- Calibration didn't change predictions. On digits, it didn't clearly improve ECE (a score for how trustworthy the confidence is), slightly worse in this run and also confidence itself dropped a little.

- Confidence was already much lower on unfamiliar inputs than on familiar ones, and calibration lowered it further.

**What this made me realise:-**

Changing confidence does not automatically make it more reliable. However, the difference between familiar and unfamiliar inputs made confidence worth testing as a possible signal for when the model should **"answer"** or **"abstain"**.

**Decision:-**

Move forward with a confidence-threshold experiment to test whether
confidence can support an "I don't know" decision.

**What I chose not to test:-**

I didn't try other calibration methods beyond temperature scaling, and I didn't yet test harder, more similar-looking unfamiliar inputs. I only have the easy CIFAR-10 case ( low-resolution color images of non-digits). Both are reasonable next steps, but answering the core question didn't require them yet.

**Status**

Checking completed

---

## Day 4:- Looking at the Failures & Logging

**What I did:-**

- Looked at cases where the model was very confident but still wrong on handwritten digits. Also checked unfamiliar images(non-digits) to see whether the
model could still be very confident, even though those images were outside what it was built to recognize.

- Then I added logging: every time the model makes a decision, it now writes a record of - what it predicted, how confident it was, and
  whether it answered or said "I don't know", to a log file.

**What I found:-**

- On digits, 16 wrong predictions still had confidence above 95% before adjustment. After adjustment, 13 wrong predictions remained above 95%.
  
- On unfamiliar images (i.e, non-digits input), 27 out of 1000 were above 95% confidence before adjustment, 13 remained above 95% after ajustment.These aren't       *"wrong answers"* like in the digit cases. The images aren't digits, so there's nothing correct to compare against. The real concern is just that the model        sounded very sure about something it had no business recognizing at all.

The logging works as designed: it correctly recorded a familiar digit being answered, an unfamiliar image being rejected, and *most importantly* - an unfamiliar image that still passed the cutoff and got answered anyway. That last case is the clearest evidence of the exact limitation this project is testing.

**How I knew it worked, and what would have told me it hadn't:-**

I checked every logged record against a simple rule: 
- if confidence was at or above the cutoff, the verdict should say "answer". 
-  if below the cutoff, it should say "I don't know," with no prediction recorded.
  
  All records matched. It would have failed if any record showed a mismatch, like an *"I don't know" case* with a real prediction attached, or an *"answer" case* below the cutoff, either of those would have meant the logging logic was wrong, not just the model.

**What changed after I started building:-**

While building this, I noticed the log file would normally be hidden by settings meant to keep temporary files out of the repo. Since this log is the actual proof that logging works, I made sure it stays visible instead.

**What I chose not to do futher:-**

I only logged three example decisions, not the full dataset. The goal here was to prove the logging mechanism works correctly, not to log every single case logging at full scale.

I also did not add another detection method beyond confidence. This experiment already shows the limitation of relying on confidence
alone, fixing that limitation would be a different,  a larger project perhaps.

**Outcome:-**

Confidence is useful, but not enough on its own to safely decide whether an unfamiliar input should be answered.

**Status:-**

Day 4 complete - failure analysis and inference logging both done and
verified.

---

## Day 5:-
