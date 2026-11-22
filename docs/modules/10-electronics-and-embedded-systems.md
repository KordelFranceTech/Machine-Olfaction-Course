---
layout: default
title: '10 · Electronics and embedded systems'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [**Modules**](index.md) · [Labs](../labs/index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Modules](index.md) / 10 · Electronics and embedded systems

**Module 10 of 18**

<!-- course-navigation:end -->

# 10 · Electronics and embedded systems

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Learning outcomes](#section-learning-outcomes)
- [1. Begin with a block diagram and a measurand](#section-1-begin-with-a-block-diagram-and-a-measurand)
- [2. A potentiostat controls a potential difference](#section-2-a-potentiostat-controls-a-potential-difference)
- [3. Current-to-voltage conversion and dynamic range](#section-3-current-to-voltage-conversion-and-dynamic-range)
- [4. Worked example: ADC resolution is one term](#section-4-worked-example-adc-resolution-is-one-term)
- [5. Worked example: thermal noise and bandwidth](#section-5-worked-example-thermal-noise-and-bandwidth)
- [6. Sampling, anti-aliasing, and impedance measurements](#section-6-sampling-anti-aliasing-and-impedance-measurements)
- [7. Embedded timing and a defensible data record](#section-7-embedded-timing-and-a-defensible-data-record)
- [8. Operating conditions and alerts](#section-8-operating-conditions-and-alerts)
- [9. Design decision carried forward](#section-9-design-decision-carried-forward)
- [10. Exercises and worked answers](#section-10-exercises-and-worked-answers)

</details>
<!-- course-toc:end -->

An electrochemical measurement is a controlled interaction with a material followed by an electrical observation. The electronics must keep the intended conditions sufficiently stable, measure a small signal without changing it excessively, and preserve enough context to interpret the result. A high-resolution converter alone cannot achieve these goals.

**Level and time:** upper-division undergraduate; 6–8 hours. **Prerequisites:** operational amplifiers, basic feedback, sampling theory, [electrode interfaces](04-electrode-interfaces.md), and [electrochemical methods](06-electrochemical-methods.md).

<a id="section-learning-outcomes"></a>

## Learning outcomes

- Explain the distinct roles of a potentiostat, transimpedance amplifier, ADC, and processor.
- Derive current-to-voltage conversion and a simple noise budget.
- Identify saturation, reference instability, leakage, aliasing, and timing failures.
- Specify a measurement instrument from range, noise, timing, and calibration requirements.
- Separate analytical output, quality status, and user notification.

<a id="section-1-begin-with-a-block-diagram-and-a-measurand"></a>

## 1. Begin with a block diagram and a measurand

A generic instrument can be decomposed as:

```text
command / waveform -> control loop -> electrochemical cell
                            ^                  |
                      reference sense         current
                                               |
                      analog filter <- current-to-voltage stage
                            |
                           ADC -> timestamped record -> estimation
                                                        |
                                             quality / result / alert
```

The current-to-voltage stage is normally called a transimpedance amplifier, or TIA. The analog front end, or AFE, may integrate several blocks. A processor schedules measurements and interprets data but cannot undo every error introduced before conversion.

The [Texas Instruments LMP91000 datasheet](https://www.ti.com/lit/ds/symlink/lmp91000.pdf) is a public example of a configurable electrochemical AFE. The [Analog Devices AD5940 product documentation](https://www.analog.com/en/products/ad5940.html) illustrates integration of excitation and measurement functions for several electrochemical techniques. Study these as examples of architecture and specification language, not as endorsements or as proof that a particular sensing material will work.

A design specification starts from expected current and impedance ranges, required bandwidth, acceptable uncertainty, electrode configuration, and allowable excitation. Those requirements determine circuit choices. Starting with a convenient converter and then asserting that its bit depth defines chemical sensitivity reverses the engineering logic.

<a id="section-2-a-potentiostat-controls-a-potential-difference"></a>

## 2. A potentiostat controls a potential difference

In a conventional three-electrode arrangement, a control amplifier drives the counter electrode so that the working-electrode potential relative to the reference electrode follows the commanded value. The reference input should draw little current. The counter electrode supplies the current needed by the working-electrode process.

A real control loop has finite bandwidth, output swing, current capacity, and phase margin. A large solution resistance can force the counter-electrode driver toward a supply rail. A disconnected reference electrode can produce an apparently stable but meaningless voltage. Interfacial capacitance and cable capacitance add dynamics that matter for stability.

Two-electrode measurements can be appropriate in some systems, but the measured or controlled voltage includes both electrode interfaces and solution contributions. State what voltage is actually known. A programmed terminal voltage should not automatically be described as an absolute interfacial potential.

The application note [AN-1563: Optimizing the AD5940 for Electrochemical Measurements](https://www.analog.com/en/resources/app-notes/an-1563.html) is useful for seeing how a real AFE implements measurement paths and calibration. Its device-specific capabilities do not remove the need to validate the complete cell and wiring arrangement.

<a id="section-3-current-to-voltage-conversion-and-dynamic-range"></a>

## 3. Current-to-voltage conversion and dynamic range

For an ideal inverting TIA referenced to a midpoint voltage `V_mid`:

```text
V_out = V_mid - I_in R_f

I_in: A
R_f: ohm
V_out and V_mid: V
```

The sign depends on the current convention. State it in the data schema so that an anodic current does not become “negative concentration” merely because another implementation uses the opposite sign.

A larger feedback resistance produces a larger voltage for the same current. It also reduces the maximum current that fits within the output range and interacts with input capacitance and amplifier bandwidth. A feedback capacitor can help control bandwidth and stability, but its value must be justified by the complete circuit. The [Analog Devices discussion of TIA noise](https://www.analog.com/en/resources/technical-articles/transimpedance-amplifier-noise-considerations.html) explains why amplifier current noise, voltage noise, input capacitance, and feedback resistance all matter.

Leakage is especially important at small currents. Moisture, contamination, insulation, connectors, and board surfaces can provide unintended current paths. Guarding and shielding serve different purposes: a guard reduces leakage-driving voltage across insulation; a shield reduces coupling from external electric fields. Neither substitutes for a clean, characterized measurement assembly.

<a id="section-4-worked-example-adc-resolution-is-one-term"></a>

## 4. Worked example: ADC resolution is one term

Use these invented classroom values: `R_f = 1.0 MΩ`, an ADC span of `2.5 V`, and `16 bits`. Ignore offset and headroom initially.

```text
voltage per code = 2.5 / 2^16 = 38.15 microvolt
current per code = 38.15 microvolt / 1.0 megohm = 38.15 pA

A 10 nA current change produces:
Delta_V = 10 nA × 1.0 megohm = 10 mV
code change ≈ 10 mV / 38.15 microvolt = 262 codes
```

This is a nominal quantization increment, not the instrument's detection limit. Suppose the usable swing around the midpoint is only `±1.0 V`. Then the ideal current range is `±1.0 µA`, not whatever range is obtained by using the full supply voltage in the calculation. An offset or charging transient can consume that headroom before the target signal arrives.

If gain is switched during a measurement, record the gain and settling interval. Concatenating raw ADC codes across gain settings can create false chemical transients. If saturation occurs, label the samples invalid or censored according to a predefined rule; clipping is not a reliable high-concentration measurement.

<a id="section-5-worked-example-thermal-noise-and-bandwidth"></a>

## 5. Worked example: thermal noise and bandwidth

At temperature `T`, a feedback resistor has an equivalent input current-noise density:

```text
i_R = sqrt(4 k_B T / R_f)  [A / sqrt(Hz)]
i_R,rms = i_R sqrt(B_ENBW)
```

`B_ENBW` is the equivalent noise bandwidth, not automatically the cutoff frequency. For a single-pole low-pass filter, `B_ENBW = (pi/2) f_c` when integrating a one-sided white-noise density from zero frequency.

For `T = 300 K`, `R_f = 1 MΩ`, and an illustrative `B_ENBW = 10 Hz`:

```text
i_R = sqrt(4 × 1.380649e-23 × 300 / 1e6)
    = 0.129 pA / sqrt(Hz)
i_R,rms = 0.407 pA
```

For comparison, if the previous ADC's quantization error could be modeled as independent uniform noise, its input-referred RMS value would be `38.15/sqrt(12) = 11.0 pA`. That assumption requires appropriate signal variation or dithering; static quantization error is not always independent random noise.

A real budget adds amplifier noise, reference noise, electromagnetic interference, electrode fluctuations, and drift. Independent random terms combine in quadrature. Correlated errors require covariance terms. Averaging can reduce independent noise but does not remove a calibration bias or a slowly drifting reference. A calculation showing a low resistor noise floor cannot establish a low chemical detection limit.

<a id="section-6-sampling-anti-aliasing-and-impedance-measurements"></a>

## 6. Sampling, anti-aliasing, and impedance measurements

An ADC samples the analog waveform that reaches it. Frequencies above half the sample rate can alias into the recorded band unless sufficiently attenuated. A digital filter applied afterward cannot uniquely identify which analog frequency produced an aliased sample sequence.

For example, a `63 Hz` sinusoid sampled at `100 samples/s` can appear at `37 Hz`. If the chemical dynamics occupy only a few hertz, the analog front end should be designed to reject unwanted higher-frequency content while preserving the relevant response. Merely saving fewer points after a high-rate acquisition is not equivalent to antialias filtering.

Impedance measurements additionally require amplitude and phase accuracy. Excitation, current conversion, filtering, and channel delays can all contribute frequency-dependent errors. A calibration using known electrical loads tests the electrical measurement path. It does not validate an equivalent-circuit interpretation of a changing chemical interface. Conversely, a plausible semicircle in a plot does not prove that the electronics measured phase correctly.

The AFE's maximum advertised frequency is not a promise of equal uncertainty across every load and frequency. Read the conditions attached to specifications and verify performance in the intended range.

<a id="section-7-embedded-timing-and-a-defensible-data-record"></a>

## 7. Embedded timing and a defensible data record

Distinguish the time a measurement was requested, the time it was acquired, and the time it was received by another device. Wireless or USB arrival times may vary even when acquisition timing is stable. Use a monotonic acquisition clock for intervals and a documented mapping to wall-clock time when needed.

Each data record should carry the channel identity, sample counter, acquisition timestamp, units, gain, excitation state, module identity, and relevant quality flags. Missing samples must remain distinguishable from measured zeros. Calibration coefficients and firmware revisions should be associated with the result they produced.

For multiple channels, determine whether they are sampled simultaneously or multiplexed. A multiplexed sequence can create apparent timing differences between sensors that are actually acquisition offsets. Switching also creates settling requirements and possible cross-talk. If a model uses transient timing as a feature, these details are part of the scientific measurement.

<a id="section-8-operating-conditions-and-alerts"></a>

## 8. Operating conditions and alerts

A portable enclosure constrains power, heat, size, and maintenance. It also changes the measurement environment: a warm battery, a processor burst, or a radio transmission can alter temperature or electrical noise. A replaceable module adds connector and calibration states. These are reasons to measure system behavior under realistic operating modes.

Use separate states for **valid measurement**, **target decision**, and **instrument fault**. A low-battery or disconnected-reference condition must not silently produce a reassuring “target absent” display. Conversely, a transient ADC overflow is not sufficient evidence of a target.

A conceptual state machine might be:

```text
INITIALIZING -> QUALITY_CHECK -> READY -> ACQUIRING -> EVALUATING
                     |                        |             |
                    FAULT                    FAULT      RESULT_READY
```

Alerts should communicate what the evidence supports: a measured threshold exceeded, a sample invalid, or maintenance required. A chemical measurement does not by itself justify a medical diagnosis. Threshold hysteresis can prevent rapid toggling near a boundary, but it changes timing and must be included in validation.

<a id="section-9-design-decision-carried-forward"></a>

## 9. Design decision carried forward

In the [design studio](../design-studio.md), choose an instrument architecture from the required electrical range and sampling task. Compare an integrated AFE with a discrete implementation; compare fixed gain with carefully logged gain switching; compare continuous sensing with duty-cycled operation. Your deliverable is a block diagram, a one-page error budget, a channel-timing diagram, and a state table for normal and invalid measurements. Evidence required before progression includes electrical dummy-load checks, range and saturation checks, measured timing, and, where interchangeability is part of the selected public design, verification that replacement selects the correct calibration. These establish an instrument pathway, not analyte selectivity or clinical utility.

<a id="section-10-exercises-and-worked-answers"></a>

## 10. Exercises and worked answers

1. **Gain selection.** A maximum expected current is `2 µA`, and allowable output change is `0.8 V`. What is the largest ideal feedback resistance? **Answer:** `0.8/(2e-6) = 400 kΩ`; leave additional margin for transients and offsets.
2. **Leakage.** An unintended `10 GΩ` path spans `1 V`. What current does it contribute? **Answer:** `100 pA`, larger than several ideal noise terms in the examples.
3. **Aliasing.** What lower frequency can a `95 Hz` interference resemble when sampled at `100 samples/s`? **Answer:** `5 Hz`, directly inside many slow-sensing bands.
4. **Averaging.** Independent white-noise RMS is `8 pA`. How many independent samples reduce the mean's RMS to `2 pA`? **Answer:** `N = (8/2)^2 = 16`. Correlated samples do not provide the same reduction.
5. **Fault logic.** A reference wire disconnects and the ADC becomes constant. Should a flat trace be classified as a clean blank? **Answer:** no. Independent quality checks must establish valid electrical operation before chemical interpretation.

<!-- course-footer:start -->
---

[Previous: 09 · Sample storage and modularity](09-sample-storage-and-modularity.md) · [All modules](index.md) · [Next: 11 · Calibration and uncertainty](11-calibration-and-uncertainty.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
