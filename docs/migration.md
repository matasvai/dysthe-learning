# Learning migration

The source snapshot is matasvai/dysthe-pinn `bca8aa3833d79e5030ed53efab3bd94c9480aa54`.
The shared core port must be available first.

- `codex/fno-baseline`: extract the reusable model from `src/field_fno/model.py`;
  reconcile the optical adapter with the core equation and data layout.
- `codex/hybrid-solver`: define the coarse numerical step and learned correction;
  compare against an equally tuned numerical solver at matched error and cost.
- `codex/reduced-model`: check held-out field/disturbance compression before
  fitting reduced dynamics. Learn the basis from training trajectories only.
- `codex/deeponet`: condition on initial-field samples, coefficients and query
  coordinates. Keep full initial-condition trajectories disjoint across splits.
- `codex/active-learning`: define the scalar observable and acquisition policy;
  active sampling may use development data, never the locked test set.

The existing PINN remains a single-initial-field baseline until an explicit
conditioning design is implemented. Historical plasma results are not optical
Dysthe performance evidence. Model branches begin at the same shared scaffold.
