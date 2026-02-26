# Architecture (Public Summary)

## Core modules

**PSUDEPSim**
- Implements nonlinear 6-DOF rigid-body dynamics and a modular aircraft model composed of rotors, wings, tails, fuselage, motors, and actuators.
- Historically developed in MATLAB/Simulink and prepared for code generation to enable faster execution and coupling.

**CHARM Rotor Module**
- Provides higher-fidelity aeromechanics for rotors and lifting surfaces, including wake models capable of representing interactional aerodynamics.

## Data exchanged (conceptual)

At each simulation step (conceptually):
1. PSUDEPSim provides CHARM with the instantaneous aircraft state and control/effectors needed for aeromechanics.
2. CHARM returns aerodynamic forces and moments.
3. PSUDEPSim integrates the equations of motion using those forces/moments.

[IMAGE PLACEHOLDER: “state/control → CHARM → forces/moments → EOM integration” loop diagram]

## Controller context (high level)

DEPSim/PSUDEPSim workflows often involve:
- trimming to a steady flight condition
- generating linear models (uncoupled or coupled)
- designing/tuning a controller (commonly dynamic inversion variants)
- running closed-loop maneuvers

Important practical note: coupling to CHARM changes predicted forces/moments; controllers designed purely from uncoupled models may degrade, so re-identification or redesign based on coupled linear models is often needed.