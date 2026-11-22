---
layout: default
title: '07 · Sampling and fluidics'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [**Modules**](index.md) · [Labs](../labs/index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Modules](index.md) / 07 · Sampling and fluidics

**Module 07 of 18**

<!-- course-navigation:end -->

# 07 · Sampling and fluidics

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Learning outcomes](#section-learning-outcomes)
- [1. Specify what the sample represents](#section-1-specify-what-the-sample-represents)
- [2. Follow the mass through the system](#section-2-follow-the-mass-through-the-system)
- [3. Velocity and Reynolds number](#section-3-velocity-and-reynolds-number)
- [4. Worked example: a generic sampling line](#section-4-worked-example-a-generic-sampling-line)
- [5. Diffusion, delivery, and wall contact](#section-5-diffusion-delivery-and-wall-contact)
- [6. Worked example: chamber flushing and pulse dilution](#section-6-worked-example-chamber-flushing-and-pulse-dilution)
- [7. Build a validation plan from independent observations](#section-7-build-a-validation-plan-from-independent-observations)
- [8. Failure modes and misconceptions](#section-8-failure-modes-and-misconceptions)
- [Design decision carried forward](#section-design-decision-carried-forward)
- [9. Exercises and worked answers](#section-9-exercises-and-worked-answers)

</details>
<!-- course-toc:end -->

A sensor measures the molecules that reach its interface. Those molecules may differ from the molecules at the place and time the engineer wanted to observe. Before asking whether an electrode is sensitive, ask whether the sample is representative. A perfectly calibrated detector attached to a poorly understood inlet can produce precise measurements of the wrong gas.

**Level and time:** upper-division undergraduate; approximately 5–7 hours including exercises. **Prerequisites:** conservation of mass, ordinary differential equations, [transport and partitioning](03-transport-and-partitioning.md), and [electrochemical methods](06-electrochemical-methods.md).

<a id="section-learning-outcomes"></a>

## Learning outcomes

By the end of this module, you should be able to:

- Define a sampling measurand and distinguish it from the detector's immediate input.
- Calculate mean velocity, Reynolds number, residence time, pressure drop, and a relevant Péclet number.
- Explain why laminar flow does not guarantee rapid or uniform chemical delivery.
- Separate transport delay, mixing, wall interactions, and sensor response.
- Design a computational or bench-validation plan that can falsify a proposed inlet model.

<a id="section-1-specify-what-the-sample-represents"></a>

## 1. Specify what the sample represents

“Measure the VOC concentration” leaves essential questions unanswered. Is the desired quantity an instantaneous mole fraction at one point, a flow-weighted average through an inlet, or an average over a collection period? Is the reported value on a wet or dry basis? What pressure and temperature apply? Which analytes and interfering species matter?

For a time-varying inlet concentration `c(t)` and volumetric flow `Q(t)`, at approximately constant pressure and temperature, the collected concentration is:

```text
c_collected = integral[c(t) Q(t) dt] / integral[Q(t) dt]

c: mol m^-3
Q: m^3 s^-1
```

A high-concentration interval contributes little if almost no gas enters during it. Conversely, a brief high-flow event can dominate a bag sample. If pressure or temperature changes appreciably, replace volumetric weighting with molar-flow weighting. A notebook entry saying “sampled for one minute” cannot reconstruct this distinction.

For breath research, gas from different parts of an exhalation is not interchangeable. An apparatus should describe what fraction it measures and how that choice is verified. The [European Respiratory Society technical standard](https://doi.org/10.1183/13993003.00965-2016) is a primary professional-society resource for collection and analytical standardization; it is not a declaration that every measured breath feature has diagnostic meaning.

An engineering specification should include the sampling location, collection window, flow range, environmental range, acceptable recovery, and maximum timing error. These become requirements against which later design choices can be judged.

<a id="section-2-follow-the-mass-through-the-system"></a>

## 2. Follow the mass through the system

A useful conceptual diagram is:

```text
source field -> inlet -> tubing -> conditioning -> chamber -> electrode
                  |        |            |            |
               dilution   wall loss   selective     mixing and
                                      removal      residence time
```

Every arrow is a transport process. Every surface can store or release material. The system also has boundaries: a pressure leak can admit surrounding gas, and a polymer wall can exchange species even when the pressure seal is intact.

For a well-mixed chamber of constant volume `V`, constant flow `Q`, no wall uptake, and equal inlet and outlet flows:

```text
V dc/dt = Q(c_in - c)
tau = V/Q

For a step from zero to c_in at t = 0:
c(t) = c_in [1 - exp(-t/tau)]
t_90 = ln(10) tau ≈ 2.303 tau
```

This model follows directly from accumulation = input − output. It does not describe a plug-flow tube, whose ideal response is mostly a delay, or a chamber with stagnant regions, whose response may have several time scales. Treat the model as a testable approximation rather than a label bestowed by the enclosure drawing.

If the electrode response is another first-order process, the observed signal is the composition of both systems. Their 90% response times generally cannot simply be added. Convolution, a state-space model, or numerical integration is more reliable. A slowly decaying tail may come from the inlet rather than from irreversible electrode chemistry.

<a id="section-3-velocity-and-reynolds-number"></a>

## 3. Velocity and Reynolds number

For a circular tube with diameter `d`, cross-sectional area `A`, and mean velocity `u`:

```text
A = pi d^2/4
u = Q/A
Re = rho u d / mu

rho: gas density, kg m^-3
mu: dynamic viscosity, Pa s
Re: dimensionless
```

Reynolds number compares inertial and viscous effects. Geometry and disturbances matter as well as the number; there is no universal “laminar below X” rule covering every inlet. [NASA's Reynolds-number explanation](https://www.grc.nasa.gov/www/k-12/airplane/reynolds.html) provides the dimensionless scaling, while [OpenStax's viscosity chapter](https://openstax.org/books/university-physics-volume-1/pages/14-7-viscosity-and-turbulence) develops the straight-tube model.

In a fully developed laminar circular-tube flow, the velocity is largest at the center and zero at the wall. Thus, “laminar” does not mean all molecules travel at the same speed. Radial molecular diffusion exchanges molecules between streamlines; the resulting pulse spreading depends on both advection and diffusion.

For fully developed, incompressible, Newtonian flow through a straight circular tube:

```text
Delta_p = 128 mu L Q / (pi d^4)
```

Gas can be approximated as incompressible here when pressure changes are small relative to absolute pressure and speeds are low. Entrance effects, bends, valves, porous filters, and contractions add pressure losses not captured by this expression. The `d^-4` dependence makes diameter a powerful design variable, but reducing diameter also changes residence time, surface-to-volume ratio, and fouling susceptibility.

<a id="section-4-worked-example-a-generic-sampling-line"></a>

## 4. Worked example: a generic sampling line

The following values are invented for teaching, not a recommended device geometry. Take `L = 0.20 m`, `d = 2.0 mm`, `Q = 100 mL/min`, `rho = 1.18 kg/m^3`, and `mu = 1.85 × 10^-5 Pa s`.

```text
Q = 100 × 10^-6 / 60 = 1.667 × 10^-6 m^3/s
A = pi (0.002)^2 / 4 = 3.142 × 10^-6 m^2
u = 0.531 m/s
Re = 1.18 × 0.531 × 0.002 / (1.85 × 10^-5) = 67.7
V_tube = A L = 6.283 × 10^-7 m^3 = 0.628 mL
mean residence time = V_tube/Q = 0.377 s
Delta_p = 15.7 Pa
```

The low Reynolds number is consistent with laminar flow in this straight-tube approximation. It says nothing by itself about chemical recovery. The calculated pressure drop is small compared with atmospheric pressure, supporting the incompressible approximation for this tube segment. A restrictive filter downstream could dominate the total pressure requirement.

Now halve the diameter while keeping `Q` and `L` fixed. Velocity rises fourfold, Reynolds number doubles, residence time falls fourfold, and the ideal pressure drop rises sixteenfold. There is no single best diameter independent of the rest of the system. Students should express the tradeoff as a requirement comparison, not select the smallest available tubing.

<a id="section-5-diffusion-delivery-and-wall-contact"></a>

## 5. Diffusion, delivery, and wall contact

A Péclet number compares advective and diffusive transport over a declared length scale:

```text
Pe = u L_characteristic / D
D: molecular diffusion coefficient, m^2 s^-1
```

Always state the length scale. Using the diameter gives a different number from using the entire tube length. A large axial Péclet number means axial advection dominates axial molecular diffusion over that distance; it does not mean radial diffusion is absent.

For the example above and an illustrative gas diffusivity `D = 1 × 10^-5 m^2/s`, `Pe_d ≈ 106`. A rough radial diffusion time across radius `r = 1 mm` is `r^2/D ≈ 0.10 s`. Compare this with the `0.377 s` residence time: radial exchange can matter during passage. Such scaling is more informative than simply announcing that the inlet “has laminar flow.”

Wall interactions can delay a compound without permanently removing it. Adsorption followed by desorption creates memory; permeation can move material into or through the wall; chemical reaction can change identity. A recovery test at one concentration and duration may miss nonlinear saturation or long tails. [Beauchamp et al.](https://doi.org/10.1088/1752-7155/2/4/046001) experimentally observed compound-dependent storage behavior in gas-sampling bags, illustrating why transport materials need chemical as well as mechanical characterization.

<a id="section-6-worked-example-chamber-flushing-and-pulse-dilution"></a>

## 6. Worked example: chamber flushing and pulse dilution

Suppose a generic chamber has `V = 4.0 mL` and receives `Q = 80 mL/min`. Its ideal mixing time constant is:

```text
tau = 4/80 min = 3.0 s
t_90 = 6.91 s
t_99 = ln(100) tau = 13.82 s
```

If a one-second concentration pulse enters an initially blank chamber, the chamber concentration at the pulse's end is only:

```text
c(1 s)/c_in = 1 - exp(-1/3) = 0.283
```

After the pulse, that concentration decays with the same time constant in this reversible model. A fast electronic sampling rate cannot recover an undiluted peak that the chamber never delivered. A deconvolution algorithm may estimate the input, but it amplifies noise and depends on a valid transfer model.

This distinction matters when comparing sensor papers. One reported response time may start at a valve command; another may start when reference gas actually reaches the sensing surface. Both are interpretable only if their timing conventions are explicit.

<a id="section-7-build-a-validation-plan-from-independent-observations"></a>

## 7. Build a validation plan from independent observations

For a computational exercise, simulate a plug delay followed by a mixed chamber and a first-order detector. Vary each parameter separately. Plot arrival time, peak attenuation, and recovery tail. Then ask which parameters can be uniquely inferred from one measured output. Several combinations can produce similar traces.

For a supervised institutional bench study, a design plan should specify an independently characterized reference stream and an independent downstream reference measurement. Students need not generate gases themselves. Include a bypass path to separate inlet losses from detector behavior, a system blank, repeated concentration steps, and test orders that reveal carryover. An established atmospheric-method example is [EPA Method TO-15A](https://www.epa.gov/amtic/compendium-methods-determination-toxic-organic-compounds-ambient-air), which connects sampling-container performance with analytical quality control. Its scope is canister sampling and GC–MS, not automatic qualification of an electrochemical device.

Timing must be measured, not guessed from cable length. Record valve command time, flow stabilization, reference arrival, and sensor acquisition time. If a sampling pump changes flow as a filter loads, the previously estimated residence time changes too. Log enough context to detect that change.

<a id="section-8-failure-modes-and-misconceptions"></a>

## 8. Failure modes and misconceptions

| Observation | Plausible explanation | Discriminating observation |
| --- | --- | --- |
| Slow rise and fast recovery | Concentration-dependent adsorption or nonlinear sensor response | Compare bypass and complete-path responses |
| Fast rise and long tail | Dead zones, desorption, or detector recovery | Change tubing length independently of detector |
| Response changes with flow | Delivery limitation or pressure-dependent behavior | Measure actual flow and reference concentration |
| Stable blank, low recovery | Selective sample loss | Compare several chemical classes |
| Identical timing for all channels | Shared chamber dynamics dominate | Independently characterize channel chemistry |

A clean-looking CAD model is not evidence of representative sampling. A low Reynolds number is not proof of uniform delivery. A nominal flow specification is not an actual flow measurement. Finally, a gas-phase analyte and an aerosol particle carrying that analyte are different sampling problems; conditioning may alter their relative contributions.

<a id="section-design-decision-carried-forward"></a>

## Design decision carried forward

For the [design studio](../design-studio.md), analyze one independently documented sampling experiment or one synthetic flow model. Compare tube diameter, length, volume, and flow range using pressure drop, residence time, and surface contact. The deliverable is a conceptual diagram, a mass balance, and a simulated transport response with explicit boundary conditions. State what would establish delivered concentration and arrival time independently. This can remain a stand-alone study; do not prescribe a collection interface or combine subsystems without a project-specific justification.

<a id="section-9-exercises-and-worked-answers"></a>

## 9. Exercises and worked answers

1. **Flow weighting.** A stream is at 10 units for 20 s with flow 50 mL/min, then at 30 units for 10 s with flow 100 mL/min. What concentration enters the combined collection? **Answer:** both intervals contribute the same volume, so the result is 20 units. The time average is 16.7 units and answers a different question.
2. **Flushing specification.** A 2 mL ideal mixed chamber operates at 60 mL/min. How long until 95% of a step is reached? **Answer:** `tau = 2 s`; `t_95 = -tau ln(0.05) = 5.99 s`.
3. **Pressure tradeoff.** Double the tube length and halve its diameter at fixed flow. **Answer:** the ideal pressure drop multiplies by `2 × 2^4 = 32`; tube volume becomes half its original value.
4. **Model critique.** A measured step has a long tail that remains after the chamber volume is halved. Does that prove electrode memory? **Answer:** no. Tubing sorption, stagnant connectors, and filtering can also produce the tail. Change one subsystem at a time and use independent measurements.
5. **Design deliverable.** Write a one-page sampling specification with a measurand, time basis, recovery limits, and falsifiable flow model. **Answer criterion:** each numerical requirement must connect to an observation or decision, and every model must list its assumptions.

<!-- course-footer:start -->
---

[Previous: Electrochemical methods and model validation](06-electrochemical-methods.md) · [All modules](index.md) · [Next: 08 · Humidity, filtration, and conditioning](08-humidity-filtration-and-conditioning.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
