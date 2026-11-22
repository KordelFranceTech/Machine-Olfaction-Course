---
layout: default
title: 'Worked solutions to integrated problems'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [Modules](../modules/index.md) · [Labs](../labs/index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Assessments](index.md) / Worked solutions to integrated problems

<!-- course-navigation:end -->

# Worked solutions to integrated problems

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [1. Concentration and chemical potential](#section-1-concentration-and-chemical-potential)
- [2. Transport times](#section-2-transport-times)
- [3. Charging current](#section-3-charging-current)
- [4. Impedance](#section-4-impedance)
- [5. Fluidics](#section-5-fluidics)
- [6. Conditioning and storage](#section-6-conditioning-and-storage)
- [7. Readout](#section-7-readout)
- [8. Correlated channels](#section-8-correlated-channels)
- [9. Predictive value](#section-9-predictive-value)
- [10. Leakage](#section-10-leakage)
- [11. Mechanism](#section-11-mechanism)
- [12. Synthesis](#section-12-synthesis)

</details>
<!-- course-toc:end -->

The reasoning matters as much as the number. Alternative answers to open-ended questions can be equally strong when their assumptions and tests are explicit.

<a id="section-1-concentration-and-chemical-potential"></a>

## 1. Concentration and chemical potential

Mole fraction is `5e-7`. Partial pressure is `5e-7*100000=0.05 Pa`. Molar concentration is `0.05/(8.31446*300)=2.0045e-5 mol/m^3`. The one-electron potential change is `(R*T/F)*ln(10)=0.05953 V` at 300 K. Gas composition does not establish the activities of an electroactive redox couple at a surface; partitioning, reaction, speciation, and transport intervene.

<a id="section-2-transport-times"></a>

## 2. Transport times

Film scale is `(50e-6)^2/(2e-10)=12.5 s`. Chamber time constant is `25/5=5 s`. The larger film scale merits early investigation, but `L^2/D` is a characteristic scale rather than a unique step-response constant. Boundary conditions, film geometry, partitioning, reaction, and chamber nonideality determine the actual response. Cascaded processes require a combined model or direct measurement.

<a id="section-3-charging-current"></a>

## 3. Charging current

`I=C*dE/dt=2e-6*0.020=40 nA`. This is already a substantial fraction of 60 nA. The remaining 20 nA cannot automatically be assigned to the target because other reactions and errors may exist. Suitable controls include a matched blank ramp, scan-rate dependence, a stable dummy cell, target-free humidity changes, and appropriate interferents. Subtraction should include its own uncertainty.

<a id="section-4-impedance"></a>

## 4. Impedance

`R_ct*C=0.01 s`, so `f=1/(2*pi*0.01)=15.9155 Hz`. At this frequency, `Re(Z)=200+10000=10200 Ω` and `-Im(Z)=10000 Ω`. A resistance change can reflect multiple chemical or physical changes; the circuit parameter alone does not identify a molecule.

<a id="section-5-fluidics"></a>

## 5. Fluidics

Flow is `100e-6/60=1.6667e-6 m^3/s`. Cross-sectional area is `pi*(0.001)^2=3.1416e-6 m^2`, giving velocity `0.5305 m/s`. Reynolds number is approximately `70.74`. Tube volume is `6.2832e-7 m^3=0.6283 mL`, with mean residence time `0.3770 s`. Hagen–Poiseuille pressure drop is approximately `15.28 Pa`.

The low Reynolds number is consistent with laminar flow under the stated assumptions. This calculation omits entry effects, fittings, valves, filters, pulsation, sorption, axial dispersion, and any substantial gas compression. Laminar flow does not imply identical molecular arrival times.

<a id="section-6-conditioning-and-storage"></a>

## 6. Conditioning and storage

Total recovery is `0.90*0.80=0.72`, or 72%. Independent relative standard uncertainties combine as `sqrt(0.05^2+0.05^2)=0.07071`, about 7.07%. Absolute standard uncertainty of the recovery fraction is approximately `0.0509`. Shared humidity effects introduce covariance; positive covariance increases uncertainty relative to the independent calculation. Recovery can also be concentration-dependent, making one correction factor inadequate.

<a id="section-7-readout"></a>

## 7. Readout

Maximum steady output change is `50e-9*20e6=1 V`. Ideal ADC step is `2/65536=30.52 µV`, corresponding to `1.526 pA` at the input. Actual detection depends on noise, bandwidth, bias, calibration, chemical sensitivity, blanks, drift, and decision criteria. A 2 µA transient would demand 40 V from this ideal gain, so ordinary low-voltage electronics would saturate. Range switching or a different gain/bandwidth strategy must be justified and tested.

<a id="section-8-correlated-channels"></a>

## 8. Correlated channels

Variance of the mean is `sigma^2*(rho+(1-rho)/n)=4*(0.5+0.5/4)=2.5`, so standard deviation is `1.5811`. Independent channels would give `2/sqrt(4)=1`. Compare dummy-cell measurements, shared versus separate sample paths, and common versus independent power sources. Change one suspected source at a time and estimate the covariance structure under realistic conditions.

<a id="section-9-predictive-value"></a>

## 9. Predictive value

At 1% prevalence: `0.95*0.01/[0.95*0.01+0.10*0.99]=0.08756`, or 8.76%. At 20% prevalence: `0.19/(0.19+0.08)=0.7037`, or 70.37%. The calculation assumes transfer of sensitivity and specificity; it does not prove that assumption. Study design, population, reference standard, confounding, confidence intervals, and intended clinical role remain essential.

<a id="section-10-leakage"></a>

## 10. Leakage

For deployment on new devices, reserve complete devices. For future operation of existing devices, reserve later acquisition periods while ensuring the development procedure matches the intended use. A study of both challenges needs a split that separates both or an explicit factorial evaluation. Fit scaling, imputation, feature selection, dimensionality reduction, threshold choice, and hyperparameters only within permitted development partitions. Repeated measurements do not create independent devices or days.

<a id="section-11-mechanism"></a>

## 11. Mechanism

Possible explanations include water-induced dielectric/conductivity change, altered wetted area, adsorption of an interferent, surface aging, and temperature change. Begin with electronics checks and matched blanks; vary target and humidity independently; include chemical neighbors; repeat across preparations; and add an orthogonal structural or compositional observation where the hypothesis requires it. Equivalent electrical responses may remain mechanistically ambiguous even after a high-quality fit.

<a id="section-12-synthesis"></a>

## 12. Synthesis

A strong answer makes each component serve a stated requirement and identifies an acceptance test. An adjacent project might be a public-data calibration workbench or a dummy-cell impedance teaching instrument, with an explicit architecture, reproducibility record, and review of applicable licenses and IP. Independent implementation and a different use case do not establish noninfringement. See [responsible innovation](../responsible-innovation.md).

[Return to assessments](index.md)

<!-- course-footer:start -->
---

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
