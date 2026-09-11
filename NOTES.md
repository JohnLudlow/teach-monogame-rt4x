# Teaching Notes

- Learner: extensive C#/.NET experience; minimal MonoGame experience; has completed some tutorials.
- Development environment: Visual Studio and Visual Studio Code.
- Target: start with a prototype, then evolve `monogame-rt4x` into a full game.
- Teaching boundary: do not implement subject code for the learner; guide the learner to do it in `monogame-rt4x`.
- Repository boundary: store teaching material and toy exercises in this repository; use `docs/` for lessons, reference material, and reusable lesson assets.
- Prototype direction: top-down.
- Lesson 1 complete: the template project runs; learner correctly identified Update as game-state change and Draw as state presentation.
- Correction: `dotnet build` validates compilation; `dotnet run --project <project-path>` launches the game.
- Lesson UX: show every retrieval prompt before its answer; keep feedback prompts and retrieval prompts together.
