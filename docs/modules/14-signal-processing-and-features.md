---
layout: default
title: '14. Signal processing, time response, and features'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [**Modules**](index.md) · [Labs](../labs/index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Modules](index.md) / 14. Signal processing, time response, and features

**Module 14 of 18**

<!-- course-navigation:end -->

# 14. Signal processing, time response, and features

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Learning outcomes](#section-learning-outcomes)
- [The measurement chain as a sequence of transformations](#section-the-measurement-chain-as-a-sequence-of-transformations)
- [Baselines are measurements, not constants of nature](#section-baselines-are-measurements-not-constants-of-nature)
- [First-order dynamics: useful model, limited interpretation](#section-first-order-dynamics-useful-model-limited-interpretation)
- [Sampling and aliasing](#section-sampling-and-aliasing)
- [Filtering trades variance for temporal detail](#section-filtering-trades-variance-for-temporal-detail)
- [Features should express a testable hypothesis](#section-features-should-express-a-testable-hypothesis)
- [Impedance features and model fitting](#section-impedance-features-and-model-fitting)
- [Evaluation of the entire signal pipeline](#section-evaluation-of-the-entire-signal-pipeline)
- [Design decision carried forward](#section-design-decision-carried-forward)
- [Problems and worked answers](#section-problems-and-worked-answers)

</details>
<!-- course-toc:end -->

The electrical signal is already the output of a physical filter. Molecules take time to travel, partition, react, and leave; electrodes and amplifiers have their own dynamics. Digital filtering adds another layer. A cleaner plot is useful only if the processing preserves the information required for the decision and if its delay is included in the system model.

**Prerequisites:** basic circuits, sampling, uncertainty propagation, and the electrochemical methods module. **Suggested effort:** 3 hours of study and 2 hours of computation.

<a id="section-learning-outcomes"></a>

## Learning outcomes

- Separate physical response dynamics, sampling effects, and digital processing.
- Choose baseline, amplitude, kinetic, and spectral features with explicit units.
- Compute filter delay and propagate uncertainty through a normalized response.
- Explain why noncausal processing cannot support a real-time latency result.
- Build an auditable transformation from raw measurements to a feature vector.

<a id="section-the-measurement-chain-as-a-sequence-of-transformations"></a>

## The measurement chain as a sequence of transformations

```text
sample concentration at inlet
    -> transport and mixing
    -> interfacial dynamics
    -> electrical readout and analog filter
    -> sampled measurements with timestamps
    -> quality checks and baseline estimation
    -> causal processing or explicitly offline processing
    -> feature vector plus uncertainty and validity flags
```

This representation is deliberately explicit about where time enters. The inlet concentration may not equal the concentration at the sensing interface. If a step arrives gradually because of tubing and chamber mixing, fitting a single exponential to the output identifies the combined system, not the intrinsic reaction rate.

Preserve the raw values and instrument settings. A feature table should link back to the exact measurement segment and processing version. Never replace a saturated sample with an ordinary numerical value without also preserving the saturation flag. Missing samples, clipped peaks, and a genuine zero response represent different physical situations.

<a id="section-baselines-are-measurements-not-constants-of-nature"></a>

## Baselines are measurements, not constants of nature

A baseline can be a pre-exposure average, a fitted trend, a matched blank, or an independently measured reference channel. Each choice answers a different question. A pre-exposure baseline is local in time but may contain residual analyte. A reference channel may track common electronics while responding differently to humidity. A polynomial fitted across the entire trace can accidentally remove a slow genuine signal.

Common feature definitions are:

```text
absolute response:       r = x - b                 [same units as x]
relative response:       q = (x - b)/b             [dimensionless]
log ratio:               l = ln(x/b)               [dimensionless]
integrated response:     a = integral(r dt)        [response units * s]
```

Ratios require a meaningful, nonzero baseline. Log ratios require positive values and an appropriate physical interpretation. Signed electrochemical currents can cross zero, so a logarithm of raw current is not generally valid. Baseline correction must also preserve sign conventions: a reduction current becoming more negative may correspond to increasing analyte, not decreasing response.

### Worked example: uncertainty after normalization

Let measured current `x = 12.0 microampere` and baseline `b = 10.0 microampere`, with independent standard uncertainties `u_x = 0.2 microampere` and `u_b = 0.1 microampere`. The absolute response is 2.0 microampere with standard uncertainty `sqrt(0.2^2 + 0.1^2) = 0.224 microampere`.

For `q = x/b - 1`:

```text
dq/dx = 1/b = 0.1 per microampere
dq/db = -x/b^2 = -0.12 per microampere
u_q^2 = (u_x/b)^2 + (x*u_b/b^2)^2
u_q = 0.0233
q = 0.200
```

The relative response has about 11.7% relative standard uncertainty. Treating the baseline as exact would underestimate uncertainty. If `x` and `b` share errors, add the covariance term `2*(dq/dx)*(dq/db)*Cov(x,b)`; its sign and magnitude matter.

<a id="section-first-order-dynamics-useful-model-limited-interpretation"></a>

## First-order dynamics: useful model, limited interpretation

A simple first-order system satisfies:

```text
tau * dy/dt + y = K*c(t)

For a step from zero to c0 at t = 0:
y(t) = K*c0*[1 - exp(-t/tau)]
t_90 = tau*ln(10) approximately 2.303*tau
```

Here `tau` is in seconds, `K` converts concentration to response, and the equation assumes constant parameters. It does not capture several coupled transport stages, different rise and recovery kinetics, saturation, or drift. A good exponential fit is evidence that a simple approximation describes a trace; it is not a unique mechanistic explanation.

For `tau = 2 s`, 90% response requires 4.605 s. If the decision algorithm also averages one second of data, the complete decision delay exceeds the physical arrival delay and may depend on threshold. Reporting only the ADC interval as the response time would be misleading.

A rise-time estimate should state the initial and final levels, interpolation rule, and uncertainty. A noisy signal may cross a threshold many times. Requiring persistence reduces spurious crossings but adds another delay that belongs in the specification.

<a id="section-sampling-and-aliasing"></a>

## Sampling and aliasing

The sampling frequency must support the fastest information-bearing signal and the analog bandwidth. Sampling at 100 Hz does not make a sensor with a 10-second response resolve 100 chemical events per second. Conversely, slow nominal chemistry does not guarantee that high-frequency electrical interference is absent. An analog anti-alias filter limits frequencies that would otherwise fold into the sampled band.

Consider 60 Hz interference sampled at 50 Hz. It can appear as a 10 Hz component because frequencies separated by integer multiples of the sampling rate become indistinguishable after sampling. A digital filter applied afterward cannot determine which pre-sampling frequency produced the samples. Good instrument design controls aliasing before conversion.

Record actual timestamps, not just an assumed sample interval. Wireless transport can deliver packets in bursts. Arrival time at a computer is not necessarily acquisition time. Feature extraction should detect missing intervals and avoid treating interpolation as newly observed evidence.

<a id="section-filtering-trades-variance-for-temporal-detail"></a>

## Filtering trades variance for temporal detail

A moving average over `M` equally spaced samples reduces independent white noise but blurs rapid events. For a symmetric finite impulse response average, the group delay is `(M-1)/(2*f_s)` seconds. At `f_s = 10 Hz` and `M = 11`, this is 0.5 s. The noise reduction is smaller when adjacent samples are correlated.

An exponential moving average is convenient for streaming:

```text
z[k] = alpha*x[k] + (1-alpha)*z[k-1]
alpha = 1 - exp(-Delta_t/tau_f)
```

With `Delta_t = 0.1 s` and desired filter time constant `tau_f = 2 s`, `alpha = 0.04877`. This smooths noise while retaining a state that depends on previous samples. Initialization matters; starting at zero can create an artificial transient if the first measurement has a nonzero baseline.

A Savitzky-Golay filter estimates local polynomial behavior and can estimate derivatives. Window length, polynomial order, edge handling, and sample spacing change the result. Consult the official implementation documentation before treating a computed derivative as a physical rate. [SciPy, Savitzky-Golay filter](https://docs.scipy.org/doc/scipy/reference/generated/scipy.signal.savgol_filter.html)

Forward-backward filtering uses data from both temporal directions. It is useful for some offline analyses, but future samples contribute to earlier output values. A zero-phase trace cannot establish the latency of a causal online detector. [SciPy, forward-backward filtering](https://docs.scipy.org/doc/scipy/reference/generated/scipy.signal.filtfilt.html)

<a id="section-features-should-express-a-testable-hypothesis"></a>

## Features should express a testable hypothesis

| Feature family | Examples | Physical question | Important limitation |
| --- | --- | --- | --- |
| Amplitude | Blank-corrected plateau, peak, ratio | How much does the response change? | Sensitive to concentration and gain drift |
| Kinetic | Rise time, recovery time, initial slope | How quickly does the system respond? | Conflates sample delivery with interface kinetics |
| Integral | Charge or response area | What accumulated response occurred? | Depends on exposure duration and baseline drift |
| Spectral | Impedance magnitude and phase | Which time scales appear electrically? | Parameters may be non-identifiable |
| Cross-channel | Ratios, differences, covariance | Which changes are shared or distinct? | Ratios amplify uncertainty near zero |
| Quality | Saturation, missing fraction, blank slope | Is this measurement interpretable? | Quality flags are not chemical identity |

Choose features before looking at the final test labels. If a feature is selected because it separates the entire dataset, that selection has already learned from the test examples. Use a training pipeline that refits selection and scaling independently inside each split. [scikit-learn, data leakage guidance](https://scikit-learn.org/stable/common_pitfalls.html)

A public chemical-sensor dataset can contain extracted features rather than raw time series. The published UCI concentration extension describes a 128-feature representation formed from 16 channels. A benchmark using those features evaluates decisions after the original extraction process; it cannot independently validate a new raw-signal filter. [UCI, concentration-annotated drift dataset](https://archive.ics.uci.edu/dataset/270/gas+sensor+array+drift+dataset+at+different+concentrations)

<a id="section-impedance-features-and-model-fitting"></a>

## Impedance features and model fitting

For a resistor in series with a parallel resistor-capacitor element:

```text
Z(omega) = R_s + R_ct/[1 + j*omega*R_ct*C]
omega = 2*pi*f
```

The labels describe a circuit model, not automatic proof of a particular surface mechanism. Multiple processes can overlap over a limited frequency range. Report the fit residuals, frequency range, parameter covariance, and whether the system was sufficiently stable during acquisition.

### Worked example: a characteristic frequency

Use synthetic `R_s = 100 ohm`, `R_ct = 900 ohm`, and `C = 10 microfarad`. Then `R_ct*C = 0.009 s` and the imaginary magnitude peaks at `f = 1/(2*pi*0.009) = 17.68 Hz`. At that frequency, `Z = 550 - j450 ohm`. Its magnitude is approximately 710.6 ohm and phase approximately -39.3 degrees.

A classifier could use this complex value directly, fit the circuit, or use several frequency features. Circuit fitting can compress the data into interpretable parameters, but only when those parameters are supported by the frequency coverage and noise level. A single frequency cannot independently recover three unknown circuit parameters.

<a id="section-evaluation-of-the-entire-signal-pipeline"></a>

## Evaluation of the entire signal pipeline

Use three tests. First, pass synthetic signals with known amplitude, delay, and noise through the code to measure numerical distortion. Second, compare repeated real measurements and blanks to estimate reproducibility. Third, evaluate the frozen pipeline on independent exposures, devices, and days. These tests address different questions and should not be substituted for one another.

For temporal features, report errors in seconds as well as classification performance. For amplitude features, report the calibration domain and propagated uncertainty. For dropped or invalid samples, report the rejection rate. A model that succeeds only after discarding difficult records needs its exclusions stated in the result.

<a id="section-design-decision-carried-forward"></a>

## Design decision carried forward

**Choice:** freeze the causal preprocessing and feature definitions for the device's intended decision. **Criteria:** units, delay, uncertainty, missing-data behavior, and preservation of chemical information. **Evidence:** known-answer signals, error propagation, and independent exposure tests. **Artifact:** a signal-processing contract listing input timestamps, every transformation, feature units, validity flags, processing version, and end-to-end latency contribution. Add it to the [design studio](../design-studio.md).

<a id="section-problems-and-worked-answers"></a>

## Problems and worked answers

1. **Two response stages:** A chamber and an electrode each behave as a first-order system. Is their cascade generally one exponential? **Answer:** No. The product of two transfer functions produces two poles; a single exponential may only approximate part of the trace.
2. **Filter delay:** A 21-point moving average at 20 Hz has what group delay? **Answer:** `(21-1)/(2*20) = 0.5 s`.
3. **Ratio instability:** Why is `(x-b)/b` dangerous near `b = 0`? **Answer:** Both the value and its uncertainty can diverge; choose a physically justified alternative representation.
4. **EIS ambiguity:** Does a falling fitted resistance prove selective binding? **Answer:** No. Conductivity changes, electrode condition, temperature, and model mismatch can also change the estimate.
5. **Future information:** A detector uses centered smoothing and reports onset before the raw signal crosses threshold. What should be reported? **Answer:** An offline reconstructed onset, with uncertainty. Reevaluate causal deployment latency using only samples available at each decision time.

<!-- course-footer:start -->
---

[Previous: 13. Arrays, selectivity, and identifiable mixtures](13-arrays-and-selectivity.md) · [All modules](index.md) · [Next: 15. Machine learning, uncertainty, and domain shift](15-machine-learning-and-domain-shift.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
