---
layout: default
title: 'Transport, partitioning, and response time'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [**Modules**](index.md) · [Labs](../labs/index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Modules](index.md) / Transport, partitioning, and response time

**Module 03 of 18**

<!-- course-navigation:end -->

# 03. Transport, partitioning, and response time

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Learning outcomes](#section-learning-outcomes)
- [Follow one molecule through the system](#section-follow-one-molecule-through-the-system)
- [Conservation comes before fitting](#section-conservation-comes-before-fitting)
- [Diffusion: motion down a concentration gradient](#section-diffusion-motion-down-a-concentration-gradient)
- [Convection and electromigration](#section-convection-and-electromigration)
- [Partitioning across a gas/liquid interface](#section-partitioning-across-a-gas-liquid-interface)
- [Ideal diffusion-limited current after a potential step](#section-ideal-diffusion-limited-current-after-a-potential-step)
- [Resistances to mass transfer](#section-resistances-to-mass-transfer)
- [Adsorption and memory](#section-adsorption-and-memory)
- [Design decision carried forward](#section-design-decision-carried-forward)
- [Problems and worked answers](#section-problems-and-worked-answers)
- [Further study](#section-further-study)

</details>
<!-- course-toc:end -->

**Level:** undergraduate engineering. **Suggested effort:** 6–8 hours. **Prerequisites:** Modules 01–02; derivatives and simple differential equations.

<a id="section-learning-outcomes"></a>

## Learning outcomes

You will construct a material balance; distinguish diffusion, convection, and electromigration; translate between gas and liquid concentrations without mixing Henry-law conventions; estimate response times; derive an ideal diffusion-current response; and recognize when sampling hardware dominates the apparent sensor dynamics.

<a id="section-follow-one-molecule-through-the-system"></a>

## Follow one molecule through the system

A molecule released into air has no obligation to arrive promptly at a sensor. It travels with the gas, undergoes random thermal motion, encounters walls, and may enter a liquid film. Within the film it can diffuse, adsorb, react, or return to the gas. The electrical output therefore reflects a history of delivery and interaction.

A useful conceptual pathway is:

```text
Bulk gas
  → inlet and connecting volume
  → gas boundary layer
  → gas/liquid interface
  → liquid film
  → electrode interface
  → electrical record
```

Each arrow can impose delay or loss. The pathway also works in reverse during recovery. A material that strongly accumulates a compound can improve the amount present near the electrode but can retain it long after the external concentration falls. Sensitivity and recovery time can therefore compete.

<a id="section-conservation-comes-before-fitting"></a>

## Conservation comes before fitting

For a defined control volume, write accumulation as inflow minus outflow plus generation. For a well-mixed chamber of fixed volume `V`, equal inlet/outlet volumetric flow `Q`, and no wall loss or reaction:

```text
V dc/dt = Q(c_in - c)
tau_chamber = V/Q
```

`c` is amount concentration, `V` is in m³, and `Q` is actual volumetric flow in m³/s at chamber conditions. A standard-volume flow reported by a mass-flow controller must be converted if its reference temperature and pressure differ.

For a step from zero to constant `c_in`:

```text
c(t)/c_in = 1 - exp(-t/tau_chamber)
t90 = ln(10) tau_chamber ≈ 2.303 tau_chamber
```

This is a chamber model, not a universal sensor model. A long tube with nearly plug flow can introduce an approximate transport delay. A real chamber may contain stagnant regions or short-circuit paths. Measure the impulse or step response of the sampling path before attributing its dynamics to a sensing material.

### Worked example 1: A fast sensor in a slow chamber

Take `V = 5 mL` and `Q = 100 mL/min`. Then `tau = 0.050 min = 3.0 s`, and `t90 = 6.91 s`. An electrode that responds internally in 0.1 s cannot make the chamber concentration reach its final value faster.

If the sensor itself has a 2 s first-order time constant, the two stages form a cascade. Its total step response is not a single exponential with an exact time constant of 5 s. For distinct time constants `tau_1` and `tau_2`, the normalized response is:

```text
y(t) = 1 - [tau_1 exp(-t/tau_1) - tau_2 exp(-t/tau_2)]
             /(tau_1 - tau_2)
```

For `tau_1 = 3 s` and `tau_2 = 2 s`, `y(10 s) ≈ 0.9065`. The combined 90% response is near 9.8 s. Cascaded dynamics can conceal a material improvement unless the flow path is characterized independently.

<a id="section-diffusion-motion-down-a-concentration-gradient"></a>

## Diffusion: motion down a concentration gradient

Fick's first law in one dimension is:

```text
J = -D dc/dx
```

`J` is molar flux in mol/(m² s), `D` is diffusion coefficient in m²/s, and `dc/dx` is in mol/m⁴. The negative sign means that the net flux points down the concentration gradient. Random molecular motion occurs in both directions; the gradient creates an imbalance.

Combining this constitutive relation with conservation and constant `D` yields Fick's second law:

```text
partial c/partial t = D partial²c/partial x²
```

Boundary conditions are essential. Is the outer edge held at a fixed concentration? Is the electrode a perfect sink? Is the film sealed? Does the surface react at a finite rate? The same differential equation produces very different signals under different boundary conditions.

The dimensional timescale for diffusion across a length `L` is:

```text
tau_D ~ L²/D
```

The numerical prefactor depends on geometry and how response time is defined. Use the scaling to compare designs, not as an exact `t90` formula.

### Worked example 2: Film thickness is powerful

Let `D = 1 × 10^-10 m²/s`, an illustrative slow-liquid value. For `L = 10 µm`, the diffusion timescale is `1 s`. For `L = 100 µm`, it is `100 s`. A tenfold increase in thickness causes a hundredfold increase in this timescale.

If the film also increases capacity tenfold, the design tradeoff becomes visible: more storage does not necessarily provide faster or more useful sensing. Thickness variation across a manufactured surface can produce a distribution of relaxation times even when the chemistry is identical.

<a id="section-convection-and-electromigration"></a>

## Convection and electromigration

Fluid motion carries dissolved or gaseous material. A dilute-solution flux expression for a species of charge number `z` is:

```text
J = -D grad(c) - (z F D/RT)c grad(phi) + c u
      diffusion      electromigration       convection
```

`u` is fluid velocity in m/s. This Nernst–Planck form uses assumptions about dilute behavior and mobility. Concentrated electrolytes can require activity gradients and coupled transport descriptions. Neutral VOC molecules have `z = 0`, so the direct electromigration term vanishes for them. Electric fields may still change their environment or influence charged intermediates.

The Péclet number compares convection with diffusion over a specified length:

```text
Pe = U L/D
```

A large `Pe` along a channel means axial transport is mostly convective; it does not mean diffusion across a thin boundary layer is irrelevant. Define the direction and length scale before using a dimensionless number. The official [COMSOL electrochemistry model documentation](https://doc.comsol.com/6.4/doc/com.comsol.help.echem/ElectrochemistryModuleUsersGuide.pdf) provides examples of coupling ionic transport and electrode boundary conditions.

<a id="section-partitioning-across-a-gas-liquid-interface"></a>

## Partitioning across a gas/liquid interface

At equilibrium, a dilute gas species can have a concentration in a liquid different from its concentration in the gas. One explicit Henry-law convention is:

```text
c_liquid = H_s^cp p_A
H_s^cp units: mol/(m³ Pa)
```

Combining this with `c_gas = p_A/(RT)` gives a dimensionless concentration ratio:

```text
K_lg = c_liquid/c_gas = H_s^cp RT
```

Other publications use an inverse constant or a different concentration basis. Never copy a number labeled “Henry constant” without its equation and units. [Sander's 2023 compilation](https://acp.copernicus.org/articles/23/10901/2023/) supplies a consistent water-solvent convention and references to measurements. It does not supply universal values for other solvents or ionic liquids.

### Worked example 3: Two phases, one partial pressure

For a hypothetical solute at 298.15 K, let `H_s^cp = 2.0 × 10^-3 mol/(m³ Pa)` and `p_A = 0.10 Pa`:

```text
c_liquid = 2.0 × 10^-4 mol/m³
c_gas = 0.10/(8.314462618 × 298.15)
      = 4.034 × 10^-5 mol/m³
K_lg = 4.958
```

The liquid concentration is about five times the gas concentration on the same mol/m³ basis. This statement concerns equilibrium concentration, not rate, selectivity in a mixture, or available electroactive fraction. Strong equilibrium partitioning can coexist with slow arrival.

At low concentration, this linear relation can be useful. At higher loading, chemical reaction, association, saturation, or nonideal behavior may invalidate it. If the material changes composition as it absorbs water, the partition coefficient itself can change during an experiment.

<a id="section-ideal-diffusion-limited-current-after-a-potential-step"></a>

## Ideal diffusion-limited current after a potential step

Consider a planar electrode contacting a semi-infinite, initially uniform solution of an electroactive species. Assume excess supporting electrolyte suppresses migration, convection is absent, the potential step makes the electrode a perfect sink, and diffusion coefficient and area are constant. Solving Fick's equation under these conditions gives the magnitude of the Cottrell current:

```text
|i(t)| = n F A c_bulk sqrt[D/(pi t)]
```

The formal result is singular at `t = 0`; real instruments, charge-transfer kinetics, and double-layer charging prevent that idealized infinite current from being measured. The [IUPAC Cottrell entry](https://goldbook.iupac.org/terms/view/09069/html) states the boundary conditions explicitly. Use them as a checklist before fitting `i` against `t^-1/2`.

Take `n = 1`, `A = 1 mm²`, `c_bulk = 1 mol/m³`, and `D = 10^-9 m²/s`. At `t = 1 s`, the calculated current is `1.72 µA`. At `t = 4 s`, it is `0.861 µA`. A square-root decay does not imply that the total amount reacted has stopped increasing: the integrated charge grows approximately as `sqrt(t)` in this ideal model.

<a id="section-resistances-to-mass-transfer"></a>

## Resistances to mass transfer

For a simple one-dimensional, steady diffusion film of thickness `L`, with concentration drop `Delta c`:

```text
J ≈ (D/L) Delta c = k_m Delta c
k_m = D/L       [m/s]
```

Gas-side transfer, interface partitioning, liquid transport, and reaction can all contribute. Resistances can sometimes be added after expressing every driving force on the same concentration basis. Adding a gas-side resistance to a liquid-side resistance without accounting for partitioning is dimensionally and physically misleading.

A useful experiment varies one transport condition. If response changes strongly with flow at fixed composition, gas delivery may matter. If response time scales with film thickness squared, diffusion is a candidate explanation. Neither observation alone proves a unique mechanism; adsorption kinetics, thermal effects, or morphology changes may correlate with the manipulated variable.

<a id="section-adsorption-and-memory"></a>

## Adsorption and memory

For a simple reversible surface population with fractional occupancy `theta`:

```text
dtheta/dt = k_ads c (1 - theta) - k_des theta
theta_eq = K c/(1 + K c),  K = k_ads/k_des
```

At low `Kc`, occupancy is approximately linear in concentration. At high `Kc`, it saturates. On removing the analyte, this model predicts decay with a time constant `1/k_des`. Surface heterogeneity, competitive adsorption, and irreversible fouling can produce more complex behavior.

A downstream algorithm cannot fully reconstruct concentration information that has been lost through unknown irreversible retention. Include blanks after strong exposures, randomize presentation order, and record the recovery trajectory. A sensor with excellent single-exposure separation can fail when memory from the previous sample dominates the next one.

<a id="section-design-decision-carried-forward"></a>

## Design decision carried forward

**Decision:** choose a sample-path volume, flow regime, and film transport scale consistent with the required response and recovery times. **Criteria:** chamber turnover, diffusion time, partitioning, wall loss, and analyte consumption. **Evidence:** a material balance, a dimensional timescale table, and a proposed independent measurement of the sampling-path response.

**Artifact:** a transport budget assigning a delay or response contribution to each stage, with assumptions and uncertainty. Include a blank-flush test and a recovery criterion. Carry this budget into the [design studio](../design-studio.md) before choosing an acquisition rate; rapid digitization cannot undo slow unknown transport.

<a id="section-problems-and-worked-answers"></a>

## Problems and worked answers

1. **Thickness scaling.** A film is reduced from 30 to 15 µm without changing `D`. What happens to the characteristic diffusion time?

   **Answer:** it becomes one quarter as large because time scales with length squared. Actual response may remain limited by another process.

2. **Chamber flushing.** How much time does the ideal well-mixed chamber require to reduce an initial concentration to 1% after switching to clean gas?

   **Answer:** `t = ln(100) V/Q = 4.605 V/Q`. This assumes no continuing release from walls or the sensor.

3. **Partition convention.** A source reports `p_A/c_liquid = 500 Pa m³/mol`. Express the equivalent `H_s^cp`.

   **Answer:** `H_s^cp = 1/500 = 0.002 mol/(m³ Pa)`. The reciprocal is valid only because the numerator and denominator definitions match.

4. **Cottrell critique.** A 100 µm finite film is analyzed for several hours using a semi-infinite planar model. What should be checked?

   **Answer:** compare `sqrt(Dt)` with film thickness and electrode dimensions; evaluate depletion, replenishment, convection, charging, and drift. Once diffusion explores the boundaries, the semi-infinite assumption fails.

<a id="section-further-study"></a>

## Further study

Consult [Sander's conversion tables](https://henry.mpch-mainz.gwdg.de/henry/convert.html?Htype=HscpSI&Hval=1) for a worked example of convention management, and [IUPAC's electroanalytical terminology](https://doi.org/10.1515/pac-2018-0109) for formal transport-current definitions. The [foundations bibliography](../references/fundamentals.md) records the scope of each source.

<!-- course-footer:start -->
---

[Previous: Thermodynamics, redox, and electrode potential](02-thermodynamics-and-redox.md) · [All modules](index.md) · [Next: Electrode interfaces and electrical transduction](04-electrode-interfaces.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
