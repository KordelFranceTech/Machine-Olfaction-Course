---
layout: default
title: 'Integrated engineering problem set'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [Modules](../modules/index.md) · [Labs](../labs/index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Assessments](index.md) / Integrated engineering problem set

<!-- course-navigation:end -->

# Integrated engineering problem set

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [1. Concentration and chemical potential](#section-1-concentration-and-chemical-potential)
- [2. Competing transport times](#section-2-competing-transport-times)
- [3. Current and charging](#section-3-current-and-charging)
- [4. Impedance](#section-4-impedance)
- [5. Fluidics](#section-5-fluidics)
- [6. Conditioning and storage](#section-6-conditioning-and-storage)
- [7. Readout design](#section-7-readout-design)
- [8. Correlated channels](#section-8-correlated-channels)
- [9. Diagnostic interpretation](#section-9-diagnostic-interpretation)
- [10. Data leakage](#section-10-data-leakage)
- [11. Mechanism versus fit](#section-11-mechanism-versus-fit)
- [12. Design synthesis and independent extension](#section-12-design-synthesis-and-independent-extension)

</details>
<!-- course-toc:end -->

All numerical systems below are hypothetical. State units and assumptions in every answer. Use the [worked solutions](solutions.md) after making an independent attempt.

<a id="section-1-concentration-and-chemical-potential"></a>

## 1. Concentration and chemical potential

A gas mixture contains a generic target at 500 ppb by mole, total pressure 100 kPa, and 300 K. Calculate target partial pressure and molar concentration. For a one-electron reduction at 300 K, compute the equilibrium potential change if the oxidized-to-reduced activity ratio increases by a factor of ten. Explain why the gas concentration calculation does not determine that activity ratio at an electrode.

<a id="section-2-competing-transport-times"></a>

## 2. Competing transport times

Compare a 50 µm sensing film with diffusion coefficient `2e-10 m^2/s` against a 25 mL perfectly mixed chamber flowing at 5 mL/s. Calculate the film scale `L^2/D` and the chamber time constant. Which should be investigated first as a possible response bottleneck? Why cannot their time constants simply be treated as experimentally established response times?

<a id="section-3-current-and-charging"></a>

## 3. Current and charging

A 2 µF interface experiences a linear voltage ramp of 20 mV/s. Calculate its ideal charging current. A simultaneous measured current is 60 nA. Explain why attributing all measured current to a target reaction would be unjustified. List two controls.

<a id="section-4-impedance"></a>

## 4. Impedance

An ideal `R_s + (R_ct parallel C)` circuit has `R_s=200 Ω`, `R_ct=20 kΩ`, and `C=0.5 µF`. Find its characteristic frequency and its real and negative-imaginary components at that frequency. Would a change in `R_ct` uniquely establish that a particular analyte was present?

<a id="section-5-fluidics"></a>

## 5. Fluidics

Air is approximated as Newtonian with density `1.2 kg/m^3` and viscosity `1.8e-5 Pa*s`. A circular tube is 0.2 m long and 2 mm in diameter. Flow is 100 mL/min at the stated conditions. Estimate mean velocity, Reynolds number, tube volume, residence time, and laminar pressure drop. List unmodeled contributions.

<a id="section-6-conditioning-and-storage"></a>

## 6. Conditioning and storage

A conditioning element transmits 90% of a target contribution, while a storage stage retains 80%. Assuming independent multiplicative recovery with no contamination, calculate total recovery. If each stage has independent relative standard uncertainty 5%, find relative standard uncertainty of the product. Explain what changes if the recovery errors share a humidity dependence.

<a id="section-7-readout-design"></a>

## 7. Readout design

A signal spans 0–50 nA, and a proposed TIA uses a 20 MΩ feedback resistor. Find output swing. With a 2 V ideal 16-bit ADC span, compute voltage step and equivalent input-current step. Why is this not the system's limit of detection? What happens if a 2 µA charging transient occurs?

<a id="section-8-correlated-channels"></a>

## 8. Correlated channels

Four identical channels have individual standard deviation 2 units and equal pairwise correlation 0.5. Find the standard deviation of their average. Compare it with independent-channel averaging. What kinds of experiments would help determine whether the correlation is caused by electronics or sample handling?

<a id="section-9-diagnostic-interpretation"></a>

## 9. Diagnostic interpretation

A hypothetical test has sensitivity 0.95 and specificity 0.90. Compute positive predictive value at prevalence 0.01 and 0.20, assuming performance transfers. Identify why this calculation alone cannot justify a health claim or deployment.

<a id="section-10-data-leakage"></a>

## 10. Data leakage

There are five devices, each measured 100 times on each of three days. A student randomly splits all rows and reports excellent classification. Propose two different held-out designs for two different deployment goals. Name at least three transformations that must be fitted without access to final-test data.

<a id="section-11-mechanism-versus-fit"></a>

## 11. Mechanism versus fit

A spectrum fits a resistor-capacitor model with very small residuals. The student interprets a capacitance change as a unique molecular recognition event. Construct at least three alternative explanations and design a sequence of controls that distinguishes them. State what electrical measurements alone may still leave ambiguous.

<a id="section-12-design-synthesis-and-independent-extension"></a>

## 12. Design synthesis and independent extension

Choose a sensing application and produce a one-page architecture. Include sample path, sensing interface, measurement mode, environmental context, calibration, decision states, and module interfaces. Then propose one useful adjacent project that can be pursued from independently documented public sources. State its acceptance test, what it omits from the first architecture, and why technical differences do not establish freedom to operate.

[Worked solutions](solutions.md) · [Design studio](../design-studio.md)

<!-- course-footer:start -->
---

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
