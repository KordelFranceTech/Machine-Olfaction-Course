---
layout: default
title: '09 · Sample storage and modularity'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [**Modules**](index.md) · [Labs](../labs/index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Modules](index.md) / 09 · Sample storage and modularity

**Module 09 of 18**

<!-- course-navigation:end -->

# 09 · Sample storage and modularity

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Learning outcomes](#section-learning-outcomes)
- [1. A container is part of the measurement](#section-1-a-container-is-part-of-the-measurement)
- [2. Four processes that must not be confused](#section-2-four-processes-that-must-not-be-confused)
- [3. Worked example: a holding-time criterion](#section-3-worked-example-a-holding-time-criterion)
- [4. Compressible reservoirs change the flow problem](#section-4-compressible-reservoirs-change-the-flow-problem)
- [5. Worked example: connector dead volume](#section-5-worked-example-connector-dead-volume)
- [6. Modularity is an agreement between subsystems](#section-6-modularity-is-an-agreement-between-subsystems)
- [7. Keep a usable history record](#section-7-keep-a-usable-history-record)
- [8. Validation matrix and acceptance logic](#section-8-validation-matrix-and-acceptance-logic)
- [Design decision carried forward](#section-design-decision-carried-forward)
- [9. Exercises and worked answers](#section-9-exercises-and-worked-answers)

</details>
<!-- course-toc:end -->

Collecting gas and measuring it later separates two engineering tasks: preserving the sample and interpreting the detector. That separation can make measurements practical, but it introduces a clock. A sealed container is a chemical environment, not a frozen record of the atmosphere. Replaceable sensing modules introduce a second boundary: the system must know which physical component, calibration, and history produced each result.

**Level and time:** upper-division undergraduate; 5–7 hours. **Prerequisites:** [sampling and fluidics](07-sampling-and-fluidics.md), [humidity and conditioning](08-humidity-filtration-and-conditioning.md), gas laws, and first-order differential equations.

<a id="section-learning-outcomes"></a>

## Learning outcomes

- Distinguish pressure leakage, permeation, adsorption, reaction, and outgassing.
- Calculate simple holding-time and dilution limits with explicit assumptions.
- Explain how compressible reservoirs and one-way valves affect delivery.
- Design a modular interface specification spanning mechanics, chemistry, electronics, and data.
- Construct a sample-history record and a defensible acceptance decision.

<a id="section-1-a-container-is-part-of-the-measurement"></a>

## 1. A container is part of the measurement

Consider a nominal concentration `c_0` at collection. The later value can be changed by loss to walls, release from walls, permeation, leaks, gas-phase chemistry, and water redistribution. Some mechanisms remove target molecules; others add chemically indistinguishable molecules from contamination. A blank and a recovery test are therefore complementary.

A useful teaching balance for a rigid, well-mixed, constant-volume container is:

```text
V dc/dt = -k_loss V c + r_background + Q_leak(c_out - c)

V: m^3
c, c_out: mol m^-3
k_loss: s^-1
r_background: mol s^-1
Q_leak: m^3 s^-1
```

This assumes that the leak exchanges equal volumes at approximately constant conditions. It is not a general model for an evacuated canister filling from the environment. It also lumps several chemical processes into `k_loss`; that parameter can depend on concentration, humidity, temperature, and surface history.

If background and leakage vanish, `c(t) = c_0 exp(-k_loss t)`. If background is present, a sample can initially decline and later approach a nonzero plateau. Such a plateau should not be mistaken for a stable original sample.

Original storage studies demonstrate why broad labels such as “inert bag” are insufficient. [Mochalski et al.](https://doi.org/10.1039/C2AN36193K) compared multiple polymer containers for 41 breath-related compounds and found that sample integrity depended on the material and filling conditions. [Beauchamp et al.](https://doi.org/10.1088/1752-7155/2/4/046001) likewise documented compound-dependent changes during storage. Their findings motivate compound-specific validation, not a universal allowable holding time.

<a id="section-2-four-processes-that-must-not-be-confused"></a>

## 2. Four processes that must not be confused

**Leakage** is bulk flow through an unintended opening. It often responds strongly to pressure difference. A pressure-decay test can help detect it, but only within the sensitivity and conditions of the test.

**Permeation** is molecular transport through a material. A container can hold pressure while allowing an analyte to diffuse through its wall. Permeation depends on solubility in the material, diffusion within it, thickness, area, and the concentration gradient.

**Adsorption and absorption** store molecules on a surface or within a material. Reversible storage can suppress the first exposure and contaminate the next. The relevant wall capacity relative to the gas inventory often grows as surface-to-volume ratio increases.

**Outgassing and reaction** create or transform chemical species. A pristine-looking component may release manufacturing residues. A cleaning agent can become an interferent. Oxygen, moisture, and light can change the chemistry during storage.

An idealized membrane expression illustrates permeation:

```text
molar transfer rate = (permeability × area / thickness) × partial-pressure difference
```

Permeability units must match the expression used. Do not combine a value stated in a customary polymer unit with SI dimensions without conversion. A steady-state permeability calculation also omits the initial diffusion lag through the wall.

<a id="section-3-worked-example-a-holding-time-criterion"></a>

## 3. Worked example: a holding-time criterion

Suppose an independently characterized hypothetical analyte decays with `k_loss = 0.015 h^-1` in a specified storage system. The analytical requirement is at least 95% recovery from storage loss alone.

```text
c(t)/c_0 = exp(-0.015 t) >= 0.95
t <= -ln(0.95)/0.015 = 3.42 h
```

At eight hours, the model predicts `exp(-0.12) = 88.7%` recovery. A system advertised simply as “usable overnight” would not meet this particular 95% criterion. Yet 3.42 h is only a model-based limit: uncertainty in `k_loss`, background, and concentration dependence must be considered before it becomes an operating requirement.

Now add a constant background source equal to `0.5 concentration-units/h`, with `c_0 = 20 units`. The solution is:

```text
c(t) = c_0 exp(-k t) + (b/k)[1 - exp(-k t)]
b/k = 0.5/0.015 = 33.3 units
```

The measured concentration rises despite simultaneous target loss. A recovery calculation could look reassuring while the sample is being replaced by container background. The distinction requires a matched blank and a chemically appropriate reference, not just repeated readings of the same bag.

<a id="section-4-compressible-reservoirs-change-the-flow-problem"></a>

## 4. Compressible reservoirs change the flow problem

A flexible reservoir can deliver gas without a large pressure swing if it collapses smoothly as gas leaves. In the ideal well-mixed, nonreactive limit, removal of gas with the same composition as the reservoir does not change the remaining mole fraction. It reduces the number of molecules available.

Real reservoirs can fold, occlude outlets, or change their surface-to-volume ratio as they empty. Manual compression produces time-varying pressure and flow. If sensor response depends on delivery rate, an operator's handling can become a hidden predictor. A compressible compartment therefore does not guarantee constant flow or constant concentration at the detector.

For a rigid container, `PV = nRT` connects sample withdrawal to pressure. A change in pressure can also affect leaks, valve opening, and detector response. Engineering comparisons should state whether flow is actively regulated, pressure-driven, or produced by reservoir compression.

A one-way valve adds directionality but not perfect isolation. Important properties include opening pressure, reverse leakage, flow resistance, hysteresis, dead volume, and chemical compatibility. “One-way” is a functional category, not a claim that no molecule can ever travel backward. A valve can mechanically work while contaminating the gas that passes through it.

<a id="section-5-worked-example-connector-dead-volume"></a>

## 5. Worked example: connector dead volume

A connector contains `0.20 mL` of surrounding gas before attachment. A collected sample contributes `2.00 mL`. Assume complete mixing, the same pressure and temperature, and no chemical loss. Let target concentration be `100 ppb` in the sample and `5 ppb` in the connector.

```text
c_mix = (2.00 × 100 + 0.20 × 5)/(2.00 + 0.20)
      = 91.36 ppb
```

The apparent target reduction is 8.64%, even though neither the container nor the sensor removed a molecule. A low-concentration sample can suffer the opposite error if the connector contains a higher concentration than the sample.

Now a sensing chamber draws `20 mL/min` for `30 s`, requiring `10 mL`. A reservoir with `8 mL` of usable volume cannot sustain that nominal exposure. The engineering response is to revise the duration, flow, or sample volume and validate the resulting measurement. Silently substituting a shorter trace may change the model's input distribution.

For a variable-flow reservoir, calculate delivered amount by integrating molar flow over time. A single nominal flow and a start/stop timestamp can miss substantial underdelivery.

<a id="section-6-modularity-is-an-agreement-between-subsystems"></a>

## 6. Modularity is an agreement between subsystems

A replaceable sensing cartridge is useful only if the host can interpret it correctly. Mechanical fit is one part of that agreement.

| Interface | Questions the specification must answer |
| --- | --- |
| Mechanical | Does attachment seal reproducibly? Can partial insertion be detected? |
| Fluidic | What are dead volume, resistance, direction, and allowable pressure? |
| Chemical | What backgrounds and recoveries are acceptable after storage and use? |
| Electrical | What connections, ranges, isolation, and fault states are supported? |
| Calibration | Which coefficients apply to this unit and operating range? |
| Digital | How are identity, units, timestamps, revisions, and invalid states represented? |
| Operational | What establishes replacement, expiration, or failed quality control? |

A shared connector does not make two modules analytically interchangeable. Manufacturing variation can change area, film thickness, resistance, or sensitivity. The base instrument must either use a justified common calibration or load an appropriate module-specific calibration. Changing the module should not silently preserve coefficients fitted to a previous unit.

The [BIPM's JCGM publications](https://www.bipm.org/en/committees/jc/jcgm/publications) provide metrological vocabulary and uncertainty frameworks for distinguishing a device identity from a valid measurement result. Traceability concerns the result and its documented calibration chain, not merely the existence of a serial number.

<a id="section-7-keep-a-usable-history-record"></a>

## 7. Keep a usable history record

A sample record should allow an independent analyst to reconstruct the important transformations. For a classroom design exercise, use pseudonymous identifiers and synthetic values:

```text
sample_id: teaching-sample-017
collection_start / collection_end: recorded with timezone
container_id and material lot: recorded
initial volume or collection flow integral: recorded
pressure / temperature / humidity: measured where relevant
conditioning state and component identifiers: recorded
storage interval and temperature history: recorded
module_id and calibration_revision: recorded
acquisition clock and firmware_revision: recorded
quality_control_result: pass / fail / indeterminate, with reason
```

This is a schema example, not a request to collect human data. The value of each field should be justified by a possible bias or decision. Avoid accumulating identifiers that do not help the scientific purpose. A container label can support chain of custody while a separate access-controlled record handles sensitive context.

A calibration revision should be immutable once used for a reported result. If a correction is necessary, preserve the original result and record how the revised one was computed. Without that distinction, a software update can make historical data impossible to reproduce.

<a id="section-8-validation-matrix-and-acceptance-logic"></a>

## 8. Validation matrix and acceptance logic

An efficient validation design varies factors that are plausibly coupled: container material, fill fraction, storage duration, humidity, concentration, and repeated-use history. Include blanks, independent reference samples, and enough replicates to quantify variability. A small exploratory matrix can identify dominant factors before a larger confirmatory study.

The [EPA Method TO-15A resource](https://www.epa.gov/amtic/compendium-methods-determination-toxic-organic-compounds-ambient-air) offers a mature example of linking sampling vessels with cleanliness and analytical performance. Its method-specific requirements should inform the questions asked, not be presented as certification of a different device.

Acceptance criteria should be specified before examining the final validation data. Possible criteria include recovery range, blank contribution, maximum uncertainty, and timing error. An output can be indeterminate because the sample history is incomplete even if the sensor trace looks clean. “No reliable result” is a valid system state.

<a id="section-design-decision-carried-forward"></a>

## Design decision carried forward

For the [design studio](../design-studio.md), audit one independently published container or connection study, or compare synthetic storage-loss models. Document measurement conditions, recovery, blanks, timing, and uncertainty. Your artifact is a source-based evidence table and a sensitivity analysis identifying the most informative follow-up measurement. Any physical implementation must follow the selected public design and its applicable requirements. Storage and serviceability remain separate optional studies unless the student's own application establishes a need to combine them.

<a id="section-9-exercises-and-worked-answers"></a>

## 9. Exercises and worked answers

1. **First-order loss.** A hypothetical sample retains 90% after five hours. Estimate `k` and the time to 98% recovery. **Answer:** `k = -ln(0.90)/5 = 0.0211 h^-1`; `t_98 = -ln(0.98)/k = 0.959 h` under the same model and conditions.
2. **Pressure versus chemistry.** A container passes a pressure-hold test but loses a target compound. **Answer:** permeation, sorption, or reaction can cause chemical loss without detectable bulk leakage.
3. **Valve selection.** Two one-way valves have the same opening pressure. Are they interchangeable? **Answer:** no. Reverse leakage, resistance, dead volume, materials, contamination, and cycling behavior also matter.
4. **Calibration identity.** A replacement module produces twice the baseline current of the previous one but the same standard-gas increment. Must its sensitivity be halved? **Answer:** no. Baseline and sensitivity are different parameters. Re-establish calibration and operating validity rather than infer slope from offset.
5. **Design deliverable.** Draft an acceptance policy for a stored sample with an unknown storage temperature. **Answer criterion:** state which performance assumptions depend on temperature and whether available evidence permits a result. Do not fill missing history with the nominal laboratory temperature.

<!-- course-footer:start -->
---

[Previous: 08 · Humidity, filtration, and conditioning](08-humidity-filtration-and-conditioning.md) · [All modules](index.md) · [Next: 10 · Electronics and embedded systems](10-electronics-and-embedded-systems.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
