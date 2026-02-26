# DEPSim Overview

DEPSim (Distributed Electric Propulsion Simulation) is a simulation environment originally developed to model distributed electric propulsion aircraft, but it is general enough to model conventional rotorcraft and fixed-wing aircraft as well.

At a high level, DEPSim combines:
1. **PSUDEPSim** — a flight dynamics simulator (originally MATLAB/Simulink-based, set up for C code generation), and
2. **CHARM Rotor Module** — a higher-fidelity aeromechanics tool used to compute rotor/lifting-surface forces and moments, including interactional effects.

## Standalone vs coupled operation

- **Standalone PSUDEPSim mode:** internal low-/mid-fidelity aeromechanics (e.g., blade element rotor model with inflow model, lookup tables for lifting surfaces) is used.
- **Coupled mode:** CHARM replaces internal rotor aeromechanics with CHARM-computed forces and moments during simulation. A brief “phase over” is used so the simulation transitions smoothly from internal forces/moments to CHARM forces/moments.

[IMAGE PLACEHOLDER: diagram of phase-over timeline / blending]

## Why people use DEPSim

DEPSim is commonly used for:
- initial trim solutions and rapid flight-dynamics studies
- controller prototyping (e.g., dynamic inversion approaches)
- exploring the effects of rotor–rotor and rotor–airframe interactions on dynamics
- generating linear models for analysis and control design (uncoupled and coupled)

## What DEPSim is not

DEPSim is not meant to replace full CFD or full flexible-body FEA/CFD coupling for all regimes. In practice, users treat it as a tool that balances:
- richer physics than purely low-fidelity “performance-only” tools, and
- lower cost than very high-fidelity CFD-based approaches.