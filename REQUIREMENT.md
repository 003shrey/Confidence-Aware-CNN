# Requirements


## 1. Project Purpose
This project is a small experiment around a simple question:

> Can a program recognize when it does not have enough information
> to give a reliable answer, and say "I don't know" instead of
> confidently giving the wrong answer?

Handwritten-digit recognition is being used as a small, controlled
problem to explore this question.

The project is intentionally kept narrow so the problem can be taken
from definition to implementation and testing without unnecessary
complexity.

---

## 2. Problem

Even if a program consistently provides an answer, it may still be incorrect, particularly if it is given input that is different from what it was intended to handle.

For this, the system should be able to:
- identify handwritten numbers in the intended input;
- identify when an input is obviously not what was intended; and
- avoid forcing a digit prediction when it should not trust the result.

In the second scenario, a stated "I don't know" is preferred than a guessing digit.
---

## 3. Scope

### In Scope

- Handwritten digit images.
- Clearly non-digit inputs.
- Investigating whether the model's confidence can help decide when
  the system should abstain.
- Testing the system's behaviour on both types of input.
- Recording important decisions and changes as the project develops.

### Out of Scope

- Handling every possible kind of unknown input.
- Building a general solution for all types of unfamiliar data.
- Trying to solve the problem for every real-world image.
- Adding complexity that is not necessary for answering the main question.

The narrow scope is intentional. It keeps the experiment small enough
to investigate the main question properly.

---

## 4. Initial Hypothesis

My initial hypothesis is that confidence alone may not be enough to
reliably identify something the model has never seen before.

A separate check or additional signal may be needed.

## 5. Questions This Experiment Should Answer

- Can the system recognize when it should give a prediction?
- Can it recognize when it should abstain?
- Is confidence alone enough for this task?
- If it is not enough, what evidence shows its limitation?

The final conclusion should be based on what is actually tested rather
than what is expected beforehand.

This is only a starting hypothesis and has not yet been tested.

---

## 6. Project Constraints

- Keep the problem small enough to work through end-to-end.
- Avoid solving a much broader problem than the one defined here.
- Record important reasoning and decisions as the project changes.
- Keep the project understandable to another engineer who was not part
  of the original conversation.

---

## Open Questions

- How do I decide when the model should say "I don't know"?
- Is confidence alone enough to make that decision?
- What should I test to find out?
