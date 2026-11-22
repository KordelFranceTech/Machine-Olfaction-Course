---
layout: default
title: 'Molecules, odor, and measurement'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [**Modules**](index.md) · [Labs](../labs/index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Modules](index.md) / Molecules, odor, and measurement

**Module 01 of 18**

<!-- course-navigation:end -->

# 01. Molecules, odor, and measurement

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Learning outcomes](#section-learning-outcomes)
- [Start with the engineering question](#section-start-with-the-engineering-question)
- [Gas, vapor, volatile compound, and odor](#section-gas-vapor-volatile-compound-and-odor)
- [Count molecules using amount fractions](#section-count-molecules-using-amount-fractions)
- [Humidity changes both the sample and the sensor](#section-humidity-changes-both-the-sample-and-the-sensor)
- [Concentration is not activity](#section-concentration-is-not-activity)
- [Data sources: read the conditions, not just the number](#section-data-sources-read-the-conditions-not-just-the-number)
- [Uncertainty and significant figures](#section-uncertainty-and-significant-figures)
- [Common mistakes and how to correct them](#section-common-mistakes-and-how-to-correct-them)
- [Design decision carried forward](#section-design-decision-carried-forward)
- [Problems and worked answers](#section-problems-and-worked-answers)
- [Further study](#section-further-study)

</details>
<!-- course-toc:end -->

**Level:** undergraduate engineering. **Suggested effort:** 5–7 hours, including problems. **Prerequisites:** algebra, introductory chemistry, dimensional analysis.

<a id="section-learning-outcomes"></a>

## Learning outcomes

After this module, you should be able to define the quantity a chemical sensor is intended to measure; distinguish chemical identity from odor perception; convert gas amount fractions into concentrations; explain why humidity belongs in the measurement model; and state a result with meaningful units and uncertainty.

<a id="section-start-with-the-engineering-question"></a>

## Start with the engineering question

A machine does not encounter a label saying “coffee,” “leak,” or “healthy.” It encounters molecules, particles, temperature gradients, and changing airflow. The instrument must convert some part of that physical environment into an electrical record. A later algorithm may associate the record with a label. Keeping those stages separate helps locate errors.

Imagine a sensor beside a cup containing an aromatic liquid. The amount placed in the cup is not the amount present at the sensor. Molecules must leave the liquid, mix with surrounding gas, pass through the inlet, and interact with a sensing surface. Some stick to tubing. Others dissolve in condensed water. Even before electronics are considered, the sample has changed.

Write an initial measurement specification as a sentence: “Estimate the amount fraction of species A in an air stream, averaged over ten seconds, at the sensor inlet, over a stated temperature and humidity range.” That sentence identifies a **measurand**, the quantity intended to be measured. It also identifies where and when the quantity is defined. “Detect smell accurately” does not.

The [International Vocabulary of Metrology](https://www.iso.org/sites/JCGM/VIM/JCGM_200e_FILES/MAIN_JCGM_200e/02_e.html) provides the vocabulary needed to distinguish a measurand, a measurement result, calibration, and uncertainty. These distinctions are practical design tools: changing the measurand can change the required sampling system and the meaning of the calibration.

<a id="section-gas-vapor-volatile-compound-and-odor"></a>

## Gas, vapor, volatile compound, and odor

Gas and vapor both describe gaseous material; “vapor” usually emphasizes that the substance can coexist with a liquid or solid under the conditions of interest. Volatility concerns a substance's tendency to enter the gas phase. It is influenced by temperature, composition, and intermolecular interactions.

An organic vapor is not automatically odorous at every concentration. Conversely, important odorous gases can be inorganic. Ammonia and hydrogen sulfide are not organic compounds. Carbon dioxide is not ordinarily treated as an organic compound. Nitric oxide is not a VOC. A curriculum on machine olfaction must therefore extend beyond VOCs while preserving those chemical distinctions.

The phrase “VOC” also has different scientific and regulatory uses. The [US EPA's technical overview](https://www.epa.gov/indoor-air-quality-iaq/technical-overview-volatile-organic-compounds) distinguishes general volatility-based usage from definitions designed for particular environmental purposes. State which meaning applies. Do not infer a sensor's chemical coverage from the phrase “total VOC” without knowing how the instrument responds to different compounds.

Human odor perception adds biology. A molecule's airborne concentration, its interactions with receptors, and the nervous system's processing all matter. An electrical response to a compound is evidence of transduction, not evidence that the instrument reproduces human perception. An array can be useful for classifying a restricted set of samples even if it cannot assign their complete molecular composition or perceptual odor.

<a id="section-count-molecules-using-amount-fractions"></a>

## Count molecules using amount fractions

For a gas mixture, the amount fraction of species A is its amount of substance divided by the total amount:

```text
x_A = n_A / n_total

1 µmol/mol = 10^-6 mol/mol = 1 ppm by amount
1 nmol/mol = 10^-9 mol/mol = 1 ppb by amount
```

Here `n` is measured in moles. The fraction is dimensionless, but writing `µmol/mol` makes its basis explicit. “ppm” alone can also refer to mass fractions in other contexts. A liquid sample reported in mg/kg and a gas reported in µmol/mol cannot be compared numerically without conversion. The [BIPM SI Brochure](https://www.bipm.org/en/si-brochure-9) is the authoritative reference for units and quantity notation.

For a nearly ideal gas mixture:

```text
p_A = x_A P
c_A = n_A/V = x_A P/(R T)
rho_A = c_A M_A
```

`p_A` is partial pressure in Pa; `P` is total pressure in Pa; `c_A` is amount concentration in mol/m³; `T` is absolute temperature in K; `R = 8.314462618 J/(mol K)`; `M_A` is molar mass in kg/mol; and `rho_A` is mass concentration in kg/m³. The ideal-gas approximation is generally a useful starting point for dilute gases near ambient pressure. It is not a universal high-pressure equation of state.

Notice a subtle distinction. Keeping `x_A` constant while heating a gas at fixed pressure decreases its molecular concentration per cubic metre. A sensor controlled by molecular flux can change response even when the certified mixture's amount fraction is unchanged.

### Worked example 1: What does one ppm contain?

Use a hypothetical species with molar mass `60 g/mol`. At `298.15 K`, `101325 Pa`, and `x_A = 1 × 10^-6`:

```text
c_A = (1 × 10^-6)(101325)/(8.314462618 × 298.15)
    = 4.087 × 10^-5 mol/m³

rho_A = (4.087 × 10^-5)(0.060)
      = 2.452 × 10^-6 kg/m³
      = 2.452 mg/m³
```

A one-litre gas volume contains `4.087 × 10^-8 mol` of A, or approximately `2.46 × 10^16` molecules. A low amount fraction can therefore correspond to many molecules. Detection is difficult because only a small, noisy, and potentially biased fraction reaches an informative transduction event, not because the macroscopic sample necessarily contains fewer than one molecule.

These are constructed teaching values, not specifications for a particular analyte or device. Constants can be checked against [NIST's fundamental physical constants](https://www.nist.gov/pml/fundamental-physical-constants).

<a id="section-humidity-changes-both-the-sample-and-the-sensor"></a>

## Humidity changes both the sample and the sensor

Relative humidity is a ratio involving the saturation vapor pressure of water at the local temperature:

```text
RH = 100 p_water / p_sat(T)
```

It is not the mole fraction of water and not the amount of liquid water in a sample. The same water partial pressure can correspond to different relative humidities at different temperatures. If a warm, moist sample enters a cooler inlet, condensation can remove water and water-soluble compounds, change wall films, and alter transport.

Distinguish wet-basis amount fraction, which includes water in the denominator, from dry-basis amount fraction, which excludes it:

```text
x_A,dry = x_A,wet / (1 - x_water,wet)
```

This conversion only changes the accounting basis. It does not predict the chemical losses caused by physically drying the sample.

### Worked example 2: Wet and dry bases

A sample contains 4.0% water by amount and 2.00 µmol/mol of A on a wet basis. Its dry-basis amount fraction is:

```text
x_A,dry = 2.00/(1 - 0.040) = 2.083 µmol/mol
```

If an actual dryer removes 15% of A, the outlet would not retain this ideal dry-basis value. Under the simplified assumption that water removal is complete and other dry constituents are unchanged, the outlet becomes about `0.85 × 2.083 = 1.77 µmol/mol`. A mathematically correct basis conversion and a chemically lossy preparation step can operate simultaneously.

<a id="section-concentration-is-not-activity"></a>

## Concentration is not activity

Thermodynamics uses activity, a dimensionless measure of effective chemical availability relative to a chosen standard state. For a dissolved species, a common convention is:

```text
a_A = gamma_A c_A/c_standard
```

`gamma_A` is an activity coefficient. It approaches unity only under appropriate limiting conditions and conventions. Concentrated electrolytes, ionic liquids, mixed solvents, and strongly interacting species need more care. An electrode responding to activity can change voltage when the background composition changes even if an independently measured concentration stays constant.

This explains why “same concentration” does not always mean “same electrochemical environment.” Track matrix composition, temperature, and solvent condition along with the analyte. The next module develops the electrical consequences of activity.

<a id="section-data-sources-read-the-conditions-not-just-the-number"></a>

## Data sources: read the conditions, not just the number

The [NIST Chemistry WebBook](https://webbook.nist.gov/chemistry/) provides chemical identifiers, phase-change information, thermochemistry, spectra, and references to the underlying measurements. It is a starting point for constructing a physical-property record. Check isomer identity, phase, temperature range, pressure units, and the original data reference before using a value.

A boiling point is useful but does not directly give the concentration above a dilute solution. A vapor-pressure equation may describe a pure liquid rather than a compound dissolved in another liquid. A Henry-law constant may use water as the solvent rather than the material in your sensor. A value measured at one temperature should not silently become a universal constant.

For each imported datum, keep a small record containing its quantity definition, numerical value, units, conditions, uncertainty if available, source, and reason it applies. This is the beginning of reproducible sensor engineering.

<a id="section-uncertainty-and-significant-figures"></a>

## Uncertainty and significant figures

A measurement result is an estimate accompanied by uncertainty. Repeated readings quantify only part of the problem. Calibration standard uncertainty, flow error, blank contamination, temperature measurement, and sampling losses can remain even after hundreds of readings have been averaged.

For independent, sufficiently small input uncertainties, propagation through a differentiable model can be approximated using partial derivatives:

```text
y = f(q_1, q_2, ...)
u(y)^2 ≈ sum[(partial f/partial q_i)^2 u(q_i)^2]
```

Correlated inputs require covariance terms. The [JCGM uncertainty guides](https://www.bipm.org/en/committees/jc/jcgm/publications) explain the framework; uncertainty should be tied to a defined measurement model rather than added as an arbitrary percentage.

For `c_A = x_A P/(RT)`, suppose independent relative standard uncertainties are 2.0% in `x_A`, 0.5% in `P`, and 0.2% in `T`. The combined relative standard uncertainty is approximately `sqrt(2.0² + 0.5² + 0.2²)% = 2.07%`. Reporting eight meaningful digits in the resulting concentration would misrepresent the evidence.

<a id="section-common-mistakes-and-how-to-correct-them"></a>

## Common mistakes and how to correct them

| Mistake | Better engineering practice |
| --- | --- |
| Treating every gas signal as a VOC signal | Name the chemical species or explicitly define the measured aggregate. |
| Equating odor strength with mass concentration | Separate molecular measurement from a perceptual endpoint. |
| Reporting ppm without a basis | State amount fraction, mass fraction, wet/dry basis, and relevant conditions. |
| Treating drying as neutral preparation | Measure recovery and blank effects through the complete sampling path. |
| Using more digits to imply better measurement | Report uncertainty and sensible rounding. |
| Assuming a property database validates the whole sensor | Validate the device under the actual matrix and environmental conditions. |

<a id="section-design-decision-carried-forward"></a>

## Design decision carried forward

**Decision:** define what the complete instrument will measure and the conditions under which its output will be meaningful. **Criteria:** chemical identity or sample-class endpoint, amount-fraction basis, sample location, temporal resolution, and operating environment. **Evidence:** a property card from a public database and a list of quantities that require calibration.

**Artifact:** a one-page measurement requirements sheet with units, wet/dry basis, expected range, uncertainty target, and explicit non-goals. Add a block diagram separating sampling, transduction, and inference. Carry this sheet into the [design studio](../design-studio.md); later design choices must trace back to it.

<a id="section-problems-and-worked-answers"></a>

## Problems and worked answers

1. **Pressure change.** A 5 µmol/mol mixture is measured at the same temperature at 100 kPa and 80 kPa. How does its amount concentration change?

   **Answer:** `c_A` is proportional to `P`, so it falls to 80% of the first concentration. The amount fraction is still 5 µmol/mol. A calibration expressed only in amount fraction must account for any pressure sensitivity of the transducer.

2. **Missing units.** A paper lists a detection threshold of “0.5 ppm.” What must you recover before comparing it with a value in µg/m³?

   **Answer:** chemical identity and molar mass; whether ppm means amount or mass fraction; temperature and pressure for a gas conversion; wet/dry basis; and the statistical definition and conditions of the threshold. Unit conversion alone does not make thresholds comparable.

3. **Drying bias.** A 1.50 µmol/mol wet-basis sample has water fraction 0.03. An ideal dryer would produce what dry-basis value?

   **Answer:** `1.50/0.97 = 1.546 µmol/mol`, assuming no analyte loss. An observed outlet of 1.20 µmol/mol suggests loss or another model mismatch; the ratio `1.20/1.546 ≈ 0.776` is an apparent recovery under the stated assumptions.

4. **Design a property card.** Select a benign, publicly documented volatile compound in the NIST WebBook. Record identity, molecular mass, one phase-change datum, and its conditions. Explain why this is insufficient to predict a sensor response.

   **Answer guide:** the card lacks electrode kinetics, partitioning into the sensing material, interferent response, transport geometry, and instrumentation. Good property lookup narrows hypotheses; it does not replace calibration.

<a id="section-further-study"></a>

## Further study

Use the [annotated foundations reading list](../references/fundamentals.md) to find metrology references and formal terminology. Before proceeding, write a one-paragraph specification for a hypothetical classroom sensor that includes measurand, sample location, units, time resolution, operating conditions, and intended decision.

<!-- course-footer:start -->
---

[Previous: Getting started and prerequisite diagnostic](../getting-started.md) · [All modules](index.md) · [Next: Thermodynamics, redox, and electrode potential](02-thermodynamics-and-redox.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
