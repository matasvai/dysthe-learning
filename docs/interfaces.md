# Adapter requirements before declaring a method implemented

Full-field methods consume initial complex fields, equation coefficients,
coordinates, requested times, and normalization metadata. They return physical
complex fields on the requested grid plus measured runtime and diagnostic data.
The training method owns its weights/basis; equation definitions live in core.

Keep one-step models and direct space-time predictors explicit. Define exactly
which inputs are available at inference; targets and future reference fields
must never enter a rollout. A new initial condition must not trigger retraining
when measuring operator generalization.

The active GP consumes a declared finite parameter vector and predicts selected
scalar observables with uncertainty. Evaluate calibration and simulation budget;
do not compare its scalar output as though it reconstructs the full field.

Before changing `implemented` to true, provide an adapter, tiny fit/predict test,
checkpoint round trip where applicable, determinism metadata and a held-out
evaluation smoke run. Those checks establish execution, not accuracy.

Early stopping, validation rollouts, best/last checkpoints, resume state and
physics-loss component logging belong to the shared training infrastructure.
Compute physical penalties from the selected equation and normalization. Do not
reuse Vlasov positivity, particle energy, or Landau damping losses for Dysthe.
