# Aerodynamic devices on a truck (without trailer)

**Academic project — Politecnico di Milano — 2025/2026**
Course: Aerodynamics of Transport Vehicles (Prof. P. Schito, Prof. A. Zanotti).
Group work (4 authors). 

## Summary

A steady-state RANS CFD study in OpenFOAM of drag-reduction devices on a
heavy-duty truck tractor operating **without its trailer** — a road-vehicle drag
problem centred on bluff-body flow and wake management. Each device was assessed
individually and in combination to find a configuration that lowers drag. The
main result: a straight **boat tail reduced drag by 7.18%** relative to the bare
cabin, while the conventional **roof fairing proved detrimental (+6%)**, driving
the conclusion that recovering base pressure is more effective than chasing wake
reduction on a tractor without trailer.

## Setup & method

- Simplified CAD (CATIA V5) from a European-type truck reference; 6 × 2.4 × 4 m,
  frontal area 4.52 m².
- OpenFOAM, steady incompressible **RANS** (`simpleFoam`), **k–ω SST** turbulence
  model with wall functions.
- U∞ = 20 m/s (Ma ≈ 0.06, Re ≈ 6.6 × 10⁶); half domain via symmetry; moving-ground
  boundary condition; `potentialFoam` initialisation; C_D averaged over the last
  200 iterations to handle bluff-body unsteadiness.

## Mesh & validation

- `blockMesh` + `snappyHexMesh`, five refinement regions (max level 8), extra
  refinement in separation zones, and a tyre contact patch.
- **Farfield-independence** study (four domain sizes) and **grid-convergence**
  study (0.8M → 8.2M cells) → a 3.6M-cell reference mesh balancing accuracy and cost.

## Device study & results

- Baseline (bare cabin) C_D = 0.384.
- **Roof fairing:** +6% drag — the main detriment, thickening the wake.
- **Side fairings:** slightly beneficial; act like winglets, limiting the roof
  deflector's tip vortices. Replacing mirrors with **MirrorCams** (NACA0012 arm)
  gave −1.62%.
- **Roof deflector angle sweep (0°–20°):** a straight (0°) deflector is best;
  drag rises with angle as tip vortices grow and separation spreads.
- **Boat tail** (side + roof fairings at 0°): **−7.18%** vs baseline — the best
  configuration.

## Techniques

`OpenFOAM (simpleFoam)` · `RANS / k–ω SST` · `snappyHexMesh` · `farfield & grid independence`
· `CATIA V5` · `ParaView` · `MATLAB`

## Relevance to vehicle aerodynamics

Directly transferable to motorsport aero: bluff-body external aerodynamics, drag
and wake management, device evaluation, and the full RANS workflow — meshing,
turbulence modelling, mesh- and domain-independence — used to develop road- and
race-car aero packages. The winglet/tip-vortex reasoning and the base-pressure
vs wake-reduction trade-off are core aerodynamic concepts.

---

*Full report (English):* `Aerodynamic_devices_on_a_truck.pdf`
