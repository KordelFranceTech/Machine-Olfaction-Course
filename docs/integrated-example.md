---
layout: default
title: 'Integrated worked example: from a gas input to a valid reading'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](index.md) · [Start](getting-started.md) · [Modules](modules/index.md) · [Labs](labs/index.md) · [**Projects**](projects/index.md) · [Library](references/index.md) · [Site map](navigation.md)

[Course home](index.md) / [Projects](projects/index.md) / Integrated worked example: from a gas input to a valid reading

<!-- course-navigation:end -->

# Integrated worked example: from a gas input to a valid reading

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Interface contract](#section-interface-contract)
- [Complete runnable example](#section-complete-runnable-example)
- [What to observe](#section-what-to-observe)
- [Experiments that turn the example into engineering](#section-experiments-that-turn-the-example-into-engineering)
- [Design artifact](#section-design-artifact)

</details>
<!-- course-toc:end -->

The individual labs study different parts of the instrument. This example connects them through explicit interfaces and units. It is a **fully synthetic teaching system**: the transduction coefficients, recovery, time constants, and operating values are invented. They do not describe a demonstrated sensing chemistry or a commercial device.

The example's purpose is to show what an integrated model must specify. It is not evidence of molecular selectivity, an electrochemical operating recipe, or a clinical classifier.

<a id="section-interface-contract"></a>

## Interface contract

| Stage | Input | Output | Assumption |
| --- | --- | --- | --- |
| Sample path | Inlet mole fraction in ppm | Chamber gas-equivalent concentration in ppm | First-order turnover with fixed recovery |
| Sensing dynamics | Chamber concentration | Effective sensed concentration in ppm | First-order lag; no chemical species discrimination |
| Transduction | Effective concentration and RH in percent | Current in A | Invented linear constitutive relation |
| Readout | Current | Voltage in V | Ideal inverting TIA around a bias voltage |
| Digitization | Voltage | Unsigned integer code and clipping status | Ideal finite-resolution ADC |
| Interpretation | Code, calibration, RH, and quality flags | Effective concentration or invalid result | Known calibration, correct units, valid hardware |

An effective sensed concentration is a model state. It is not an assertion that gas and liquid concentrations share the same numerical value. A real gas-to-liquid interface requires a partition model and a physically validated response relationship. Here those complexities are deliberately replaced by a declared synthetic transduction law.

```text
I = b + g*c_effective + h*(RH - RH_reference)
V = V_bias - R_feedback*I
ADC_code = round(V/V_span * (2^N - 1)), if V lies inside the ADC range
c_est = [(V_bias - V_digitized)/R_feedback - b - h*(RH-RH_reference)]/g
```

The simulator knows the inlet history for evaluation. The inversion function never receives that truth. Its estimate is of the delayed effective state. Dividing by sample-path recovery estimates inlet concentration only after equilibration under this model; it cannot undo a transient simply by multiplication.

<a id="section-complete-runnable-example"></a>

## Complete runnable example

This block requires only Python's standard library and writes no files. It uses the exact two-stage response over each interval with constant inlet concentration. The time constants differ; the equal-time-constant limit would need its own expression.

```python
from math import exp

DT = 0.5
TAU_CHAMBER = 2.0
TAU_SENSOR = 4.0
RECOVERY = 0.90
BASELINE_A = 5e-9
GAIN_A_PER_PPM = 8e-9
HUMIDITY_A_PER_PERCENT = 0.08e-9
RH_REFERENCE = 50.0
R_FEEDBACK_OHM = 2e6
V_BIAS = 1.2
V_SPAN = 2.4
ADC_MAX = 2**16 - 1


def advance(chamber, sensor, inlet_ppm):
    target = RECOVERY * inlet_ppm
    a = exp(-DT/TAU_CHAMBER)
    b = exp(-DT/TAU_SENSOR)
    new_chamber = target + (chamber-target)*a
    new_sensor = (target + (sensor-target)*b
                  + (chamber-target)*TAU_CHAMBER
                  /(TAU_CHAMBER-TAU_SENSOR)*(a-b))
    return new_chamber, new_sensor


def acquire(sensor_ppm, rh_percent, connected=True, overrange=False):
    if not connected:
        return None, "FAULT"
    current = (BASELINE_A + GAIN_A_PER_PPM*sensor_ppm
               + HUMIDITY_A_PER_PERCENT*(rh_percent-RH_REFERENCE))
    if overrange:
        current = 2e-6  # Injected electronics test fault, not chemistry.
    voltage = V_BIAS - R_FEEDBACK_OHM*current
    if not 0.0 <= voltage <= V_SPAN:
        return None, "CLIPPED"
    return round(voltage/V_SPAN*ADC_MAX), "VALID"


def infer(code, quality, rh_percent):
    if quality != "VALID" or code is None:
        return None
    measured_voltage = code/ADC_MAX*V_SPAN
    current = (V_BIAS-measured_voltage)/R_FEEDBACK_OHM
    return (current-BASELINE_A
            - HUMIDITY_A_PER_PERCENT*(rh_percent-RH_REFERENCE)) / GAIN_A_PER_PPM


chamber = sensor = 0.0
largest_error = 0.0
fault_states = []
print("time_s inlet_truth_ppm effective_ppm estimate_ppm status")
for step in range(1, int(60/DT)+1):
    t = step*DT
    interval_start = t-DT
    inlet = 2.0 if 10.0 <= interval_start < 40.0 else 0.0
    rh = 60.0 if 20.0 <= t < 40.0 else 50.0
    chamber, sensor = advance(chamber, sensor, inlet)
    code, quality = acquire(sensor, rh, connected=(t != 28.0),
                            overrange=(t == 45.0))
    estimate = infer(code, quality, rh)
    if estimate is not None:
        largest_error = max(largest_error, abs(estimate-sensor))
    else:
        fault_states.append((t, quality))
    if t in {5.0, 10.0, 20.0, 28.0, 35.0, 40.0, 45.0, 55.0, 60.0}:
        shown = "None" if estimate is None else f"{estimate:.4f}"
        print(f"{t:6.1f} {inlet:15.1f} {sensor:13.4f} {shown:>12} {quality}")

half_code_error_ppm = V_SPAN/ADC_MAX/2/R_FEEDBACK_OHM/GAIN_A_PER_PPM
assert largest_error <= half_code_error_ppm + 1e-12
assert fault_states == [(28.0, "FAULT"), (45.0, "CLIPPED")]
print(f"largest quantization error: {largest_error:.6f} ppm")
print(f"half-code theoretical bound: {half_code_error_ppm:.6f} ppm")
```

<a id="section-what-to-observe"></a>

## What to observe

The inlet steps to 2 ppm, but the effective signal approaches 1.8 ppm because of the invented 90% recovery. The two dynamic stages delay the rise and produce a tail after the inlet returns to zero. At 28 s, disconnection yields no concentration. At 45 s, a deliberately excessive current yields a clipped status and no concentration. Neither becomes a numeric zero or a confident negative.

At 20 s, the humidity term changes the raw current. Because this synthetic model supplies the exact coefficient and an error-free RH measurement, the inverse removes that term. This ideal success is a useful baseline for deliberately breaking the assumptions. It is not evidence that humidity compensation is easy in a real device.

The quantization-only error bound is approximately 0.001144 ppm of the effective state. It is emphatically not a detection limit: the model contains no analog noise, calibration uncertainty, cross-sensitivity, reference instability, reference-concentration uncertainty, or material drift.

<a id="section-experiments-that-turn-the-example-into-engineering"></a>

## Experiments that turn the example into engineering

1. **Humidity-model error:** use an incorrect humidity coefficient only in `infer`. Quantify the apparent target change at the humidity transition.
2. **Calibration transfer:** change the true gain in `acquire` while leaving the calibration fixed. Distinguish offset and gain errors.
3. **Common-mode drift:** add the same changing current offset to several channels. Show why averaging does not remove it.
4. **Unknown interferent:** add a second response contribution in `acquire` that the inverse does not model. Determine which extra independent measurement would be needed to resolve it.
5. **Adaptive sampling:** alter the inlet history or chamber timescale and compare decision latency. Keep all changes and power implications explicit.
6. **Quality logic:** distinguish hardware validity from a steady-state condition. A valid transient measurement can still be inappropriate for steady-state inlet quantitation.
7. **Parameter uncertainty:** propagate recovery and calibration uncertainty rather than reporting the quantization bound as total uncertainty.

<a id="section-design-artifact"></a>

## Design artifact

Create a version of the interface table for your project. Each boundary must specify physical meaning, unit, reference condition, timing, uncertainty, and invalid-state behavior. Replace a synthetic relationship with a measured one only when the new evidence supports the substitution. This is how separate subsystem demonstrations become a coherent instrument.

[Continue the physical build ladder](build-ladder.md) · [Choose a derivative project](derivative-projects.md)

<!-- course-footer:start -->
---

[Previous: Design studio: derive an integrated sensing system](design-studio.md) · [Project routes](projects/index.md) · [Next: Build ladder: from models to a physical demonstrator](build-ladder.md)

[Back to top](#page-top) · [Site map](navigation.md) · [Course home](index.md)
<!-- course-footer:end -->
