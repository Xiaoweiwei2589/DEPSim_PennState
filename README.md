# DEPSim (Distributed Electric Propulsion Simulation) — Public Overview

> **This repository does NOT contain the DEPSim source code or executable binaries.**
> It is a public documentation hub describing DEPSim’s capabilities, workflow, and I/O interfaces.

DEPSim is a mid-fidelity simulation environment for distributed electric propulsion (DEP) aircraft that couples:
- **PSUDEPSim**: a 6-DOF nonlinear flight-dynamics simulator originally developed in MATLAB/Simulink and auto-coded to C for performance and coupling, and
- **CHARM Rotor Module**: higher-fidelity aeromechanics for rotors and lifting surfaces, enabling rotor–rotor and rotor–airframe interaction modeling.

This coupling approach is widely used in DEPSim-related publications and internal documentation.  
See the DEPSim manual for the canonical software architecture schematic and description of standalone vs coupled operation.  
[IMAGE PLACEHOLDER: architecture block diagram showing PSUDEPSim ↔ CHARM data exchange]

## What this repo is (and isn’t)

### ✅ This repo provides
- A **high-level description** of DEPSim architecture and workflow
- A **non-proprietary description** of key input/output files (formats, roles, typical usage)
- References to public literature describing the simulator and example applications
- Guidance for researchers/students on how to reason about cases, trims, linearization, and controller workflows

### ❌ This repo does NOT provide
- DEPSim binaries or source code
- CHARM libraries, build scripts, or proprietary dependencies
- Restricted aircraft models, parameter sets, or sponsor/NDA materials

## Capabilities (high level)

DEPSim was developed to support flight dynamics and controls analysis for DEP aircraft, with optional CHARM coupling for higher-fidelity aeromechanics and interactional effects.

Typical capabilities include:
- 6-DOF nonlinear simulation of VTOL / fixed-wing / compound configurations
- Modular modeling of rotors, wings, tails, fuselage, motors, actuators
- Automated trimming and numerical linearization workflows
- Built-in (optional) dynamic inversion control structure for stabilization and maneuver execution
- Optional CHARM coupling to replace internal rotor models with CHARM-predicted forces/moments during simulation

For technical background and demonstrations, see:
- Theron et al., integrated tool for e-VTOL aeromechanics and flight control analysis (VFS 2020).  
- Theron & Horn et al., nonlinear dynamic inversion control for UAM aircraft (VFS 2020).  
- Gan et al., coupled flight dynamics + free wake + acoustics predictions (VFS 2021).

[IMAGE PLACEHOLDER: example vehicle (OpenVSP rendering) + example response plots]

## How DEPSim is organized (conceptual)

DEPSim separates:
- **core simulator code** (aircraft-agnostic) and
- **aircraft-specific models** (inputs, tables, cases, commands, and outputs stored per aircraft).

The manual describes a directory structure with a top-level simulator and an `AircraftModels/` tree containing subfolders per aircraft, each holding case files, command files, CHARM inputs, trim states, and results.

[IMAGE PLACEHOLDER: directory tree schematic]

## Inputs and outputs (overview)

DEPSim is largely driven by text-based input files. Canonical examples include:
- `SimFile.inp`: selects aircraft model folder, case file, command file, output options, and CHARM coupling switches
- `PSUDEPSimInputData.txt` (aircraft parameters): defines aircraft mass properties, component definitions (rotors/wings/tails), motor models, mixers, trim and control settings
- CHARM input files (if coupling is enabled)
- Case file and command file describing trims, sweeps, maneuvers, and run options

Outputs typically include:
- time histories in binary and/or CSV formats
- logs
- trim state vectors
- (optionally) linear models (A/B matrices) from uncoupled or coupled runs

See `docs/io-spec.md` for a public, interface-level description.

## Accessing DEPSim (restricted distribution)

DEPSim itself is distributed under restrictions (e.g., third-party/proprietary dependencies, institutional agreements, sponsor terms, or export controls).  
If you believe you are eligible for access through your institution/project and need to run DEPSim, open an issue titled **“Request access”** with:
- affiliation and intended use
- confirmation you have (or can obtain) the required licenses/permissions
- whether you need CHARM coupling or PSUDEPSim-only workflows

We will reply with the appropriate process (which may include NDA or institutional verification).

## Citation

If you use DEPSim in academic work, cite the relevant DEPSim publications listed in `CITATION.cff`.

## Disclaimer

This repository documents concepts and file/interface roles. It is not an official distribution channel for DEPSim.