# CFD analysis of a 3D combustor

**MSc course project — Politecnico di Milano — 2025/2026**
Advisor: Prof. F. Piscaglia; co-advisor: Prof. F. Ghioldi. Individual project.

## Summary

A transient reacting-flow CFD study in **OpenFOAM v13** of a non-premixed
**n-Heptane** combustor, with liquid fuel injected as a **Lagrangian spray** onto
a V-shaped bluff-body flame holder. A two-stage methodology was used: a cold-flow
precursor to initialise the domain, then a fully reactive hot-flow run with
evaporation, auto-ignition and combustion. The study captures the coupling
between bluff-body aerodynamics, spray evaporation and combustion — the
recirculation zone behind the splitter anchors the flame and prevents blow-off.

## Method

- OpenFOAM v13, `multicomponentFluid` solver, transient **PIMPLE**
  (momentumPredictor deactivated), non-reflective `waveTransmissive` outlet,
  `hePsiThermo` energy model.
- Two-stage run: cold-flow precursor (spray off, 905 K / 10 m/s inlet air) →
  reactive hot-flow mapped from the precursor's final time step.

## Mesh

- `blockMesh` background + `snappyHexMesh` with cylindrical refinement following
  the spray/flame region (~401k cells); `checkMesh` skewness 1.1, max
  non-orthogonality ≈ 65°.
- y⁺ verification (min 0.36, max 75, domain-averaged ≈ 16) against the RANS wall
  functions.

## Combustion & spray modelling

- Non-premixed n-Heptane, single-step reaction
  (C₇H₁₆ + 11 O₂ → 7 CO₂ + 8 H₂O, stoichiometric A/F ≈ 15.1); **partially stirred
  reactor (PaSR)** combustion model; `seulex` implicit ODE solver for the stiff
  chemistry.
- Lagrangian `reactingCloud`: 95 mg injected on a half-sine profile,
  500k parcels/s, Reitz–Diwakar breakup; Sauter mean diameter ≈ 105 µm, droplets
  fully evaporating before wall impingement (no wall-film model needed).

## Key results

- Flame anchored in the splitter's recirculation zone (negative centreline
  velocity), sustaining combustion against the high-velocity inflow — no blow-off.
- Flame front tracked via the stoichiometric A/F iso-surface; specular O₂/CO₂
  mass fractions confirm the reaction; peak temperatures ≈ 2800 K (adiabatic,
  single-step).
- Max Mach ≈ 0.05 → incompressible regime; density changes driven by temperature,
  not pressure.
- Bluff-body wake shows the characteristic M-shaped velocity profile, recovering
  downstream through turbulent mixing.

## What it demonstrates

Advanced OpenFOAM multiphysics — transient, reacting, multiphase (Lagrangian
spray) simulation with stiff chemistry — on top of the meshing, turbulence-modelling
and post-processing workflow shared with external-aero CFD. The bluff-body wake,
recirculation and vortex-shedding analysis is directly aerodynamics-relevant; the
combustion side shows CFD depth beyond aerodynamics.

## Techniques

`OpenFOAM v13` · `transient reacting RANS` · `PIMPLE` · `Lagrangian spray (reactingCloud)`
· `PaSR combustion` · `stiff-chemistry ODE (seulex)` · `snappyHexMesh` · `ParaView` · `MATLAB`

---

*Full report (English):* `3D_Combustor.pdf`
