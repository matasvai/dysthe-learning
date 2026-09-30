# Water-wave learning migration

First accept and pin the core water-wave reference and initial-packet contract.
Reusable architecture code must be audited independently of its previous
application; no old solver, dataset, loss or performance claim is automatically
eligible. In particular, the earlier optical PINN is not a water-wave baseline.

- `codex/fno-baseline`: build a one-profile-coordinate envelope adapter with
  complex channels, propagation rollouts and the core mean-flow convention.
- `codex/hybrid-solver`: retain the water-wave numerical step and learn a small
  correction; compare against a tuned numerical solver at matched accuracy.
- `codex/reduced-model`: test held-out packet and modulation compression before
  learning reduced dynamics; use only training fields to construct the basis.
- `codex/deeponet`: encode initial-packet samples and epsilon; query `(xi,tau)`.
- `codex/active-learning`: select development simulations for a declared wave
  observable, with a separate locked test set.

Start with FNO and hybrid after reference qualification. All branches address
the same water-wave model; alternatives are methods, not physical-scope pivots.
