# I/O Specification (Public Interface-Level Description)

This document describes the *roles* of major DEPSim input/output files without distributing restricted implementations.

## Key input files

### 1) `SimFile.inp` — simulator settings
Purpose:
- selects operational flags and which aircraft/case/command files to load
- selects output formatting and decimation options
- toggles CHARM coupling switches conceptually (if available to you)

Common fields (examples, not exhaustive):
- operational mode / command input mode
- CHARM enable + connectivity toggles
- output type (binary / CSV options) and decimation rate
- aircraft model folder name
- aircraft parameter file name
- case file name and command file name
- output/log file names

[IMAGE PLACEHOLDER: annotated snippet of SimFile.inp]

### 2) Aircraft parameter file (often `PSUDEPSimInputData.txt`)
Purpose:
- defines aircraft mass properties, CG, components (rotors/wings/tails/fuselage), motors, mixers, trim parameters, and control parameters.

Typical content:
- aircraft-level constants (weight, inertia, CG, component counts)
- per-rotor definitions (location/orientation, RPM, flapping model parameters, inflow model choices)
- wing/tail definitions (geometry, lookup tables, control surfaces)
- fuselage model selection
- motor model selection and parameters
- mixer definitions mapping pilot/control axes to effectors
- trim schedule parameters and control scheduling parameters

[IMAGE PLACEHOLDER: annotated snippet of component definition]

### 3) Case input file
Purpose:
- defines what the simulator should *do* for a run (trim commands, sweeps, linearization, controller design toggles, simulation type).

[IMAGE PLACEHOLDER: case file example structure]

### 4) Command input file
Purpose:
- defines time histories of pilot/autopilot commands for maneuvers and excitations.

[IMAGE PLACEHOLDER: command timeline diagram]

### 5) CHARM input files (if coupling is enabled)
Purpose:
- define rotor/lifting-surface geometry, wake model settings, run characteristics, etc., as required by CHARM.

## Key output files (typical)

### Simulation results (`HeloSimOutXXX.bin/.csv`)
Purpose:
- stores time histories of states, controls, forces/moments, and other internal signals.
- may be produced as binary and/or converted to CSV depending on settings.

### Logs
Purpose:
- record run metadata, warnings, and error codes.

### Trim state vectors and linear models
Purpose:
- store trim solutions and (optionally) A/B matrices from linearization workflows.

[IMAGE PLACEHOLDER: “outputs produced by workflow stage” flowchart]