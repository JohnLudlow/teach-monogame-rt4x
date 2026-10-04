# Distinguished seeded randomness from tile-placement rules

The learner correctly explained that `Random(seed)` supplies a reproducible sequence but cannot enforce an ice/desert adjacency rule without terrain-generation logic. They specifically meant rejecting or retrying an invalid cell choice, not discarding the entire map, and recognised backtracking as important when earlier choices leave no valid candidate. This establishes the prerequisite for studying constraint propagation without claiming that backtracking has been implemented.
