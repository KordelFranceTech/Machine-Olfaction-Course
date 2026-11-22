---
layout: default
title: 'Electrochemical methods and model validation'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [**Modules**](index.md) · [Labs](../labs/index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Modules](index.md) / Electrochemical methods and model validation

**Module 06 of 18**

<!-- course-navigation:end -->

# 06. Electrochemical methods and model validation

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Learning outcomes](#section-learning-outcomes)
- [Choose a measurement to answer a question](#section-choose-a-measurement-to-answer-a-question)
- [Open circuit is not absence of chemistry](#section-open-circuit-is-not-absence-of-chemistry)
- [Cyclic voltammetry: a controlled perturbation](#section-cyclic-voltammetry-a-controlled-perturbation)
- [Chronoamperometry: inspect the whole transient](#section-chronoamperometry-inspect-the-whole-transient)
- [Impedance starts with small-signal linearization](#section-impedance-starts-with-small-signal-linearization)
- [Derive an ideal semicircle](#section-derive-an-ideal-semicircle)
- [Diffusion impedance and nonideal capacitance](#section-diffusion-impedance-and-nonideal-capacitance)
- [Linearity, stationarity, and consistency tests](#section-linearity-stationarity-and-consistency-tests)
- [Identifiability: can the experiment answer the question?](#section-identifiability-can-the-experiment-answer-the-question)
- [A disciplined measurement sequence](#section-a-disciplined-measurement-sequence)
- [Design decision carried forward](#section-design-decision-carried-forward)
- [Problems and worked answers](#section-problems-and-worked-answers)
- [Further study](#section-further-study)

</details>
<!-- course-toc:end -->

**Level:** advanced undergraduate engineering. **Suggested effort:** 8–10 hours. **Prerequisites:** Modules 01–05; sinusoidal signals, complex numbers, least-squares fitting.

<a id="section-learning-outcomes"></a>

## Learning outcomes

You will choose between open-circuit, voltammetric, transient-current, and impedance measurements; calculate elementary responses; distinguish circuit fitting from mechanism identification; evaluate linearity and stationarity; and produce a measurement plan with blanks, controls, and stopping criteria.

<a id="section-choose-a-measurement-to-answer-a-question"></a>

## Choose a measurement to answer a question

Each electrochemical method imposes one electrical condition and observes another. Changing the method changes which processes are emphasized. A single endpoint cannot reveal every kinetic, transport, and interfacial contribution.

| Method | Typical imposed condition | Observed quantity | Useful question |
| --- | --- | --- | --- |
| Open-circuit potential | Negligible external current | Potential versus reference | Does the equilibrium or mixed potential change? |
| Cyclic voltammetry | Forward/reverse potential ramp | Current versus potential/time | Are there reaction features, hysteresis, or changing backgrounds? |
| Chronoamperometry | Potential step or hold | Current versus time | What transient follows a change, and does a stable regime emerge? |
| Amperometric monitoring | Fixed defined potential | Current during sample exposure | Can concentration-related changes be measured continuously? |
| Impedance spectroscopy | Small periodic perturbation about an operating point | Complex voltage/current ratio | What timescales and linear response components are present? |

These methods are standardized in terminology, but their interpretation depends on the cell and assumptions. [IUPAC's recommendations](https://doi.org/10.1515/pac-2018-0109) are useful for reporting the experiment precisely.

<a id="section-open-circuit-is-not-absence-of-chemistry"></a>

## Open circuit is not absence of chemistry

At open circuit, the external current is close to zero. Several internal reactions can still occur with balancing anodic and cathodic currents. The measured potential can be a mixed potential rather than the equilibrium potential of one isolated redox couple.

A slowly changing open-circuit potential may indicate equilibration, reference drift, temperature drift, surface change, or composition change. It is a useful diagnostic but not an automatic analyte concentration scale. Record how long the system was allowed to settle and what stability criterion was used.

<a id="section-cyclic-voltammetry-a-controlled-perturbation"></a>

## Cyclic voltammetry: a controlled perturbation

In cyclic voltammetry, potential is swept to a chosen limit and then reversed. The response can reveal the onset of reactions, return features, background charging, and changes over repeated cycles. The useful comparison is often not one trace but how traces change with scan rate, concentration, electrode area, and experimental history.

For an ideal reversible, diffusion-controlled dissolved redox couple at 298.15 K, the Randles–Ševčík peak-current expression in a common unit convention is:

```text
i_p = 2.69 × 10^5 n^(3/2) A D^(1/2) c v^(1/2)

i_p in A
A in cm²
D in cm²/s
c in mol/cm³
v in V/s
```

The numerical coefficient belongs to those units and temperature. Surface-confined species, sluggish reactions, finite films, adsorption, uncompensated resistance, and coupled chemistry can break the simple scaling. [Elgrishi and colleagues' practical guide](https://doi.org/10.1021/acs.jchemed.7b00361) is a suitable first laboratory reading, with emphasis on measurement discipline rather than matching every trace to an ideal shape.

### Worked example 1: Predict a model peak current

Take `n = 1`, `A = 0.010 cm²`, `D = 1.0 × 10^-5 cm²/s`, `c = 1.0 × 10^-6 mol/cm³` (1 mmol/L), and `v = 0.10 V/s`:

```text
i_p = (2.69 × 10^5)(0.010)(sqrt(10^-5))(10^-6)(sqrt(0.10))
    = 2.69 × 10^-6 A = 2.69 µA
```

At `0.40 V/s`, the ideal peak doubles to `5.38 µA`. Capacitive background for constant capacitance instead rises fourfold because it scales with `v`. Comparing these trends can help separate contributions, but a narrow scan-rate interval and changing surface state can make the distinction ambiguous.

<a id="section-chronoamperometry-inspect-the-whole-transient"></a>

## Chronoamperometry: inspect the whole transient

A potential step produces several overlapping processes. Instrument settling and double-layer charging dominate some early intervals. Charge-transfer kinetics and diffusion can become visible later. Finite-volume depletion, convection, and drift can dominate still later.

The ideal Cottrell expression from Module 03 predicts `i ∝ t^-1/2` for a specific planar, semi-infinite diffusion problem. A straight line in `i` versus `t^-1/2` over a selected interval is compatible with that model. It is not proof that the entire trace follows it. The [IUPAC definition](https://goldbook.iupac.org/terms/view/09069/html) makes the necessary conditions explicit.

For gas exposure at constant potential, the inlet concentration may itself have a transient. Distinguish a potential-step experiment from a concentration-step experiment. Their boundary conditions differ even if the resulting current traces look similar. Record synchronized flow and exposure timing when transport is part of the question.

<a id="section-impedance-starts-with-small-signal-linearization"></a>

## Impedance starts with small-signal linearization

At a defined operating point, apply a small sinusoidal perturbation:

```text
E(t) = E_dc + E_ac sin(omega t)
omega = 2 pi f
Z(omega) = E_tilde(omega)/I_tilde(omega)
```

The tildes represent complex amplitudes; the ratio includes phase as well as magnitude. Impedance has units of ohms. The system should remain approximately linear and sufficiently unchanged during the measurement for the chosen interpretation.

An ideal resistor has `Z_R = R`. An ideal capacitor has `Z_C = 1/(j omega C)`, where `j² = -1`. Capacitor current leads voltage by 90 degrees under the usual convention. A **Bode plot** shows magnitude and phase against frequency, usually on a logarithmic frequency axis. A common **Nyquist plot** uses `Z'` on the horizontal axis and `-Z''` on the vertical axis. Always state the sign convention.

[Lazanas and Prodromidis' 2023 tutorial](https://pmc.ncbi.nlm.nih.gov/articles/PMC10288619/) develops the phasor and circuit framework. Its [2025 correction](https://pubmed.ncbi.nlm.nih.gov/39995601/) should accompany the reading. The calculations below are independent worked examples of explicit ideal circuits.

<a id="section-derive-an-ideal-semicircle"></a>

## Derive an ideal semicircle

For a series resistance and a parallel resistor-capacitor branch:

```text
Z = R_s + R_ct/(1 + j omega R_ct C_dl)
tau = R_ct C_dl

Z'  = R_s + R_ct/[1 + (omega tau)²]
-Z'' = R_ct omega tau/[1 + (omega tau)²]
```

At high frequency, impedance approaches `R_s`. At low frequency, it approaches `R_s + R_ct`. The maximum of `-Z''` occurs at `omega tau = 1`, so the characteristic frequency is `1/(2 pi R_ct C_dl)`. The apparent semicircle follows from this algebra; it does not require assuming that every semicircular experimental arc represents charge transfer.

### Worked example 2: Read a synthetic circuit

Let `R_s = 100 Ω`, `R_ct = 10 kΩ`, and `C_dl = 10 µF`. Then `tau = 0.10 s` and the characteristic frequency is `1.59 Hz`. At that frequency:

```text
Z' = 100 + 10000/2 = 5100 Ω
Z'' = -10000/2 = -5000 Ω
|Z| ≈ 7142 Ω
phase ≈ -44.4 degrees
```

The high-frequency intercept is 100 Ω and the low-frequency intercept is 10100 Ω. If the measured frequency range never reaches either side of the arc, resistance estimates can be poorly constrained even when the fitted curve appears smooth.

<a id="section-diffusion-impedance-and-nonideal-capacitance"></a>

## Diffusion impedance and nonideal capacitance

Semi-infinite diffusion can contribute a Warburg-type impedance proportional to `(1 - j)/sqrt(omega)` under a common convention. It produces a 45-degree line in a conventional Nyquist plot over the appropriate regime. Finite-length diffusion, convection, and reaction boundaries change low-frequency behavior. A diagonal segment is therefore a clue to investigate, not an automatic diffusion coefficient.

A constant-phase element, or CPE, is often written:

```text
Z_CPE = 1/[Q (j omega)^alpha]
```

`alpha = 1` gives an ideal capacitor, with `Q` in farads. Otherwise `Q` has units of `S s^alpha` and should not casually be called a capacitance. A CPE can describe a distributed response phenomenologically; it does not uniquely identify surface roughness or one particular physical cause.

Equivalent circuits should be selected from plausible physics and experimental resolution. Adding elements almost always improves an unconstrained fit, but can make parameter estimates meaningless. Report why the model is identifiable over the measured range.

<a id="section-linearity-stationarity-and-consistency-tests"></a>

## Linearity, stationarity, and consistency tests

Linearity can be examined by repeating a spectrum at more than one sufficiently small perturbation amplitude. If the normalized impedance changes systematically, the small-signal approximation may be failing, or noise and drift may dominate. A single customary amplitude is not universal proof of linearity.

Stationarity means that the system does not change appreciably over the acquisition interval relevant to the analysis. Low-frequency measurements are especially exposed to slow drift because they take longer. Compare repeated spectra, reverse frequency order when useful, and record baseline evolution. A system responding to a changing gas concentration can violate the stationary-spectrum assumption.

[Boukamp's 1995 linear Kramers–Kronig validation method](https://doi.org/10.1149/1.2044210) tests whether measured real and imaginary components are consistent with a suitable causal linear response representation. A favorable test supports consistency; finite bandwidth, noise, and model choices limit what it proves. It does not establish a unique circuit, a specific molecule, or a complete mechanism.

The open-source [impedance.py paper and implementation](https://joss.theoj.org/papers/10.21105/joss.02349) provide a reproducible entry point for fitting and validation. Software output should be accompanied by model equations, residuals, parameter bounds, uncertainty, and the data processing choices used.

<a id="section-identifiability-can-the-experiment-answer-the-question"></a>

## Identifiability: can the experiment answer the question?

Suppose a circuit has two relaxation processes with nearly equal time constants. Their arcs overlap. Many parameter combinations may reproduce the measured data. This is a practical identifiability problem, not necessarily a failure of optimization.

Look for parameter correlation, broad confidence intervals, dependence on starting values, and large changes when a few frequencies are removed. Compare predictions outside the fitted conditions, such as another temperature or concentration, when justified. Independent measurements of film thickness, conductivity, or area can constrain the model and reduce ambiguity.

Weighting also matters. Minimizing unweighted absolute error can let large low-frequency impedances dominate. Relative weighting can overemphasize noisy small values. Choose a weighting model that reflects measurement uncertainty, and state it. Inspect real and imaginary residuals as functions of frequency rather than reporting only one goodness-of-fit number.

<a id="section-a-disciplined-measurement-sequence"></a>

## A disciplined measurement sequence

For an educational investigation, begin with a passive electrical dummy circuit whose response is known. Confirm wiring, polarity, range, and phase behavior. Next examine the blank electrochemical cell, then an independently characterized educational reference system, and only then the sensing film and controlled gas exposures under an approved laboratory plan.

This progression separates electronics errors from electrochemical errors and sampling errors. It is not a device-specific operating waveform. Exact excitation limits must come from the material stability evidence and the instrument's validated capabilities.

Include a negative control, matrix-matched blanks, repeat exposures, independent devices, and recovery periods. Define rejection criteria before seeing the target data: clipping, unstable reference, failed baseline criterion, significant dummy-circuit mismatch, or unresolved drift. Rejected data should remain documented rather than silently disappearing.

<a id="section-design-decision-carried-forward"></a>

## Design decision carried forward

**Decision:** choose the measurement modality and operating-point verification strategy for the hypothetical sensor. **Criteria:** signal size, response timescale, selectivity evidence, perturbation stability, acquisition duration, and electronic feasibility. **Evidence:** a predicted response from a simple model, a blank measurement plan, and at least one competing explanation for the signal.

**Artifact:** a measurement specification containing the controlled and observed variables, reference convention, units, frequency or time requirements, validation checks, and pass/fail criteria. Add an identifiability statement explaining what the experiment cannot determine. Integrate it with the material memo in the [design studio](../design-studio.md).

<a id="section-problems-and-worked-answers"></a>

## Problems and worked answers

1. **Characteristic frequency.** If capacitance doubles while `R_ct` remains constant, what happens to the ideal arc diameter and peak frequency?

   **Answer:** diameter remains `R_ct`; peak frequency halves. A changed arc diameter would require another parameter change in this simple model.

2. **Frequency versus duration.** How long is one cycle at 0.01 Hz? What concern follows if baseline drifts substantially over 20 s?

   **Answer:** 100 s. The system can change materially within one cycle, undermining a stationary impedance interpretation.

3. **CPE interpretation.** A fit returns `alpha = 0.8` and `Q = 10^-5`. Can the result be reported as 10 µF?

   **Answer:** no. The units differ from farads unless `alpha = 1`. Any conversion to an effective capacitance requires a stated model and convention.

4. **Model evidence.** Two circuits fit within the measurement noise but predict different changes with film thickness. What experiment is useful?

   **Answer:** fabricate or obtain independently characterized thickness variants and test the preregistered predictions while controlling composition, area, and conditioning. Additional data should distinguish predictions rather than merely add more points under the same ambiguous conditions.

<a id="section-further-study"></a>

## Further study

The [foundations bibliography](../references/fundamentals.md) gives source access and limitations. Complete the dummy-circuit exercise before interpreting a fitted molecular mechanism. The next stage connects these measurements to practical sampling, device construction, and system validation.

<!-- course-footer:start -->
---

[Previous: Ionic liquids and sensing-material selection](05-ionic-liquids-and-materials.md) · [All modules](index.md) · [Next: 07 · Sampling and fluidics](07-sampling-and-fluidics.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
