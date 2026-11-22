---
layout: default
title: 'Lab 07. Transport timing and sensor response mismatch'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [Modules](../modules/index.md) · [**Labs**](index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Labs](index.md) / Lab 07. Transport timing and sensor response mismatch

**Lab 07 of 8**

<!-- course-navigation:end -->

# Lab 07. Transport timing and sensor response mismatch

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Question](#section-question)
- [Model and assumptions](#section-model-and-assumptions)
- [Run the known-answer calculation](#section-run-the-known-answer-calculation)
- [Explain the apparent reversed direction](#section-explain-the-apparent-reversed-direction)
- [Extend the model one assumption at a time](#section-extend-the-model-one-assumption-at-a-time)
- [Relate the exercise to active olfaction](#section-relate-the-exercise-to-active-olfaction)
- [Deliverable and assessment](#section-deliverable-and-assessment)

</details>
<!-- course-toc:end -->

**Time:** 2–3 hours. **Prerequisites:** [Module 14](../modules/14-signal-processing-and-features.md) and [Module 16](../modules/16-olfaction-and-active-sampling.md). **Equipment:** Python 3, standard library only. **Data:** synthetic step signals with known response dynamics.

<a id="section-question"></a>

## Question

If one sensor responds after another, how much of the difference comes from molecular transport and how much comes from the instruments? This exercise demonstrates that even a simple threshold-timing method can infer the wrong speed or direction when channel dynamics differ.

This is a controlled timing model, not a realistic turbulent-plume simulation. A step is chosen so that the true answer can be derived exactly. The model isolates one source of error before adding the many complications of outdoor transport.

<a id="section-model-and-assumptions"></a>

## Model and assumptions

Two fixed sensors lie 0.10 m apart along uniform flow at 0.20 m/s. A concentration step reaches the first at time zero and the second after 0.50 s. Each sensor has unity steady-state gain and a first-order response. There is no noise, saturation, baseline drift, clock error, or plume deformation.

For arrival time `t_a`, sensor time constant `tau`, and threshold fraction `q`:

```text
y(t) = 0                                  for t < t_a
y(t) = 1 - exp[-(t-t_a)/tau]              for t >= t_a
threshold time = t_a - tau*ln(1-q)
```

The threshold is a fraction of the same final response for both channels. If their steady-state gains differed and a common absolute threshold were used, another bias would appear.

<a id="section-run-the-known-answer-calculation"></a>

## Run the known-answer calculation

```python
from math import exp, log, ceil, sqrt

separation_m = 0.10
true_speed_m_s = 0.20
transport_lag_s = separation_m / true_speed_m_s
sample_period_s = 0.001
threshold = 0.5


def crossing(arrival, tau, q, dt):
    # Uniform samples include t = 0; result is the first sampled crossing.
    final_time = arrival - tau * log(1 - q) + 2 * dt
    for k in range(ceil(final_time / dt) + 1):
        t = k * dt
        response = 0.0 if t < arrival else 1 - exp(-(t - arrival) / tau)
        if response >= q:
            return t
    raise RuntimeError("No crossing within computed interval")


def evaluate(tau_1, tau_2):
    t1 = crossing(0.0, tau_1, threshold, sample_period_s)
    t2 = crossing(transport_lag_s, tau_2, threshold, sample_period_s)
    observed_lag = t2 - t1
    exact_lag = transport_lag_s + (tau_2 - tau_1) * (-log(1 - threshold))
    assert abs(observed_lag - exact_lag) <= sample_period_s + 1e-12
    return observed_lag, separation_m / observed_lag


for name, tau1, tau2 in [
    ("matched", 2.0, 2.0),
    ("second slower", 2.0, 5.0),
    ("first slower", 5.0, 2.0),
]:
    lag, speed = evaluate(tau1, tau2)
    print(f"{name:14s}: lag={lag: .3f} s, naive speed={speed: .4f} m/s")

# Idealized independent standard-uncertainty propagation.
u_distance = 0.005
u_lag = 0.10
relative_u = sqrt((u_distance / separation_m) ** 2
                  + (u_lag / transport_lag_s) ** 2)
print(f"Ideal relative standard uncertainty = {100 * relative_u:.2f}%")
```

Expected output:

```text
matched       : lag= 0.500 s, naive speed= 0.2000 m/s
second slower : lag= 2.579 s, naive speed= 0.0388 m/s
first slower  : lag=-1.579 s, naive speed=-0.0633 m/s
Ideal relative standard uncertainty = 20.62%
```

Minor changes in the last printed digit can occur if sampling or floating-point threshold handling is changed. The assertion checks the sampled lag against the analytic value to within one sample interval.

<a id="section-explain-the-apparent-reversed-direction"></a>

## Explain the apparent reversed direction

The upstream sensor in the third case is slow. The downstream sensor sees the concentration step later but crosses half of its final response earlier. The naive negative speed is therefore an instrument-response artifact. It does not mean that the gas traveled upstream.

The matched case works because both response delays cancel under the deliberately ideal assumptions. That cancellation can fail if the signals have different shapes, the channels saturate differently, or baseline and gain changes alter threshold interpretation. Matching nominal sensor models is not the same as matching every physical response kernel.

The final uncertainty calculation includes distance and lag uncertainty but excludes systematic model mismatch. It would be inappropriate to report 20.62% as the complete uncertainty for the mismatched cases. A precise estimate conditional on a false model can be precisely wrong.

<a id="section-extend-the-model-one-assumption-at-a-time"></a>

## Extend the model one assumption at a time

1. Change the threshold to 0.1 and 0.9. Derive how mismatch bias scales with `-ln(1-q)`. **Answer guide:** higher threshold fractions produce larger response-delay differences for first-order sensors.
2. Add a constant clock offset of 0.05 s to the second channel. Quantify the speed error even when the time constants match.
3. Add Gaussian measurement noise using a fixed seed. Compare first crossing with a persistence rule, and report both false crossings and added delay.
4. Replace the step with a finite pulse. Does each sensor reach the same fraction of the input's nominal steady response before the pulse ends?
5. Add a moving sensor position. Explain why each recorded value represents exposure history rather than only the current position.

A useful advanced extension is to estimate lag with cross-correlation and compare it with threshold timing. Include a shared nuisance signal to test whether correlation follows chemistry or the nuisance. Do not assume that using a more elaborate estimator removes physical ambiguity.

<a id="section-relate-the-exercise-to-active-olfaction"></a>

## Relate the exercise to active olfaction

In intermittent environments, actions can be selected to gain information about a source instead of following a noisy instantaneous gradient. The foundational infotaxis study formulates this idea probabilistically. It provides a research direction, not a guarantee that a two-sensor device can locate any source. [Vergassola, Villermaux, and Shraiman, 2007](https://www.nature.com/articles/nature05464)

For experimental data, distinguish electrical response time, sample-path delay, and actual flow transport. An independent flow reference and controlled delivery experiment are needed before assigning spatial meaning to measured lags. A motion sensor can support pose estimation but does not independently establish chemical transport velocity.

<a id="section-deliverable-and-assessment"></a>

## Deliverable and assessment

Submit a Markdown timing budget with separate rows for sample transport, each channel's response, filtering, timestamp uncertainty, and decision logic. Include the expected results, one extension, and a statement of the conditions under which a speed estimate would be valid.

Assessment: derivation and units (25%), reproducible simulation (25%), identification of systematic errors (30%), and a practical validation design (20%). Explicitly label all numerical results as simulated.

**Design artifact carried forward:** a synchronization and response-calibration specification, including when spatial inference must be disabled. Add it to the [design studio](../design-studio.md).

<!-- course-footer:start -->
---

[Previous: Lab 06. Drift, leakage, and honest validation](06-drift-and-validation.md) · [All labs](index.md) · [Next: Lab 08. Capstone design and evidence studio](08-capstone-studio.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
