---
layout: default
title: 'Lab 06. Drift, leakage, and honest validation'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [Modules](../modules/index.md) · [**Labs**](index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Labs](index.md) / Lab 06. Drift, leakage, and honest validation

**Lab 06 of 8**

<!-- course-navigation:end -->

# Lab 06. Drift, leakage, and honest validation

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Question](#section-question)
- [Part A: exposure leakage](#section-part-a-exposure-leakage)
- [Part B: additive drift and a reference blank](#section-part-b-additive-drift-and-a-reference-blank)
- [Interpret the results](#section-interpret-the-results)
- [Required extensions](#section-required-extensions)
- [Deliverable and assessment](#section-deliverable-and-assessment)

</details>
<!-- course-toc:end -->

**Time:** 2–3 hours. **Prerequisites:** [Module 15](../modules/15-machine-learning-and-domain-shift.md). **Equipment:** Python 3, standard library only. **Data:** entirely synthetic. No downloaded dataset, gas generation, or human samples are required.

<a id="section-question"></a>

## Question

Can an apparently excellent classifier learn an exposure-specific nuisance instead of chemistry? Can an independently measured blank correct one type of drift while leaving other types unresolved?

The lab constructs two deliberately simple worlds. Their simplicity makes the failure mechanisms visible. The numerical outcomes are properties of these constructed worlds, not performance estimates for a physical sensor.

<a id="section-part-a-exposure-leakage"></a>

## Part A: exposure leakage

Each synthetic exposure has eight windows. The input feature is dominated by the exposure number. The class alternates across exposures, and there is no transferable chemical feature. A nearest-neighbor classifier can memorize the class of an exposure if other windows from that exposure are already in training.

Compare a split that places windows from every exposure into training with a split that holds out entire future exposures. The algorithm is unchanged. Only the question asked by the test changes.

<a id="section-part-b-additive-drift-and-a-reference-blank"></a>

## Part B: additive drift and a reference blank

A second dataset has a genuine one-dimensional class signal centered at -1 or +1 response unit. A known additive offset grows by batch. The reference blank observes that offset independently of the class. Compare a frozen model on raw values with a model on blank-corrected values. Do not use future class labels to fit either model.

Copy this complete code into a Python session or a temporary file:

```python
from statistics import mean


def accuracy(truth, prediction):
    assert len(truth) == len(prediction) and truth
    return sum(a == b for a, b in zip(truth, prediction)) / len(truth)


def predict_nearest(train, test):
    # Each row is (feature, label, exposure, window).
    return [min(train, key=lambda r: abs(r[0] - x[0]))[1] for x in test]


rows = []
for exposure in range(12):
    label = exposure % 2
    for window in range(8):
        # Deliberate nuisance fingerprint, not a chemical concentration.
        feature = 10.0 * exposure + 0.01 * window
        rows.append((feature, label, exposure, window))

within_train = [r for r in rows if r[3] < 6]
within_test = [r for r in rows if r[3] >= 6]
future_train = [r for r in rows if r[2] < 8]
future_test = [r for r in rows if r[2] >= 8]

within_score = accuracy([r[1] for r in within_test],
                        predict_nearest(within_train, within_test))
future_score = accuracy([r[1] for r in future_test],
                        predict_nearest(future_train, future_test))
print(f"A: shared-exposure accuracy = {within_score:.3f}")
print(f"A: new-exposure accuracy    = {future_score:.3f}")

# Independent synthetic reference blanks are available at every batch.
drift_rows = []
for batch in range(6):
    blank = 0.7 * batch
    for label in (0, 1):
        chemical_signal = -1.0 if label == 0 else 1.0
        for perturbation in (-0.1, 0.0, 0.1):
            raw = chemical_signal + blank + perturbation
            drift_rows.append((raw, blank, label, batch))

train = [r for r in drift_rows if r[3] <= 1]
test = [r for r in drift_rows if r[3] >= 4]


def centroid_predictions(training, testing, compensate):
    def feature(row):
        return row[0] - row[1] if compensate else row[0]
    centers = {label: mean(feature(r) for r in training if r[2] == label)
               for label in (0, 1)}
    return [min(centers, key=lambda label: abs(feature(r) - centers[label]))
            for r in testing]


raw_score = accuracy([r[2] for r in test],
                     centroid_predictions(train, test, False))
corrected_score = accuracy([r[2] for r in test],
                           centroid_predictions(train, test, True))
print(f"B: future raw accuracy     = {raw_score:.3f}")
print(f"B: future corrected score  = {corrected_score:.3f}")
assert within_score == 1.0 and future_score == 0.5
assert raw_score == 0.5 and corrected_score == 1.0
```

Expected output:

```text
A: shared-exposure accuracy = 1.000
A: new-exposure accuracy    = 0.500
B: future raw accuracy     = 0.500
B: future corrected score  = 1.000
```

<a id="section-interpret-the-results"></a>

## Interpret the results

In Part A, a test window has a near-identical neighbor from the same exposure. Perfect accuracy therefore reflects exposure recognition. For the held-out exposures, the nearest training exposure has one fixed label and half the future exposures have the other label. The 50% result exposes the absence of a transferable chemical relationship.

In Part B, subtracting the independent blank removes exactly the disturbance that was constructed. The experiment does not establish that blank correction fixes sensor aging in general. Changes in sensitivity, selectivity, recovery, or nonlinearity require different evidence. The perfect corrected score depends on the intentionally ideal reference and separated class signals.

The distinction between group-aware and time-aware evaluation is supported by the official [cross-validation documentation](https://scikit-learn.org/stable/modules/cross_validation.html). Use its methods as implementations of an experimental design, not as a substitute for deciding which observations are independent.

<a id="section-required-extensions"></a>

## Required extensions

1. Add random measurement noise using a fixed seed and report results across several seeds, not only the most favorable one.
2. Add error to the reference blank and determine when correction becomes unreliable.
3. Change the class sensitivity with batch. Explain why a blank at zero concentration cannot identify the changed slope.
4. Add a genuinely chemical feature to Part A. Compare the performance of that feature alone with the nuisance feature alone.
5. Introduce a third unknown class. Add an abstention rule chosen on development data, then report both coverage and accepted-case accuracy.

For extension 3, one possible model is `raw = gain(batch)*chemical_signal + blank + noise`. Estimate the gain with independent reference concentrations rather than future test labels. If gain becomes small relative to noise, even a perfectly known correction amplifies uncertainty.

<a id="section-deliverable-and-assessment"></a>

## Deliverable and assessment

Submit a Markdown report with the two split diagrams, the expected output, extension results, and a one-paragraph deployment protocol. Identify the independent unit and describe all information available to the model at evaluation time.

Credit is based on correct split reasoning (30%), reproducible code and reported seeds (20%), interpretation of drift and correction limits (30%), and a practical validation plan (20%). High accuracy without an appropriate split earns no credit for generalization.

**Design artifact carried forward:** a data-partition manifest listing exposure, device, day, and site boundaries, plus a rule preventing test data from influencing preprocessing. Add it to the [design studio](../design-studio.md).

**Optional public-data extension:** use the [UCI drift dataset](https://archive.ics.uci.edu/dataset/224/gas+sensor+array+drift+dataset) only after reviewing its reuse terms and the [dataset notes](../references/olfaction-and-data.md). Its metal-oxide measurements are a methods benchmark; conclusions do not directly establish electrochemical performance.

<!-- course-footer:start -->
---

[Previous: Lab 05: array diversity and shared error](05-array-design.md) · [All labs](index.md) · [Next: Lab 07. Transport timing and sensor response mismatch](07-plume-and-timing.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
