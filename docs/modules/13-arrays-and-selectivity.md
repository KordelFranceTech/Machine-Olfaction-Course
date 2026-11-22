---
layout: default
title: '13. Arrays, selectivity, and identifiable mixtures'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [**Modules**](index.md) · [Labs](../labs/index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Modules](index.md) / 13. Arrays, selectivity, and identifiable mixtures

**Module 13 of 18**

<!-- course-navigation:end -->

# 13. Arrays, selectivity, and identifiable mixtures

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Learning outcomes](#section-learning-outcomes)
- [From one response to a response vector](#section-from-one-response-to-a-response-vector)
- [A local linear model and its limits](#section-a-local-linear-model-and-its-limits)
- [Conditioning: the distance between possible explanations](#section-conditioning-the-distance-between-possible-explanations)
- [Redundant channels and diverse channels serve different purposes](#section-redundant-channels-and-diverse-channels-serve-different-purposes)
- [Majority decisions require an error model](#section-majority-decisions-require-an-error-model)
- [Design the experiment before selecting the channels](#section-design-the-experiment-before-selecting-the-channels)
- [What published arrays do and do not establish](#section-what-published-arrays-do-and-do-not-establish)
- [Design decision carried forward](#section-design-decision-carried-forward)
- [Problems and worked answers](#section-problems-and-worked-answers)

</details>
<!-- course-toc:end -->

A single sensor compresses a chemical environment into a small number of electrical measurements. An array offers several views of that environment. Its value depends on whether those views contain different information, whether their errors are understood, and whether the sample reaches them in a comparable way. Adding channels is easy to count; adding useful information is harder.

**Prerequisites:** calibration and uncertainty, elementary probability, vectors, matrices, and the distinction between concentration and electrical response. **Suggested effort:** 3 hours of study and 2 hours of problems.

<a id="section-learning-outcomes"></a>

## Learning outcomes

After this module, you should be able to:

- Distinguish chemical selectivity, statistical discriminability, and redundancy.
- Build a local linear response model and determine when mixture concentrations are identifiable.
- Explain why correlated errors limit averaging and majority voting.
- Design a challenge matrix that tests interference, mixtures, environmental variation, and failed channels.
- Select array channels using independent validation and realistic measurement cost.

<a id="section-from-one-response-to-a-response-vector"></a>

## From one response to a response vector

Imagine two hypothetical gases, A and B. A channel that responds to both is cross-sensitive. That channel can still be useful if another channel responds to A and B in a different proportion. The pair may support a distinction that neither channel supports alone. Biological olfaction provides a motivation for distributed representations: Malnic and colleagues demonstrated that odorants and mammalian receptors participate in overlapping response combinations. This is evidence about a biological coding scheme, not proof that any engineered array reproduces perception. [Malnic et al., 1999](https://pubmed.ncbi.nlm.nih.gov/10089886/)

For an array, write the measurement as a vector. Each element could be a current, a conductance, or an impedance feature. Keep the feature definitions and units explicit. If one coordinate is measured in amperes and another in ohms, Euclidean distance between raw vectors has no physically meaningful interpretation until the scaling is defined.

```text
y = f(c, e, h, d) + epsilon

y: vector of measured responses
c: vector of analyte concentrations
e: environment, such as temperature and humidity
h: exposure and regeneration history
d: device properties, including manufacturing variation and age
epsilon: random measurement error
```

The function can be nonlinear and history-dependent. A learning algorithm does not remove these dependencies; it approximates some of them over its training domain. A response pattern can change because the analyte changes, because the device changes, or because the same analyte arrives under different conditions.

<a id="section-a-local-linear-model-and-its-limits"></a>

## A local linear model and its limits

Near a reference operating point, a first-order expansion gives a useful approximation:

```text
y - b = S c + epsilon

b: blank response at the stated operating conditions
S[i,j] = change in response i per unit concentration of analyte j
```

For this simplified form, concentrations are referenced so that `c = 0` represents the blank. More generally the expansion uses `c - c0`. The model assumes approximately additive responses in a defined neighborhood. Competitive adsorption, electrochemical reaction competition, saturation, pH changes, and sample depletion can violate that assumption.

With `m` channels and `p` unknown concentrations, `m >= p` is necessary for unconstrained linear identification but is not sufficient. The columns of `S` must be linearly independent. Two channels with exactly proportional selectivities measure the same mixture direction, even if their outputs have different amplitudes. Unknown humidity adds another degree of freedom unless it is measured, controlled, or otherwise constrained.

### Worked example: recovering a two-component mixture

All numbers below are synthetic teaching values. Suppose response is in arbitrary units and concentration is in ppm by amount fraction:

```text
S = [[2.0, 0.5],
     [0.5, 2.0]] response units/ppm

y - b = [6.5, 3.5] response units

det(S) = 2*2 - 0.5*0.5 = 3.75

c_A = (2*6.5 - 0.5*3.5)/3.75 = 3 ppm
c_B = (-0.5*6.5 + 2*3.5)/3.75 = 1 ppm
```

The result is an estimate conditional on the response model. A negative estimate in another sample would not imply a negative physical concentration. It could indicate noise, an incorrect baseline, model mismatch, or an unmodeled interferent. Nonnegative least squares imposes a physical constraint but does not prove that the assumed analytes are the correct ones.

Now replace the second row with `[4, 1]`. It becomes exactly twice the first row. The determinant is zero; infinitely many mixtures yield the same measurements. Collecting more repeated samples can reduce noise but cannot recover the missing chemical dimension.

<a id="section-conditioning-the-distance-between-possible-explanations"></a>

## Conditioning: the distance between possible explanations

A nearly singular matrix is also troublesome. Consider channels `[1, 1]` and `[1, 1.01]`. Their difference isolates B, but that difference is only `0.01*c_B`. A response error of 0.01 unit can change the inferred B concentration by approximately 1 ppm. The subtraction extracts chemical information and amplifies measurement uncertainty at the same time.

Singular-value decomposition formalizes this geometry. A small singular value corresponds to a mixture direction that changes the outputs very little. For equal response scaling and white measurement noise, the ratio of largest to smallest singular value is the 2-norm condition number. It describes sensitivity of the inverse problem, not an intrinsic chemical property independent of units. Scale concentrations and responses meaningfully before comparing designs.

When errors have covariance `Sigma`, a weighted fit minimizes:

```text
r = y - b - S c
objective = transpose(r) inverse(Sigma) r

Cov(c_hat) approximately equals inverse(transpose(S) inverse(Sigma) S)
```

This covariance expression assumes the model and `S` are known, errors are approximately Gaussian with the specified covariance, and the inverse exists. Calibration uncertainty and model discrepancy add further uncertainty. The matrix inside the inverse is a local information measure: good array design makes difficult concentration directions distinguishable relative to noise.

<a id="section-redundant-channels-and-diverse-channels-serve-different-purposes"></a>

## Redundant channels and diverse channels serve different purposes

Repeated channels with similar response chemistry can expose manufacturing outliers, provide fault tolerance, and improve precision. Diverse channels can help separate analytes and environmental effects. A practical array may need both. A humidity reference may contribute more useful information than another high-amplitude gas channel if humidity dominates the error budget.

An integrated chip can contain a large number of addressable elements. For example, Wang and colleagues reported a 2024 nanotube array architecture with up to 10,000 individually addressable sensors. Addressable element count, number of distinct response types, and number of independently recoverable chemical variables remain different quantities. [Wang et al., 2024](https://doi.org/10.1038/s41928-023-01107-7)

### Worked example: correlated noise defeats naive averaging

For `n` equal-variance measurements with pairwise correlation `rho`:

```text
Var(mean) = sigma^2 * [1 + (n - 1)*rho] / n
```

Four channels with `sigma = 1` response unit and independent noise have a mean standard deviation of 0.5 unit. If `rho = 0.6`, the standard deviation becomes `sqrt(0.7) = 0.837` unit. Their average is only modestly better than one channel. This result follows directly by summing the four variances and twelve cross-covariance terms, then dividing by sixteen.

Shared airflow fluctuations, electrolyte changes, reference-electrode movement, and common electronics can create correlated errors. Estimating correlation from repeated measurements of one stable sample captures only the errors present in that experiment. It may miss correlations that appear across days or during environmental excursions.

<a id="section-majority-decisions-require-an-error-model"></a>

## Majority decisions require an error model

For three independent binary detectors with equal error probability `p`, a majority decision is wrong when exactly two or all three are wrong:

```text
P(majority error) = 3*p^2*(1-p) + p^3
```

At `p = 0.10`, the result is 0.028. This attractive improvement depends on independence and on using comparable decision problems. Suppose a shared interference event occurs with probability 0.05 and makes all channels wrong. Outside that event, each channel has independent error probability 0.10. Majority error becomes `0.05 + 0.95*0.028 = 0.0766`. Repetition cannot vote away the common cause.

Voting also discards confidence and concentration information. A weak, noisy channel counts as much as a stable one in an unweighted vote. A continuous multivariate model may preserve more information, but it needs its own validated uncertainty and rejection behavior. Avoid multiplying channel probabilities unless their conditional dependence has been justified.

<a id="section-design-the-experiment-before-selecting-the-channels"></a>

## Design the experiment before selecting the channels

A useful challenge matrix crosses analyte identity and concentration with independent nuisance conditions. For a teaching design, include blanks, pure A, pure B, mixtures, and an unknown compound U. Distribute them across multiple days and devices. Cross at least two humidity conditions with every class so that humidity cannot become a shortcut for chemical identity.

Measure the full response and recovery, not only a handpicked peak. Record the sample path, device identity, conditioning history, and timing. Randomize presentation order where feasible and use appropriate carryover checks. A sequence in which every A exposure precedes every B exposure lets drift imitate chemical discrimination.

Channel selection must occur within the training portion of each validation split. Selecting the best channels using the entire dataset, then reporting test performance, leaks information from the test labels. Official machine-learning documentation explains why preprocessing and feature selection belong inside a fitted pipeline. [scikit-learn, common pitfalls](https://scikit-learn.org/stable/common_pitfalls.html)

Evaluate more than accuracy: calibration effort, power, response time, recovery, replaceability, and robustness to a missing channel all matter. A four-channel model that works across devices can be more useful than a larger model that requires device-specific retraining.

<a id="section-what-published-arrays-do-and-do-not-establish"></a>

## What published arrays do and do not establish

The UCI drift benchmark is valuable for studying changing response patterns, but its metal-oxide measurements do not establish electrochemical sensing performance. A public dataset can test a computational idea while leaving the target hardware unvalidated. [Fonollosa, Rodríguez-Luján, and Huerta, 2015](https://pubmed.ncbi.nlm.nih.gov/26217723/)

Light-activated conductive framework arrays are another route to generating differentiated responses. A 2025 study integrated such films with micro-LEDs. The general engineering lesson is that controlled excitation can add response dimensions, while also introducing energy, timing, and stability costs. Transfer to another material system requires new measurements. [Lee et al., 2025](https://doi.org/10.1038/s41467-025-64602-9)

<a id="section-design-decision-carried-forward"></a>

## Design decision carried forward

**Choice:** allocate channels among redundancy, diversity, and environmental controls. **Criteria:** response-matrix conditioning, correlated error, calibration effort, and tolerance of failed channels. **Evidence:** synthetic mixture inversion, covariance analysis, and a proposed independent interference challenge. **Artifact:** an array-selection table with each channel's role, expected information, shared failure causes, and replacement/calibration implications. Add it to the [design studio](../design-studio.md).

<a id="section-problems-and-worked-answers"></a>

## Problems and worked answers

1. **Three channels, three gases:** Does a square sensitivity matrix guarantee identification? **Answer:** No. Its columns must be independent, conditioning must be acceptable relative to noise, and environmental or unknown-mixture effects must not invalidate the model.
2. **Redundant gain:** Two channels have responses `[1, 2]` and `[3, 6]` to two gases. What does the second add? **Answer:** Potentially precision and fault monitoring, but no new linear chemical dimension. The rows are proportional.
3. **Common humidity effect:** Every channel rises during a humidity change. Does agreement establish the target gas? **Answer:** No. Agreement is compatible with a common nuisance effect. A humidity challenge and independent reference are needed.
4. **Unknown U:** A classifier always assigns A or B. What must change before open-environment use? **Answer:** Add validation with unknowns and mixtures, a defined abstention rule, and a way to distinguish invalid measurement from a supported classification.
5. **Array proposal:** Allocate six channels to precision, diversity, and controls. **Answer guide:** Several allocations can be defensible. Credit depends on an explicit error model, controls for shared drift, expected matrix conditioning, and a validation experiment that can reject the design.

<!-- course-footer:start -->
---

[Previous: 12 · Breath sensing and clinical evidence](12-breath-sensing-and-clinical-evidence.md) · [All modules](index.md) · [Next: 14. Signal processing, time response, and features](14-signal-processing-and-features.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
