# Rendered first grid and kept state in Update

The learner successfully rendered a code-drawn top-down grid in `FourxGame.MonoGame`, proving they can create a `Texture2D` in code and use `SpriteBatch` to stretch it into line rectangles. Their retrieval answer preserved the important architectural rule: state changes such as unit movement and any resulting game consequences belong in `Update`, while `Draw` only presents the current state.
