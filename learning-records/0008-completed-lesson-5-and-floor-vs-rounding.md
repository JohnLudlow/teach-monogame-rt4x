# Completed Lesson 5 — coordinate systems, and floor-vs-rounding insight

The learner completed Lesson 5 (theory) and answered the retrieval check correctly, then
raised a sharp question that produced a durable insight.

## Retrieval check

- **Screen → World → Grid conversion chain?** Correct.
- **Which method inverts the camera transform?** Correct concept (<code>Matrix.Invert</code>;
  learner wrote "Matrix.Inverse" — the method is <code>Invert</code>).
- **Why <code>Math.Floor</code> over an <code>(int)</code> cast?** Correct: cast truncates toward
  zero, so −1 collapses to 0; floor rounds down consistently.

## The insight (learner-driven)

The learner asked: if flooring has a downward "bias", why not use a bias-correcting scheme
like banker's rounding (as `decimal`/finance do)?

Resolution: **grid-cell assignment is partitioning, not rounding.**

- Rounding answers "nearest integer to an ambiguous value" — `2.5` genuinely sits between
  two answers, so banker's rounding exists to stop directional bias accumulating.
- Flooring answers "which half-open interval `[n, n+1)` contains this point" — there is no
  ambiguity and no information loss. `Math.Floor(x / cellSize)` is *exact*, not biased.

Demonstrated with a throwaway console program (48px cell): `Math.Round`(banker's) puts
pixel 47 into cell 1 though it is inside cell 0 (0..47), and flips cells at the *centre* of
each visual cell — i.e. it places cell boundaries in the wrong place. Floor matches the drawn
grid lines exactly.

The only real subtlety with floor is the half-open boundary convention: `x = 48.0` belongs to
cell 1 (each cell owns its lower edge). This is also why floor (not truncation) is correct for
negatives.

## Zone of proximal development / next

- Strong conceptual grip: learner reasons about *why* a numeric technique is right, not just
  which to use. Lean into "which model is this really?" framing in future lessons.
- Next: Lesson 6 — Build coordinate utilities and camera (the refactor of Lesson 4's inline
  math into `Transforms`, `Camera`, and `Grid` methods).
