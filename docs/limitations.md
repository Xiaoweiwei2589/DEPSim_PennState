# Practical Limitations and “Gotchas”

This is a reality-based list. It is not marketing.

## 1) Coupling changes the dynamics
When CHARM coupling is enabled, CHARM forces/moments replace internal rotor model forces/moments. Any controller designed using only uncoupled linear models can degrade in coupled simulations and may require redesign using coupled linear models.

## 2) Fidelity is not uniform across all physics
Different subsystems have different fidelity levels (e.g., simplified inflow models vs free wake, lookup-table aerodynamics vs post-stall approximations). Treat results accordingly.

## 3) Inputs are powerful but easy to misuse
DEPSim is input-file driven. Small mistakes in:
- units
- axis conventions
- component numbering
- mixer scheduling
can cause “reasonable-looking” but wrong results. Always validate trim and sanity-check signs.

## 4) Not everything is distributable
Some dependencies and models are restricted. This repo does not include those.