---
layout: default
title: '11 · Calibration and uncertainty'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [**Modules**](index.md) · [Labs](../labs/index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Modules](index.md) / 11 · Calibration and uncertainty

**Module 11 of 18**

<!-- course-navigation:end -->

# 11 · Calibration and uncertainty

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Learning outcomes](#section-learning-outcomes)
- [1. Define the result before fitting the curve](#section-1-define-the-result-before-fitting-the-curve)
- [2. Build a calibration experiment, not just a line](#section-2-build-a-calibration-experiment-not-just-a-line)
- [3. Inverse prediction and uncertainty](#section-3-inverse-prediction-and-uncertainty)
- [4. Worked example: a numerical uncertainty budget](#section-4-worked-example-a-numerical-uncertainty-budget)
- [5. Detection and quantification are different decisions](#section-5-detection-and-quantification-are-different-decisions)
- [6. Worked example: detection probability and repeated decisions](#section-6-worked-example-detection-probability-and-repeated-decisions)
- [7. Precision, bias, selectivity, and drift](#section-7-precision-bias-selectivity-and-drift)
- [8. Transfer to another device or environment](#section-8-transfer-to-another-device-or-environment)
- [9. Design decision carried forward](#section-9-design-decision-carried-forward)
- [10. Exercises and worked answers](#section-10-exercises-and-worked-answers)

</details>
<!-- course-toc:end -->

A current is an observation. A concentration is an inference obtained by relating that observation to reference information and a model. Calibration builds that relation; validation asks whether it is suitable for its intended use. Uncertainty expresses the remaining doubt about the reported value under the stated assumptions.

**Level and time:** upper-division undergraduate to beginning graduate; 6–8 hours. **Prerequisites:** regression, derivatives, elementary probability, [electrochemical methods](06-electrochemical-methods.md), and [electronics](10-electronics-and-embedded-systems.md).

<a id="section-learning-outcomes"></a>

## Learning outcomes

- Design a calibration that separates concentration response from nuisance variables.
- Invert a linear calibration and propagate important uncertainties.
- Distinguish detection, quantification, selectivity, repeatability, and accuracy.
- Explain why a small blank standard deviation does not establish field performance.
- Specify validation and recalibration decisions before examining final test results.

<a id="section-1-define-the-result-before-fitting-the-curve"></a>

## 1. Define the result before fitting the curve

A calibration model is meaningful only after specifying the measurand, units, sampling path, operating conditions, and reporting interval. “Concentration” may mean wet mole fraction, dry mole fraction, mass concentration, or concentration in a sensing film. These are not interchangeable.

A simple response model is:

```text
y = b + s c + error

y: electrical response, such as nA
b: blank offset, nA
s: sensitivity, nA/ppb
c: target mole fraction expressed in ppb
```

The slope `s` is analytical sensitivity in this model. It is not diagnostic sensitivity, which is a proportion of disease-positive people correctly classified. Also, a steep slope can coexist with poor selectivity or high noise. State the meaning of a term before comparing papers that use it differently.

The [NIST/SEMATECH calibration-model guidance](https://www.itl.nist.gov/div898/handbook/mpc/section3/mpc365.htm) emphasizes model assessment from calibration data. A high coefficient of determination does not by itself show that residuals are small enough, unbiased, or appropriate for the intended range.

<a id="section-2-build-a-calibration-experiment-not-just-a-line"></a>

## 2. Build a calibration experiment, not just a line

Use independent reference preparations, multiple concentrations across the intended range, blanks, and replicates that expose different sources of variation. Several repeated ADC readings from one exposure are not several independent calibration preparations. Randomize measurement order when possible and include checks for carryover.

Separate exploratory data used to choose a model from confirmatory data used to evaluate it. If humidity, temperature, or flow influences the response, vary it deliberately rather than hoping it stays constant. Include mixtures with relevant interferents. A pure-target calibration establishes a response under that mixture condition; it does not prove that the same signal identifies the target in arbitrary air.

Inspect residuals against fitted value, concentration, time, environmental variables, and measurement order. Increasing variance with concentration may call for weighted fitting. Curvature may require a different model or a narrower valid range. Do not extrapolate far outside the range merely because software returns a number.

The [Eurachem 2025 method-validation guide](https://www.eurachem.org/images/stories/Guides/pdf/MV_guide_3rd_ed_V1_EN.pdf) is a current professional guide to fitness for purpose, validation, and verification. Its framework helps connect performance characteristics with intended use; this course's examples are teaching calculations, not an accredited validation protocol.

<a id="section-3-inverse-prediction-and-uncertainty"></a>

## 3. Inverse prediction and uncertainty

For a valid linear model, an unknown response `y` gives:

```text
c_hat = (y - b)/s
```

This inversion becomes unstable when the slope is near zero. It also inherits uncertainty from `y`, `b`, and `s`, plus effects omitted from the model. Under a local linear propagation approximation:

```text
partial c / partial y = 1/s
partial c / partial b = -1/s
partial c / partial s = -(y - b)/s^2 = -c_hat/s

u(c)^2 = sum_i [g_i^2 u(x_i)^2]
         + 2 sum_(i<j) [g_i g_j cov(x_i,x_j)]
```

Here `g_i` are the derivatives above. Slope and intercept from the same regression are generally correlated. Ignoring their covariance is not automatically conservative. Reference concentration uncertainty, recovery, and environmental corrections may introduce additional inputs and dependencies.

The [JCGM publications page](https://www.bipm.org/en/committees/jc/jcgm/publications) lists the GUM suite, including JCGM 100:2008 and its 2026 amendment. The familiar first-order propagation method remains a useful teaching starting point; consult the current suite and relevant supplements for a real application, particularly when models are nonlinear or distributions are asymmetric.

<a id="section-4-worked-example-a-numerical-uncertainty-budget"></a>

## 4. Worked example: a numerical uncertainty budget

Suppose a hypothetical calibration has `b = 2.0 nA`, `s = 0.25 nA/ppb`, and an unknown produces `y = 27.0 nA`. Then:

```text
c_hat = (27 - 2)/0.25 = 100 ppb
```

For illustration only, treat these three inputs as independent with standard uncertainties `u(y) = 0.50 nA`, `u(b) = 0.30 nA`, and `u(s) = 0.010 nA/ppb`.

| Input | Sensitivity coefficient | Contribution to concentration standard uncertainty |
| --- | --- | --- |
| Response `y` | `1/s = 4 ppb/nA` | `2.0 ppb` |
| Offset `b` | `-1/s = -4 ppb/nA` | `1.2 ppb` |
| Slope `s` | `-c/s = -400 ppb²/nA` | `4.0 ppb` |

```text
u(c) = sqrt(2.0^2 + 1.2^2 + 4.0^2) = 4.63 ppb
U = k u(c), with k = 2, gives U = 9.26 ppb
```

The `k = 2` expanded uncertainty is not automatically an exact 95% interval. Coverage depends on distributions, effective degrees of freedom, and model adequacy. The budget also omits sampling losses and interference. Reporting `100 ± 9.3 ppb` without stating those limitations would overstate what was evaluated.

The slope contribution dominates this example. Collecting thousands more readings of the unknown would not eliminate it. Better reference information or a better calibration design could matter more than faster sampling.

<a id="section-5-detection-and-quantification-are-different-decisions"></a>

## 5. Detection and quantification are different decisions

A blank distribution describes the measurement when the target is absent under specified conditions. A decision threshold determines when an observation is sufficiently unusual relative to that blank. A detection limit additionally needs an agreed probability of detecting a small true amount. A quantification limit concerns whether the amount can be estimated with acceptable performance.

[IUPAC's limit-of-detection entry](https://goldbook.iupac.org/terms/view/L03540) provides the terminology. Shortcuts such as `3 sigma_blank / slope` or `10 sigma_blank / slope` are useful screening calculations under explicit assumptions, not universal certifications of detection or quantification.

For an increasing signal with blank mean `b`, known constant standard deviation `sigma`, and normally distributed independent errors, a decision threshold `b + 3 sigma` has a one-sided blank exceedance probability of about 0.00135. If the true mean signal is exactly `b + 3 sigma`, half its observations exceed that threshold. Thus “three sigma above blank” does not simultaneously mean a 99.9% detection probability.

<a id="section-6-worked-example-detection-probability-and-repeated-decisions"></a>

## 6. Worked example: detection probability and repeated decisions

Using the equal-variance normal model, require a blank false-positive probability corresponding to `z_alpha = 3`, and a 95% detection probability for a target concentration. The target mean must be another `1.645 sigma` above the threshold:

```text
s c_detection = (3 + 1.645) sigma = 4.645 sigma
```

For `sigma = 0.20 nA` and `s = 0.10 nA/ppb`, the illustrative value is `9.29 ppb`. A `3 sigma/s` shortcut gives `6 ppb`, which is the concentration whose mean sits at the threshold, not the concentration giving 95% detection under this model.

Repeated decisions also matter. If independent blank decisions each have false-positive probability `p = 0.00135`, the probability of at least one false positive in `N = 1000` decisions is:

```text
1 - (1 - p)^N ≈ 0.741
```

Real continuous signals are often correlated, so this independent calculation is not a field prediction. It does show why per-window error rates and per-hour alarm rates answer different questions. Validate the actual temporal decision logic, including persistence rules and hysteresis.

<a id="section-7-precision-bias-selectivity-and-drift"></a>

## 7. Precision, bias, selectivity, and drift

Repeatability describes variation under closely matched conditions. Intermediate precision introduces changes such as day, operator, or instrument. Reproducibility extends to broader conditions, often including laboratories. Bias concerns systematic displacement relative to a reference. None can be inferred from a single smooth trace.

Selectivity is the ability to make the intended measurement in the presence of other components. In a simple local model:

```text
y = b + s_target c_target + sum_j s_j c_j
```

Even a small cross-sensitivity `s_j` can dominate when an interferent is much more abundant than the target. Report interference concentrations and mixtures, not only a ratio of isolated slopes.

Drift can affect offset, sensitivity, response time, or selectivity. A blank check mainly tests offset; it does not establish an unchanged slope. A single check standard mainly tests behavior near that concentration. Choose control observations to match the types of change that would invalidate the result.

The [NIST discussion of check standards and propagation](https://www.itl.nist.gov/div898/handbook/mpc/section3/mpc3673.htm) is a useful bridge between an analytical uncertainty budget and observed long-term performance. A model-based budget and empirical quality-control evidence should inform each other.

<a id="section-8-transfer-to-another-device-or-environment"></a>

## 8. Transfer to another device or environment

A calibration fitted on one sensor may fail on another because its area, baseline, transport, or chemistry differs. A mathematical transfer function should be trained and evaluated on independent transfer data. If every target-class sample comes from one module and every control from another, classification may identify the module.

Hold out entire devices, days, batches, or sites according to the deployment question. A random split of adjacent time points can make the test set nearly duplicate the training set. The most useful validation set is often the one that deliberately challenges a plausible source of failure.

Predefine recalibration triggers. Examples include control-sample deviations, module replacement, operation outside the validated range, or detected changes in response dynamics. The trigger should state what evidence restores validity. “Recalibrate whenever results look wrong” invites selective correction after seeing the desired answer.

<a id="section-9-design-decision-carried-forward"></a>

## 9. Design decision carried forward

For the [design studio](../design-studio.md), specify the student project's intended measurand, calibration model, environmental range, uncertainty budget, and invalid-result rules. Your deliverable is a calibration matrix covering concentration, humidity, interferents, and independent modules; a held-out validation plan; and an alarm-threshold rationale. Compare a simpler model over a narrow valid range with a more flexible model requiring more data. Evidence required before progression includes independent reference agreement, residual analysis, recovery characterization, and performance on held-out conditions. Analytical validation supports a chemical measurement; a health interpretation needs additional evidence.

<a id="section-10-exercises-and-worked-answers"></a>

## 10. Exercises and worked answers

1. **Inverse calibration.** `y = 5 + 0.4c`, with `y = 25`. **Answer:** `c = 50` in the concentration units used to fit the model.
2. **Bias from recovery.** The complete sample path delivers 80% of the original target, while calibration bypasses that path. **Answer:** absent other effects, the reported concentration is 20% low. Calibrate the relevant complete system or correct recovery with justified uncertainty.
3. **Interference.** A target at 10 ppb has sensitivity 1 unit/ppb; an interferent at 1000 ppb has sensitivity 0.02 unit/ppb. **Answer:** target contribution is 10 units and interferent contribution is 20 units. Small relative cross-sensitivity does not guarantee a small error.
4. **Threshold meaning.** Why can a very low blank false-positive rate coexist with missed low-concentration samples? **Answer:** the target and blank distributions overlap. Moving the threshold trades false positives against false negatives.
5. **Transfer design.** You have six modules measured on three days. **Answer criterion:** define splits at the module/day level aligned with the intended use; keep preprocessing and model selection inside the training data; report uncertainty across independent units.

<!-- course-footer:start -->
---

[Previous: 10 · Electronics and embedded systems](10-electronics-and-embedded-systems.md) · [All modules](index.md) · [Next: 12 · Breath sensing and clinical evidence](12-breath-sensing-and-clinical-evidence.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
