---
layout: default
title: 'Electrode interfaces and electrical transduction'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [**Modules**](index.md) · [Labs](../labs/index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Modules](index.md) / Electrode interfaces and electrical transduction

**Module 04 of 18**

<!-- course-navigation:end -->

# 04. Electrode interfaces and electrical transduction

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Learning outcomes](#section-learning-outcomes)
- [The interface is an active part of the device](#section-the-interface-is-an-active-part-of-the-device)
- [Charge separation and the electrical double layer](#section-charge-separation-and-the-electrical-double-layer)
- [Faradaic and non-Faradaic pathways](#section-faradaic-and-non-faradaic-pathways)
- [Equivalent circuits are models of behavior](#section-equivalent-circuits-are-models-of-behavior)
- [Geometric area, active area, and roughness](#section-geometric-area-active-area-and-roughness)
- [Two electrodes, three electrodes, and interdigitated geometries](#section-two-electrodes-three-electrodes-and-interdigitated-geometries)
- [Surface adsorption and competitive interactions](#section-surface-adsorption-and-competitive-interactions)
- [What direct structural evidence can establish](#section-what-direct-structural-evidence-can-establish)
- [Design decision carried forward](#section-design-decision-carried-forward)
- [Problems and worked answers](#section-problems-and-worked-answers)
- [Further study](#section-further-study)

</details>
<!-- course-toc:end -->

**Level:** undergraduate engineering. **Suggested effort:** 6–8 hours. **Prerequisites:** Modules 01–03; capacitors, resistors, and basic complex numbers.

<a id="section-learning-outcomes"></a>

## Learning outcomes

You will distinguish Faradaic and non-Faradaic current; calculate charge and charging current; explain the double layer without treating a molecular liquid as a rigid parallel-plate capacitor; compare electrode configurations; and design observations that discriminate among possible causes of an electrical response.

<a id="section-the-interface-is-an-active-part-of-the-device"></a>

## The interface is an active part of the device

An electrode is often drawn as a line touching a uniform liquid. The actual boundary contains molecules and ions with orientations, interactions, and spatial distributions that differ from those in the bulk. The electrode surface also contains defects, adsorbed species, and possibly oxide or reaction films.

A gas molecule entering this environment can alter electron-transfer kinetics, ionic conductivity, surface coverage, dielectric response, or the local arrangement of ions. Several of these effects can occur together. Consequently, a measurable signal need not imply that the analyte itself undergoes a direct redox reaction. Conversely, observing a current does not prove that the current is entirely capacitive.

The engineering objective is to connect a signal to a testable model. A model should predict how the response changes with time, potential, frequency, concentration, temperature, and controls. A picture of a molecular interaction is a hypothesis until measurements distinguish it from alternatives.

<a id="section-charge-separation-and-the-electrical-double-layer"></a>

## Charge separation and the electrical double layer

When an electrode acquires charge, the adjacent electrolyte redistributes ions and solvent. Opposite charge tends to accumulate nearby, subject to molecular size, solvation, correlations, and surface interactions. The electrode and its ionic environment together form an electrical double layer.

For a local, small perturbation, define differential capacitance:

```text
C_diff = dQ/dE
```

`Q` is electrode charge in C and `E` is the relevant interfacial potential in V. Total capacitance is in F. Area-normalized differential capacitance is `C_diff/A` in F/m². The derivative can depend on potential, composition, and timescale; it is not necessarily a constant.

A parallel-plate expression `C = epsilon A/d` is useful for dimensional intuition but not a complete description of a molecular double layer. In dilute-solution models, a compact region and a diffuse ionic region are often considered separately. In concentrated electrolytes and ionic liquids, finite ion sizes and correlations can become central. [Bazant, Storey, and Kornyshev's 2011 theory](https://doi.org/10.1103/PhysRevLett.106.046102), read with its [2012 erratum](https://web.mit.edu/bazant/www/papers/pdf/Bazant_2012_PRL_ionic_liquid_erratum.pdf), is a useful example of model development beyond a dilute diffuse layer.

Do not equate a model's layers with permanent material walls. A liquid interface is dynamic. Spatial order can coexist with rapid molecular exchange, and the relation between that order and a specific sensing function requires separate evidence.

### Worked example 1: Charging without chemical conversion

Assume an illustrative area-specific capacitance of `20 µF/cm²` and a planar area of `0.10 cm²`. Then total capacitance is `2.0 µF`. For a small 50 mV change over a region where capacitance is approximately constant:

```text
Delta Q = C Delta E
        = (2.0 × 10^-6 F)(0.050 V)
        = 1.0 × 10^-7 C = 100 nC
```

The external circuit supplies charge even if no sustained analyte redox reaction occurs. Dividing this charge by `F` would give an electron-equivalent amount, but that does not mean the same amount of analyte has reacted. The interpretation of charge requires a reaction and a Faradaic-efficiency model.

<a id="section-faradaic-and-non-faradaic-pathways"></a>

## Faradaic and non-Faradaic pathways

Faradaic current is associated with electron-transfer reactions. Non-Faradaic current can arise from charging the interface. A first approximation to the measured current is:

```text
i_total = i_Faradaic + i_charging + i_leakage + i_instrument
```

These terms are not always independently measurable or strictly additive under all conditions, but the decomposition is useful for designing controls. If capacitance is approximately constant during a potential ramp:

```text
i_charging ≈ C dE/dt
```

Increasing scan rate therefore increases charging current. Faradaic peaks can also change with scan rate, but often with a different scaling under a defined transport regime. Looking at scaling can provide evidence about the dominant contribution.

### Worked example 2: Scan-rate dependence

Using `C = 2.0 µF`, a ramp at `0.10 V/s` produces `0.20 µA` of ideal charging current. A ramp at `1.0 V/s` produces `2.0 µA`. If the chemical signal of interest is only `0.10 µA`, charging cannot be ignored merely because the electrode is small.

Suppose a blank subtraction removes most charging but the capacitance changes by 5% between blank and sample. At `1.0 V/s`, the residual charging contribution is `0.10 µA`, equal to the stated chemical signal. A reproducible blank is necessary, but an imperfectly matched blank can leave a structured artifact.

<a id="section-equivalent-circuits-are-models-of-behavior"></a>

## Equivalent circuits are models of behavior

A minimal circuit for a reacting interface can place a charge-transfer resistance in parallel with double-layer capacitance, with solution resistance in series:

```text
            ┌── R_ct ──┐
R_s ────────┤          ├────────
            └── C_dl ──┘
```

`R_s` describes a lumped ohmic contribution. `R_ct` describes a local linearized reaction response. `C_dl` describes charge storage over the measurement conditions. This circuit does not establish that each fitted value corresponds uniquely to one physical object.

For a simple reaction near equilibrium, linearizing Butler–Volmer gives:

```text
R_ct = RT/(n F i0)
```

Here `i0` is total exchange current, not current density. If current density `j0` is used, the area-normalized resistance is `RT/(nFj0)` in Ω m². Confusing these forms creates area-scaling errors. The circuit's relaxation timescale is `R_ct C_dl` when the ideal model applies.

The broader interpretation and limitations of equivalent circuits are discussed in [Lazanas and Prodromidis' EIS tutorial](https://pmc.ncbi.nlm.nih.gov/articles/PMC10288619/), with a [published correction](https://pubmed.ncbi.nlm.nih.gov/39995601/). Module 06 develops the measurements that test such a circuit.

<a id="section-geometric-area-active-area-and-roughness"></a>

## Geometric area, active area, and roughness

Geometric area comes from the device dimensions. Electrochemically accessible area depends on which parts of the surface the electrolyte and reactants can reach on the timescale of interest. A rough or porous electrode can have much more microscopic area than its footprint, but some pores may fill slowly or remain inaccessible.

More area can increase both desired current and background charging. More roughness can create a wider distribution of surface environments, changing selectivity, noise, and reproducibility. A nominal area increase is therefore not a complete performance metric.

Consider two devices with the same footprint. Device A doubles analyte response and doubles blank variability. Device B increases analyte response by only 40% but leaves blank variability unchanged. Depending on the error model and operating range, B may provide better detection performance. Report signal and noise together, as well as response time and stability.

<a id="section-two-electrodes-three-electrodes-and-interdigitated-geometries"></a>

## Two electrodes, three electrodes, and interdigitated geometries

Electrode count and electrode geometry answer different questions. In a three-electrode experiment, working, reference, and counter roles are separated. In a two-electrode experiment, both interfaces contribute to the observed cell response. An interdigitated geometry places alternating finger-like conductors close together; it does not by itself specify whether the experiment is electrochemical, capacitive, resistive, or a combination.

| Configuration | Useful capability | Interpretation challenge |
| --- | --- | --- |
| Three-electrode cell | Control a working electrode relative to a reference | Reference drift, placement, junction effects, and counter limits |
| Two-electrode cell | Compact total-cell measurement | Separate contributions from both interfaces and bulk electrolyte |
| Interdigitated conductors | Short lateral length scales and planar integration | Fringing fields, film coverage, parasitic capacitance, geometry-dependent cell constant |
| Microelectrode | Small area and potentially radial diffusion | Different transport scaling and demanding low-current measurement |

The same material can produce different signals in these configurations. Comparing raw impedance or current across geometries without a physical normalization is often misleading. Definitions of electrode systems are given in [IUPAC's electrochemical terminology recommendations](https://doi.org/10.1515/pac-2018-0109).

<a id="section-surface-adsorption-and-competitive-interactions"></a>

## Surface adsorption and competitive interactions

Adsorption is accumulation at an interface; absorption is incorporation into a bulk phase. A sensing film can support both. For a simplified competitive adsorption model with species A and B:

```text
theta_A = K_A c_A/(1 + K_A c_A + K_B c_B)
theta_B = K_B c_B/(1 + K_A c_A + K_B c_B)
```

The expressions assume a common set of independent sites and equilibrium behavior. They are teaching models, not universal descriptions of complex films. They demonstrate why an interferent can suppress a target response even if the interferent produces little signal by itself: it occupies shared capacity.

For `K_A c_A = 1` and no B, `theta_A = 0.5`. With `K_B c_B = 8`, `theta_A = 0.1`. A single-analyte calibration can therefore overpredict the response in a mixture by a large factor. The appropriate test includes mixtures and realistic background conditions.

<a id="section-what-direct-structural-evidence-can-establish"></a>

## What direct structural evidence can establish

Modern surface methods can examine interfacial organization with far greater detail than a current trace alone. In 2025, [Ai and colleagues](https://doi.org/10.1073/pnas.2421635122) used electrochemical three-dimensional atomic-force microscopy to study changes in liquid layering around growing interfacial structures in an ionic-liquid battery model system. This is evidence about spatial organization under the studied conditions; it is not a demonstration of general vapor recognition.

An engineering inference from this work is that flat, homogeneous-surface models may miss important local behavior. The next experiment should depend on the inference being tested: surface imaging for morphology, spectroscopy for chemical identity, controlled electrochemistry for kinetics, and blinded mixture tests for analytical selectivity. Combining independent modalities is stronger than interpreting every observable through one preferred mechanism.

<a id="section-design-decision-carried-forward"></a>

## Design decision carried forward

**Decision:** choose an electrode topology and a candidate electrical observable that can be interpreted under realistic background changes. **Criteria:** accessible area, charging current, current path, film coverage, reference arrangement, and separation of bulk and interface effects. **Evidence:** a calculated charging background and at least two competing physical explanations for the anticipated signal.

**Artifact:** an interface model with a labeled equivalent circuit, an area convention, and a control experiment that can reject one explanation. Record which fitted parameters would remain ambiguous. Integrate this model with the [design studio](../design-studio.md), rather than treating an electrical response as molecular identification by itself.

<a id="section-problems-and-worked-answers"></a>

## Problems and worked answers

1. **Capacitive current.** A measured interface has `C = 5 µF`. What ramp rate gives an ideal charging current of 50 nA?

   **Answer:** `dE/dt = i/C = 0.010 V/s`. This estimate assumes constant capacitance and negligible other current contributions.

2. **Relaxation time.** A circuit has `R_ct = 50 kΩ` and `C_dl = 4 µF`. Find its ideal time constant and characteristic frequency.

   **Answer:** `tau = 0.20 s`; `f = 1/(2 pi tau) = 0.796 Hz`. A measured feature near this frequency is compatible with the model but does not uniquely prove it.

3. **Area normalization.** Total exchange current is `2 µA` on `0.20 cm²`. What is exchange current density?

   **Answer:** `10 µA/cm² = 0.10 A/m²`. Convert area carefully: `1 cm² = 10^-4 m²`.

4. **Design a discrimination experiment.** A vapor exposure decreases measured impedance. Give three explanations and one test for each.

   **Answer guide:** increased bulk ionic conductivity: vary electrode spacing or use a separate conductivity cell; changed interfacial capacitance: examine potential/frequency dependence with a validated model; faster Faradaic kinetics: test a reaction-sensitive potential region and appropriate blanks. Temperature or water uptake could cause any of these and should be independently measured.

<a id="section-further-study"></a>

## Further study

Read the [foundations bibliography](../references/fundamentals.md) for the status and limitations of the interface papers. Sketch a device with separate annotations for chemical species, ionic current, electronic current, charge storage, and uncontrolled parasitic paths. This diagram should be more informative than a single arrow labeled “signal.”

<!-- course-footer:start -->
---

[Previous: Transport, partitioning, and response time](03-transport-and-partitioning.md) · [All modules](index.md) · [Next: Ionic liquids and sensing-material selection](05-ionic-liquids-and-materials.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
