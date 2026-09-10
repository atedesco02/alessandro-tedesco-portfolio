# Rollover analysis of a truck (crosswind)

**Academic project — Politecnico di Milano — 2024/2025**
Course: Wind Engineering (Prof. D. Rocchi). Group work (4 authors).

## Summary

A MATLAB vehicle-dynamics study of the **crosswind-induced rollover** of a
truck-and-trailer subjected to turbulent lateral wind. Rollover is assessed with
a conservative criterion — a wheel's normal reaction dropping below 10% of its
static load. The work covers straight-line rollover speed across wind and road
conditions, the influence of mass distribution and roll-stiffness balance, and
the driver's effect during lane-change manoeuvres modelled with a PID controller.

## Model & method

- Dynamic model driven by six turbulent wind time histories (mean speed 25–30 m/s,
  turbulence intensity 7–25%, integral length 150 m), with aerodynamic loads set
  by the vehicle–wind relative speed.
- Rollover criterion: any wheel reaction < 10% of its static load.
- Driver modelled as a **PID controller** tracking a reference path for the
  lane-change studies.

## Straight-line rollover & road conditions

- Rollover speeds ranged from ~235 down to ~110 km/h across the wind histories;
  the most turbulent case overturned the vehicle even at rest.
- Higher mean wind or turbulence intensity lowers the rollover speed.
- Counter-intuitively, a **more slippery road raises the rollover speed** — with
  less grip the truck slides sideways rather than pivoting — but it also drifts
  further off the reference path, a distinct hazard.

## Load ratio & roll-stiffness distribution

- **Load ratio λ** (trailer mass and CG height) shifts the critical wheel between
  the front-right and rear-right; higher λ loads all wheels more and is safer.
- **Roll-stiffness distribution τ** (front-axle roll stiffness as a fraction of
  the total) trades load between the front-right and rear-right wheels.
- An **optimal τ** exists for each λ that balances front and rear loads; the
  analysis showed the vehicle is designed for λ > 0.4, below which no optimum exists.

## Driver & lane-change analysis

- Single lane change (3.75 m): two wheel-load peaks, the exit peak the more
  critical (inertia and aero loads align); shorter manoeuvres lower the rollover
  speed via higher lateral acceleration.
- PID driver tuning: proportional gain ≈ 0.5 and derivative gain ≈ 0.05 give a
  stable, well-damped response.
- Double lane change: minimum load ratio mapped against the spacing between the
  two switches, identifying the most critical timing.

## Relevance to vehicle dynamics & motorsport

Complements the aerodynamics and CFD work with the vehicle-dynamics and control
side: lateral dynamics, weight transfer, roll-stiffness balance and closed-loop
driver modelling. The τ (roll-stiffness distribution) and load-transfer analysis
maps directly onto race-car setup, where front/rear anti-roll balance governs
handling.

## Techniques

`MATLAB` · `vehicle dynamics modelling` · `load transfer & roll stiffness` · `turbulent wind time histories`
· `PID / closed-loop driver model` · `lateral stability analysis`

---

*Full report (English):* `Rollover_analysis_of_a_truck.pdf`
