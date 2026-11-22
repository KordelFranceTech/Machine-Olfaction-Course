---
layout: default
title: 'Getting started and prerequisite diagnostic'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](index.md) · **Start** · [Modules](modules/index.md) · [Labs](labs/index.md) · [Projects](projects/index.md) · [Library](references/index.md) · [Site map](navigation.md)

[Course home](index.md) / Getting started and prerequisite diagnostic

<!-- course-navigation:end -->

# Getting started and prerequisite diagnostic

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [A first encounter with the measurement chain](#section-a-first-encounter-with-the-measurement-chain)
- [What background do you need?](#section-what-background-do-you-need)
- [Diagnostic questions](#section-diagnostic-questions)
- [Worked diagnostic answers](#section-worked-diagnostic-answers)
- [How to read an equation](#section-how-to-read-an-equation)
- [Learning routes by background](#section-learning-routes-by-background)
- [Your first design artifact](#section-your-first-design-artifact)

</details>
<!-- course-toc:end -->

The goal is to become a designer who can explain each subsystem, not simply recognize its name. Keep a design notebook alongside the readings. After each module, record one decision, the assumptions supporting it, a plausible alternative, and a test that could overturn your choice. These records accumulate into the [design studio](design-studio.md).

<a id="section-a-first-encounter-with-the-measurement-chain"></a>

## A first encounter with the measurement chain

Imagine that an instrument reports a rise in electrical current when a vapor enters its inlet. At least six explanations are possible: the target participates in a redox reaction; a different molecule reacts; water changes ionic conductivity; the interface charges; the temperature changes reaction or transport rates; or the electronics offset changes. The first task is to design observations that separate these explanations.

A useful engineering statement has four pieces: a defined input, a proposed mechanism, a measured output, and a discriminating control. For example: “At fixed temperature and humidity, compare the electrical response with and without a generic target in a verified flow stream, and repeat with plausible interferents.” This is a statement about an experiment's logic, not a prescription for a particular chemical formulation.

Begin by drawing:

```text
environment -> inlet -> conditioning -> sensing interface
                                      -> electrical measurement
                                      -> features -> inference -> decision
```

Then add feedback paths. Flow affects transport; the electrical stimulus can alter the interface; a sampling decision changes the next measurement; calibration information changes how a signal is interpreted. A working instrument is an interacting system.

<a id="section-what-background-do-you-need"></a>

## What background do you need?

| Area | Minimum working knowledge | Where it becomes useful |
| --- | --- | --- |
| Chemistry | Moles, charge balance, bonding, oxidation/reduction, equilibrium | Chemical identity and interfacial mechanisms |
| Calculus | Derivatives, integrals, first-order differential equations | Transients, diffusion, filtering |
| Circuits | Ohm's law, impedance, Kirchhoff's laws, feedback | Potential control and current measurement |
| Linear algebra | Vectors, matrices, solving small systems, rank | Sensor arrays and inverse problems |
| Probability | Mean, variance, conditional probability, independent events | Uncertainty, diagnostic evidence, classifier evaluation |
| Programming | Variables, loops, functions, tables | Reproducing computational exercises |

Programming is useful but not a prerequisite for the first examples. The core labs use Python's standard library and can be checked with a calculator. Install software according to your institution's practices; the course does not require an online account or a proprietary dataset.

<a id="section-diagnostic-questions"></a>

## Diagnostic questions

Work these before reading the answers. A missed question identifies a topic to review, not a reason to stop.

1. Convert 250 ppb by mole into a dimensionless mole fraction. At 100 kPa, what is its partial pressure under an ideal-gas approximation?
2. A sensor produces 8 nA. What voltage magnitude does an ideal 10 MΩ transimpedance stage produce? What additional information determines the sign and whether the amplifier saturates?
3. A first-order response has time constant 4 s. What fraction of its final change has occurred after 4 s? After 12 s?
4. A signal changes from 1.0 to 1.1 arbitrary units, while its independent random standard deviation is 0.2 units per observation. What is the standard deviation of the mean of 100 independent observations? What kind of uncertainty is not removed by averaging?
5. Two outputs are `y1 = cA + cB` and `y2 = 2*cA + 2*cB`. Can they uniquely recover both concentrations?
6. A classifier has sensitivity 0.90 and specificity 0.95. For a population with 0.01 prevalence, what fraction of positive results are expected to be true positives, assuming those performance values transfer to that population?
7. If a gas sample spends 2 s in a tube, does every molecule arrive at exactly 2 s? Identify at least two reasons why not.
8. Does a good fit of a resistor-capacitor model prove a particular molecular mechanism? Explain.

<a id="section-worked-diagnostic-answers"></a>

## Worked diagnostic answers

**1.** `250 ppb = 250 * 10^-9 = 2.50 * 10^-7`. Partial pressure is mole fraction times total pressure: `2.50 * 10^-7 * 100000 Pa = 0.025 Pa`. Mole fraction is not mass concentration, and a dry-basis quantity needs care when compared with a wet sample.

**2.** `I*R = 8 * 10^-9 A * 10^7 Ω = 0.080 V`. An inverting stage has a negative current-to-voltage sign under its chosen convention. Supply rails, output swing, common-mode limits, bias point, and electrode wiring determine whether the result is achievable.

**3.** The normalized step response is `1 - exp(-t/tau)`: 0.632 at one time constant and 0.950 at three. A first-order model assumes a stable, linear, lumped process. Several transport and electronics stages can produce a more complicated response.

**4.** Independent averaging gives `0.2/sqrt(100) = 0.02`. Calibration bias, correlated drift, and common-mode humidity effects do not vanish simply because the same condition was sampled often. A smaller standard error is not automatically improved accuracy.

**5.** No. The second equation repeats the first with a different gain. There is one independent equation for two unknowns. For example, `(cA,cB)=(1,0)` and `(0,1)` both give `(y1,y2)=(1,2)`.

**6.** Among 10,000 people, expect 100 with the condition, 90 true positives, and `9900*0.05 = 495` false positives. Positive predictive value is `90/(90+495) = 0.1538`, about 15.4%. This is a conditional-probability exercise, not evidence for any clinical test.

**7.** Velocity varies across a laminar tube; molecules diffuse across streamlines; surfaces can adsorb and release molecules; fittings add dead volume. The residence time calculated as volume/flow is an average under specified conditions.

**8.** No. Several physical processes can produce similar electrical spectra. A defensible mechanism needs independent perturbations, controls, and often a second measurement modality. Fit quality addresses one model-data relationship, not uniqueness.

<a id="section-how-to-read-an-equation"></a>

## How to read an equation

Write its units beside every symbol. Ask what was held fixed during its derivation. Test zero-input and large-input limits. Then estimate a plausible order of magnitude before entering numbers into code. If an equation predicts an infinite current at time zero, that may signal an idealization rather than a physical event your instrument should reproduce.

For a paper, distinguish the quantity calculated by the authors from the quantity measured by their instrument. A fitted diffusion coefficient, a nominal gas concentration, and a measured output current are different evidence types. Copying all three into a spreadsheet does not give them equal status.

<a id="section-learning-routes-by-background"></a>

## Learning routes by background

Electrical engineers should spend extra time on activity, chemical equilibrium, and mass transport before interpreting electrical fits. Chemists should work through feedback stability, amplifier limits, sampling, and validation splits before trusting a compact instrument. Data scientists should begin with sample provenance and transport before optimizing a classifier. Mechanical engineers should connect flow design to interfacial sensitivity rather than treating the sensor as a perfect terminal boundary condition.

<a id="section-your-first-design-artifact"></a>

## Your first design artifact

Write a one-page problem statement for an invented educational application. Define the target quantity, sample matrix, environmental range, response time, acceptable error, and intended action. List three confounders and one condition under which the instrument should refuse to decide. Choose whether your final project will be an [integrated sensing system](design-studio.md) or an [adjacent independent project](derivative-projects.md).

<!-- course-footer:start -->
---

[Back to top](#page-top) · [Site map](navigation.md) · [Course home](index.md)
<!-- course-footer:end -->
