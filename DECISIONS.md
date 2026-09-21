# Decisions Log

## Day 0: What the problem is - 
**Problem:** The goal is to determine whether  a program can accurately tell
the difference between "I know this answer" and "I don't have enough
information to answer." Most software either always answers or never
checks I want to see if it can check correctly.


**Scope:**
- In: a program that reads handwritten digits, and a way to test
  whether it correctly says "not sure" when shown something that
  isn't a digit at all.
- Out: Handling every type of input. It only needs to handle two
  clearly different kinds of input, on purpose, to keep the test clean.

**Starting guess:** I don't think making the program less confident will be enough to spot something it has never seen before. I think I may need a separate check for that. Untested as of today.
