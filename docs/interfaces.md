# Water-wave adapter requirements

Full-field methods consume `u(0,tau)`, steepness `epsilon`, the periodic tau grid,
requested propagation positions `xi` and normalization metadata. They return
physical complex envelopes `u(xi,tau)`, measured runtime and diagnostic data.
Case schema 2 and water-wave-dysthe-spatial-v1 are mandatory. The numerical RHS
and its nonlocal mean-flow operator belong to core, not individual ML adapters.

Distinguish propagation steppers from direct `(xi,tau)` predictors. Targets and
future reference fields must never enter inference. New initial packets must
not trigger retraining when evaluating operator generalization.

The active GP maps bounded packet parameters to selected scalar measurements,
such as peak amplification or propagation distance to a focusing event. Evaluate
scalar error, calibration and simulation budget separately from field methods.

Before marking a method implemented, provide a tiny fit/predict test, checkpoint
round trip, determinism metadata and held-out evaluation smoke run. Execution
checks do not establish accuracy. The registry remains unimplemented for now.

Shared training must include validation-rollout early stopping, best/last
checkpoints, resume state and component-wise physics-loss logs. Use the selected
water-wave PDE residual, periodicity, initial condition and verified wave-action
constraint; add other invariants only after verifying this noncanonical envelope
and boundary convention. Assess each loss by ablation and phase/field error.
Generic conservation is not sufficient, and foreign physical losses are excluded.
