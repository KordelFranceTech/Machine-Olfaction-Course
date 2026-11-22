---
layout: default
title: 'Lab 01: units and the measurement chain'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [Modules](../modules/index.md) · [**Labs**](index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Labs](index.md) / Lab 01: units and the measurement chain

**Lab 01 of 8**

<!-- course-navigation:end -->

# Lab 01: units and the measurement chain

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Question](#section-question)
- [Model](#section-model)
- [Reproducible calculation](#section-reproducible-calculation)
- [Tasks](#section-tasks)
- [Worked interpretation](#section-worked-interpretation)
- [Failure analysis](#section-failure-analysis)
- [Design decision carried forward](#section-design-decision-carried-forward)

</details>
<!-- course-toc:end -->

**Time:** 2 hours. **Preparation:** Modules 01–02. **Tools:** calculator or standard-library Python.

<a id="section-question"></a>

## Question

A sensor produces an electrical response to material delivered through a gas stream. Can you connect a gas-phase mole fraction to a count of molecules, and then to an upper-bound electrochemical charge, without confusing concentration with flow or electrical signal with material captured?

The invented scenario uses a generic species at 2 ppm by mole, 100 kPa, and 298.15 K. Gas flows at 100 mL/min under these same conditions for 30 s. Assume an ideal gas. First calculate the amount delivered to the sampling system, not the amount captured by an electrode.

<a id="section-model"></a>

## Model

```text
n_total = P*Q*t/(R*T)
n_target = x*n_total
N_target = n_target*N_A
charge_if_all_target_reacts = n_e*F*n_target
```

`Q` must be in cubic metres per second. The electron stoichiometry `n_e=1` is a hypothetical teaching assumption. Complete capture and complete electron transfer are upper-bound assumptions; they are not a sensing model for an arbitrary vapor.

<a id="section-reproducible-calculation"></a>

## Reproducible calculation

```python
R = 8.314462618
F = 96485.33212
NA = 6.02214076e23
P = 100000.0
T = 298.15
x = 2.0e-6
flow_ml_min = 100.0
duration_s = 30.0
Q = flow_ml_min * 1e-6 / 60.0
c = x * P / (R * T)
n = c * Q * duration_s
charge = F * n
print(f"gas concentration: {c:.6e} mol/m^3")
print(f"target delivered: {n:.6e} mol")
print(f"molecules delivered: {n*NA:.6e}")
print(f"one-electron upper-bound charge: {charge:.6e} C")
print(f"upper-bound mean current: {charge/duration_s:.6e} A")
for capture_fraction in [1.0, 0.1, 0.01]:
    print(f"capture {capture_fraction:.2f}: "
          f"{capture_fraction*charge/duration_s:.6e} A")
assert 4e-9 < n < 4.1e-9
assert 1.2e-5 < charge/duration_s < 1.4e-5
```

Expected scale: roughly 4 nanomoles delivered, 2.4 quadrillion molecules, and 13 microamperes of mean current under the deliberately extreme complete-conversion assumption. A real measured current may be much smaller, larger because of background reactions, or unrelated to this direct-conversion model. Never treat the upper bound as a sensitivity specification.

<a id="section-tasks"></a>

## Tasks

1. Reproduce the amount by first calculating the 50 mL gas volume delivered and then applying the ideal-gas law.
2. Repeat at 20 ppb with every other input unchanged. Explain why the target amount changes linearly.
3. Suppose measured integrated charge is 1 microcoulomb. Compute an apparent capture-and-conversion fraction. State why an unmeasured background current prevents interpreting that fraction as collection efficiency.
4. If gas concentration is supplied on a dry basis and the sample contains 5% water by mole, derive the wet-basis target mole fraction under ideal mixing. Keep total wet pressure fixed.
5. Identify which physical observations would be needed to distinguish poor collection from slow reaction or an electronics gain error.

<a id="section-worked-interpretation"></a>

## Worked interpretation

At 20 ppb, mole fraction is one hundredth of the starting value, so amount and the hypothetical charge are one hundredth as large. For the original case, 1 microcoulomb divided by about 389 microcoulombs gives an apparent fraction near 0.00257, or 0.257%. This fraction combines every unmodeled process between inlet and charge integration.

The dry-to-wet conversion is `x_wet = x_dry*(1-y_water)` when the dry mixture's relative composition is preserved. Thus 2 ppm dry becomes 1.9 ppm wet for 5% water. Removing moisture can change both concentration basis and analyte recovery; those effects need separate treatment.

<a id="section-failure-analysis"></a>

## Failure analysis

Changing a flow controller's setting may change the total delivered target amount without changing concentration. A current-time integral may include double-layer charging. An instrument reporting “ppm” is already applying a calibration model; it does not directly count gas molecules. The purpose of the mass balance is to reveal such assumptions before a response is interpreted.

<a id="section-design-decision-carried-forward"></a>

## Design decision carried forward

Create a unit ledger for your project: concentration basis, temperature, pressure, flow conditions, integration duration, reference potential, and output units. Identify the quantity that is a specification and the quantity that is merely an instrument setting. Add one check preventing a thousand-fold unit error.

<!-- course-footer:start -->
---

[Previous: Computational and design laboratories](index.md) · [All labs](index.md) · [Next: Lab 02: transport, recovery, and storage](02-transport-and-storage.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
