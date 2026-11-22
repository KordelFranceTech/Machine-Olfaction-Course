---
layout: default
title: 'Thermodynamics, redox, and electrode potential'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [**Modules**](index.md) · [Labs](../labs/index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Modules](index.md) / Thermodynamics, redox, and electrode potential

**Module 02 of 18**

<!-- course-navigation:end -->

# 02. Thermodynamics, redox, and electrode potential

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Learning outcomes](#section-learning-outcomes)
- [An electrode is an adjustable electron reservoir](#section-an-electrode-is-an-adjustable-electron-reservoir)
- [Chemical and electrochemical potential](#section-chemical-and-electrochemical-potential)
- [Deriving the Nernst relation](#section-deriving-the-nernst-relation)
- [Potential exists between two points](#section-potential-exists-between-two-points)
- [Overpotential and kinetic limitation](#section-overpotential-and-kinetic-limitation)
- [Tafel behavior is a conditional approximation](#section-tafel-behavior-is-a-conditional-approximation)
- [Ohmic drop and what the potentiostat actually controls](#section-ohmic-drop-and-what-the-potentiostat-actually-controls)
- [Coupling thermodynamics, kinetics, and transport](#section-coupling-thermodynamics-kinetics-and-transport)
- [Design decision carried forward](#section-design-decision-carried-forward)
- [Problems and worked answers](#section-problems-and-worked-answers)
- [Further study](#section-further-study)

</details>
<!-- course-toc:end -->

**Level:** undergraduate engineering. **Suggested effort:** 6–8 hours. **Prerequisites:** Module 01; logarithms; introductory Gibbs energy and electric circuits.

<a id="section-learning-outcomes"></a>

## Learning outcomes

You will relate chemical potential to electrical work; use the Nernst equation with an explicit reaction and reference; distinguish equilibrium, kinetic, and transport effects; calculate simple Butler–Volmer behavior; and identify errors caused by reference drift and uncompensated resistance.

<a id="section-an-electrode-is-an-adjustable-electron-reservoir"></a>

## An electrode is an adjustable electron reservoir

In a metal wire, electrons carry current. In an electrolyte, ions carry much of the current. An electrode interface connects these worlds. Electrons can cross the interface through a chemical reaction, or charge can accumulate without a sustained electron-transfer reaction. The second mechanism is explored in Module 04.

Consider a generic dissolved couple:

```text
Ox + n e^- ⇌ Red
```

The symbols represent oxidized and reduced forms, not a recommended sensing chemistry. A reduction accepts electrons; oxidation releases them. Changing electrode potential changes the energetic conditions for transfer. It does not guarantee that a reaction proceeds rapidly, selectively, reversibly, or without competition.

Three separate questions are needed. Is a process thermodynamically favorable? Is electron transfer fast enough? Can reactant reach the electrode at the required rate? A large driving force answers only the first question. In sensing, a plateau current often reflects supply of molecules rather than a ceiling on the electrical capability of the instrument.

For a structured course reference, see [Bard, Faulkner, and White, *Electrochemical Methods*, third edition](https://www.wiley.com/en-us/electrochemical-methods-fundamentals-and-applications-3rd-edition-p-9781119334064). The publisher provides a first-chapter excerpt; the complete textbook is a library or purchase resource.

<a id="section-chemical-and-electrochemical-potential"></a>

## Chemical and electrochemical potential

Chemical potential is the change in Gibbs energy associated with adding a small amount of a species under specified conditions. For a simple activity convention:

```text
mu_i = mu_i° + RT ln(a_i)
mu_tilde_i = mu_i + z_i F phi
```

`mu_i` and `mu_tilde_i` are in J/mol; `z_i` is signed ionic charge number; `F ≈ 96485.33212 C/mol`; `phi` is electric potential in V. The product `C/mol × J/C` has units of J/mol. This unit check explains why electrical and chemical driving forces can appear in one expression. IUPAC defines [electrochemical potential](https://goldbook.iupac.org/terms/view/E01945) in terms of the partial molar Gibbs energy in a specified phase.

For a complete reversible cell transferring `n` electrons per reaction event written in molar form:

```text
Delta_r G = -n F E_cell
```

The reaction equation matters. Multiplying every coefficient by two doubles `n` and `Delta_r G`, but leaves the equilibrium cell voltage unchanged. Do not confuse extensive reaction energy with the intensive potential difference.

<a id="section-deriving-the-nernst-relation"></a>

## Deriving the Nernst relation

For a reaction with reaction quotient `Q`, combine `Delta_r G = Delta_r G° + RT ln Q` with electrical work:

```text
-n F E_eq = -n F E° + RT ln Q
E_eq = E° - (RT/nF) ln Q
```

For `Ox + n e^- ⇌ Red`, with the electron contribution represented by electrode potential:

```text
E_eq = E° + (RT/nF) ln(a_Ox/a_Red)
```

At `298.15 K`, one decade in the activity ratio changes potential by about `59.16/n mV`. That familiar slope applies to this defined equilibrium model; it is not a universal sensor sensitivity. The [IUPAC Nernst entry](https://goldbook.iupac.org/terms/view/09068) also distinguishes a standard potential from a formal potential adapted to a particular chemical environment.

### Worked example 1: An activity ratio changes

A one-electron couple has `a_Ox/a_Red = 100`. At 298.15 K:

```text
E_eq - E° = (0.0256926 V) ln(100)
           = 0.1183 V
```

If the ratio falls to 10, the potential becomes `E° + 0.05916 V`. The change is minus 59.16 mV. No absolute numerical potential can be reported until `E°` and its reference scale are specified.

For a two-electron reaction with the same quotient structure, each decade would contribute about 29.58 mV. Real multistep reactions can involve proton coupling, intermediates, or changing activities; the simple slope must not be applied without the balanced reaction.

<a id="section-potential-exists-between-two-points"></a>

## Potential exists between two points

A statement such as “the electrode was held at 0.3 V” is incomplete. Relative to which electrode, in which electrolyte, at what temperature? A reference electrode provides a reproducible potential against which a working electrode can be controlled or measured. Its composition and junction environment are part of the experiment.

An ideal reference draws negligible current. Passing substantial current through it changes interfacial conditions and can move its potential. A three-electrode arrangement therefore separates functions:

```text
Working electrode: reaction or interfacial response of interest
Reference electrode: potential observation with negligible current
Counter electrode: completes the current path
```

A potentiostat adjusts the counter electrode so that the measured working-to-reference potential follows the requested value, subject to its voltage and current limits. A two-electrode cell controls a total cell voltage that includes both interfaces and the electrolyte. It may be appropriate, but its voltage cannot automatically be interpreted as one working-electrode potential.

Miniaturized quasi-reference electrodes may be useful but require stability checks. A drifting reference can make a perfectly stable surface appear to have a changing reaction potential. Recording a reference check before and after an experiment can expose this failure mode. Formal definitions of electrode arrangements and electroanalytical quantities are available in [Pingarrón and colleagues' IUPAC recommendations](https://doi.org/10.1515/pac-2018-0109).

<a id="section-overpotential-and-kinetic-limitation"></a>

## Overpotential and kinetic limitation

Overpotential is the difference between the interfacial electrode potential and the equilibrium potential for the reaction under the relevant local conditions:

```text
eta = E_interface - E_eq
```

A common elementary kinetic model is Butler–Volmer. For a simple reaction with fixed surface activities and an anodic-positive sign convention:

```text
j = j0 [exp(alpha_a nF eta/RT) - exp(-alpha_c nF eta/RT)]
```

`j` is current density in A/m²; `j0` is exchange current density; `alpha_a` and `alpha_c` are transfer coefficients. In the simplest one-step representation their sum is one. Real multistep reactions need not reduce to this interpretation. The formula alone does not handle changing surface concentrations or every chemical mechanism. [COMSOL's electrochemistry documentation](https://doc.comsol.com/6.4/doc/com.comsol.help.echem/ElectrochemistryModuleUsersGuide.pdf) is an example of an engineering implementation that makes kinetic models and their coupling to transport explicit.

At equilibrium, the net current is zero even though forward and reverse microscopic reactions can continue at equal rates. Exchange current characterizes this dynamic balance. It is not an offset current that should simply be subtracted from an experimental trace.

### Worked example 2: Small and moderate overpotential

Assume `n = 1`, `alpha_a = alpha_c = 0.5`, `T = 298.15 K`, and `j0 = 1.0 A/m²`. At `eta = 10 mV`:

```text
nF eta/(RT) = 0.3892
j = exp(0.1946) - exp(-0.1946)
  ≈ 0.392 A/m²
```

Linearization gives `j ≈ j0 nF eta/(RT) = 0.389 A/m²`, a close approximation. At 100 mV, the exact model gives approximately `6.86 A/m²`, while the same linear approximation gives `3.89 A/m²`. Linear behavior has a limited neighborhood around equilibrium.

For a working area of `1 mm² = 10^-6 m²`, the 10 mV example corresponds to about `0.392 µA`. These are synthetic calculations for the stated model, not expected performance of a specific device.

<a id="section-tafel-behavior-is-a-conditional-approximation"></a>

## Tafel behavior is a conditional approximation

When one Butler–Volmer exponential dominates and transport remains unimportant, taking a logarithm gives an approximately linear relationship between overpotential and log current. This is the Tafel region. A straight-looking line over a small range is not enough to establish that those conditions hold.

If reactant supply is depleted, measured current bends toward a limiting value. If ohmic loss grows with current, the apparent slope changes. If the surface changes composition or coverage during the sweep, the fitted slope may combine several processes. Before assigning mechanistic meaning, test the effect of flow, concentration, scan direction, stabilization time, and resistance correction.

<a id="section-ohmic-drop-and-what-the-potentiostat-actually-controls"></a>

## Ohmic drop and what the potentiostat actually controls

Electrolyte between the working surface and the point sensed by the reference has finite resistance. In a simple lumped model:

```text
E_interface ≈ E_measured - i R_u
```

The signs depend on the defined current direction and potential convention; the magnitude of the lost potential is `|i|R_u`. `R_u` is uncompensated resistance in ohms. The geometry matters because the electrolyte potential is a spatial field, not a single universal voltage.

### Worked example 3: A small current can matter

Suppose `i = 20 µA` and `R_u = 2.0 kΩ`. The ohmic drop is `40 mV`. If the intended kinetic perturbation is only 10 mV, ignoring this drop overwhelms the perturbation of interest. Compensation may help, but aggressive feedback can become unstable; geometry, reference placement, conductivity, and current range should also be considered.

The important design comparison is not simply whether current is “small.” It is whether the associated voltage error is small relative to the effect being interpreted.

<a id="section-coupling-thermodynamics-kinetics-and-transport"></a>

## Coupling thermodynamics, kinetics, and transport

An electrochemical sensor can be understood as three coupled descriptions:

| Description | Question | Typical quantities |
| --- | --- | --- |
| Thermodynamics | What equilibrium is favored? | activity, formal potential, Gibbs energy |
| Kinetics | How rapidly can charge transfer occur? | exchange current, rate constant, overpotential |
| Transport | How rapidly can reactant arrive or product leave? | diffusion coefficient, flow, film thickness |

Changing temperature can affect all three. A larger signal after heating does not, by itself, identify which changed. Changing electrode material can alter kinetics and adsorption. Changing the electrolyte can alter activities, conductivity, and diffusion. Controlled experiments vary one factor where possible and record the others.

<a id="section-design-decision-carried-forward"></a>

## Design decision carried forward

**Decision:** choose whether the prototype needs controlled working-electrode potential, a total-cell voltage, or a passive potential measurement. **Criteria:** interpretation of the intended response, reference stability, expected current, uncompensated resistance, and instrument compliance. **Evidence:** a balanced generic reaction where relevant, an electrical-work calculation, and an estimated `iR` error budget.

**Artifact:** an annotated electrode schematic showing the reference convention, current path, controlled voltage, and plausible competing reactions. State which parts of the measurement depend on equilibrium and which depend on kinetics. Connect the schematic to the [design studio](../design-studio.md).

<a id="section-problems-and-worked-answers"></a>

## Problems and worked answers

1. **Energy per mole.** A reversible complete cell transfers two electrons per reaction and has `E_cell = 0.250 V`. Find `Delta_r G`.

   **Answer:** `-2 × 96485.33212 × 0.250 = -48.24 kJ/mol` of the reaction as written. A half-cell potential alone cannot be inserted into this complete-cell energy calculation without specifying the paired process.

2. **Reference drift.** A feature shifts by 18 mV while a check standard shifts by 17 mV in the same direction. What is the first hypothesis?

   **Answer:** a largely common reference or measurement-scale shift. The approximately 1 mV residual is not automatically significant; compare the combined uncertainties before assigning a chemical change.

3. **Current scaling.** Under the worked Butler–Volmer assumptions, doubling electrode area leaves what unchanged?

   **Answer:** current density remains unchanged and total current doubles, provided mass transport and potential distribution are unchanged. Those provisos can fail in a real geometry.

4. **Mechanism critique.** A large cathodic peak is described as proof that an electrode recognizes one specific vapor. Is this justified?

   **Answer:** no. A peak can reflect analyte reaction, electrolyte decomposition, impurity reduction, adsorption, or a coupled process. Recognition requires controlled interferent and mixture tests plus evidence connecting the response to the proposed chemistry.

<a id="section-further-study"></a>

## Further study

Use [NIST's constants database](https://www.nist.gov/pml/fundamental-physical-constants) to verify the values used in numerical work. Read the source notes in the [foundations bibliography](../references/fundamentals.md). Prepare a diagram marking every potential difference and current path before analyzing any experimental cell.

<!-- course-footer:start -->
---

[Previous: Molecules, odor, and measurement](01-molecules-and-measurement.md) · [All modules](index.md) · [Next: Transport, partitioning, and response time](03-transport-and-partitioning.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
