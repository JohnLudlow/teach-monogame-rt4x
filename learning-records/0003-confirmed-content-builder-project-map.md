# Confirmed content builder project map

The learner correctly explained that raw asset files belong in `FourxGame.ContentBuilder/Assets/`, with inclusion and processing rules defined in `FourxGame.ContentBuilder/Builder/Builder.cs`. They also correctly identified `BuildContent.targets` as the MSBuild bridge that builds the content-builder project and makes its generated output available to `FourxGame.MonoGame`. That mental model is now strong enough to move on to code-driven rendering without falling back to legacy MGCB workflow.
