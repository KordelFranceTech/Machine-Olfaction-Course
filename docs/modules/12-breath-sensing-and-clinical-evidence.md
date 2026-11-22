---
layout: default
title: '12 · Breath sensing and clinical evidence'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [**Modules**](index.md) · [Labs](../labs/index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Modules](index.md) / 12 · Breath sensing and clinical evidence

**Module 12 of 18**

<!-- course-navigation:end -->

# 12 · Breath sensing and clinical evidence

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Learning outcomes](#section-learning-outcomes)
- [1. From metabolism to a sensor feature](#section-1-from-metabolism-to-a-sensor-feature)
- [2. Three separate validation questions](#section-2-three-separate-validation-questions)
- [3. State the intended use before selecting metrics](#section-3-state-the-intended-use-before-selecting-metrics)
- [4. Worked example: prevalence changes the meaning of a positive](#section-4-worked-example-prevalence-changes-the-meaning-of-a-positive)
- [5. Study design that tests generalization](#section-5-study-design-that-tests-generalization)
- [6. Worked example: precision and sample size](#section-6-worked-example-precision-and-sample-size)
- [7. Recent evidence: read the design, not only the AUC](#section-7-recent-evidence-read-the-design-not-only-the-auc)
- [8. Calibration, utility, and uncertainty in model outputs](#section-8-calibration-utility-and-uncertainty-in-model-outputs)
- [9. Ethics, privacy, and scope of classroom work](#section-9-ethics-privacy-and-scope-of-classroom-work)
- [10. Design decision carried forward](#section-10-design-decision-carried-forward)
- [11. Exercises and worked answers](#section-11-exercises-and-worked-answers)

</details>
<!-- course-toc:end -->

Breath is attractive because it can carry information about chemistry within and around the body. The engineering challenge is to preserve and measure that information. The clinical challenge is different: determine whether a result improves a defined decision for a defined population. A detectable molecule, a statistically different group average, and a useful diagnostic test are three distinct achievements.

**Level and time:** upper-division undergraduate to beginning graduate; 6–8 hours. **Prerequisites:** [sampling](07-sampling-and-fluidics.md), [calibration and uncertainty](11-calibration-and-uncertainty.md), conditional probability, and basic study design. Activities use published aggregate results and synthetic examples; they do not require collecting human samples.

<a id="section-learning-outcomes"></a>

## Learning outcomes

- Separate analytical validation, clinical validation, and clinical utility.
- Explain how physiology, ambient air, and sampling affect breath measurements.
- Calculate sensitivity, specificity, predictive values, and simple precision estimates.
- Critically compare internal, temporal, and external validation.
- Draft a responsible evidence plan for a proposed breath-sensing application.

<a id="section-1-from-metabolism-to-a-sensor-feature"></a>

## 1. From metabolism to a sensor feature

A plausible chain is:

```text
biological process -> production or uptake of compounds
     -> transport in blood and tissues -> exchange in airways
     -> exhaled sample -> sample conditioning -> electrical response
     -> model output -> possible clinical decision
```

Every step can vary without a change in the disease of interest. Diet, medications, exercise, ambient exposure, oral processes, and comorbid conditions can change measured chemistry. Ventilation, blood flow, airway exchange, and sampling fraction can change how a systemic compound appears in breath.

A mechanistic model helps explain why simple subtraction of room-air concentration is not always sufficient. [Unterkofler et al.](https://doi.org/10.1088/1752-7155/9/3/036002) developed and tested a physiological model that explicitly incorporates inhaled VOC concentration. Its assumptions and studied compounds limit its scope; it should not be applied indiscriminately to every breath analyte.

The [ERS technical standard](https://doi.org/10.1183/13993003.00965-2016) supplies professional guidance on standardizing collection and analysis. Standardization improves comparability, but even perfectly comparable measurements need clinical evidence before being used for diagnosis.

<a id="section-2-three-separate-validation-questions"></a>

## 2. Three separate validation questions

**Analytical validity:** does the instrument measure its specified chemical or electrical quantity with adequate recovery, precision, selectivity, and uncertainty? The comparison might be to an established laboratory method or a characterized reference material.

**Clinical validity:** in the intended population, how well does the output relate to the condition or outcome of interest? This requires a justified reference standard, representative participants, and evaluation that avoids using the test data to tune the result.

**Clinical utility:** does using the test improve decisions or outcomes compared with the current pathway, considering errors, downstream testing, burden, and costs? High discrimination alone cannot answer this question.

A sensor array may classify a breath pattern without identifying individual molecules. That can still be a valid research approach, but the feature should be called a pattern or model output rather than an identified biomarker molecule. Chemical identification requires independent analytical evidence. Similarly, a breath pattern associated with infection need not be a direct measurement of a pathogen; it may reflect host response or other correlated processes.

<a id="section-3-state-the-intended-use-before-selecting-metrics"></a>

## 3. State the intended use before selecting metrics

A triage test, a population-screening test, a confirmatory test, and a monitoring tool face different requirements. A triage tool may aim to reduce unnecessary follow-up while missing very few cases. A monitoring tool may emphasize within-person change. A population screen operates at a different prevalence from a specialist referral clinic.

Define the population, setting, role, reference standard, timing, and consequences of each possible result. Then select a threshold and metrics. Choosing a cutoff after examining the final evaluation cohort makes the reported performance optimistic unless that selection is explicitly accounted for.

For binary results:

```text
sensitivity = TP / (TP + FN)
specificity = TN / (TN + FP)
PPV = TP / (TP + FP)
NPV = TN / (TN + FN)
```

Sensitivity and specificity condition on reference status. Positive and negative predictive values condition on the test result. Even sensitivity and specificity can change across populations because case severity, competing conditions, and measurement circumstances change; they are not universal constants attached to the instrument.

<a id="section-4-worked-example-prevalence-changes-the-meaning-of-a-positive"></a>

## 4. Worked example: prevalence changes the meaning of a positive

Consider an invented study setting with 10,000 people, 1% prevalence, 90% sensitivity, and 95% specificity. These are classroom assumptions, not performance claims for a device.

| Reference status | Test positive | Test negative | Total |
| --- | ---: | ---: | ---: |
| Condition present | 90 | 10 | 100 |
| Condition absent | 495 | 9,405 | 9,900 |
| Total | 585 | 9,415 | 10,000 |

```text
PPV = 90/585 = 15.4%
NPV = 9405/9415 = 99.89%
```

Most positive results are false positives in this example, despite apparently strong sensitivity and specificity. The high NPV partly reflects the low prevalence. At 20% prevalence with the same assumed sensitivity and specificity:

```text
PPV = (0.90 × 0.20) / [(0.90 × 0.20) + (0.05 × 0.80)]
    = 81.8%
```

This arithmetic is why performance in a referral clinic cannot be directly translated into population-screening predictive values. It also shows why a positive research signal should not be presented as an individual diagnosis.

<a id="section-5-study-design-that-tests-generalization"></a>

## 5. Study design that tests generalization

An internal random split estimates performance under a particular sharing of the original dataset. It may not expose differences between sites, times, devices, or clinical pathways. A temporal test set evaluates later data. An external cohort can test transfer across a meaningful boundary, provided the model and threshold are fixed before evaluation.

Keep repeated measurements from one participant together. If one person's breaths appear in both training and test sets, the model may recognize that person. Similar leakage occurs when preprocessing, feature selection, imputation, or normalization uses the entire dataset before splitting.

A case-control comparison between very ill patients and exceptionally healthy volunteers can exaggerate separation relative to the actual clinical problem. Diseased controls and realistic alternative diagnoses may be essential. Record who was excluded, why samples failed, and whether indeterminate results were counted. Removing every difficult sample can make a system appear more reliable than its operating workflow.

[STARD 2015](https://pmc.ncbi.nlm.nih.gov/articles/PMC4623764/) provides a primary reporting framework for diagnostic-accuracy studies. [TRIPOD+AI (2024)](https://pmc.ncbi.nlm.nih.gov/articles/PMC11019967/) addresses transparent reporting of clinical prediction models using regression or machine learning. Reporting completeness helps readers evaluate a study; adherence to a checklist does not itself prove low bias or clinical usefulness.

<a id="section-6-worked-example-precision-and-sample-size"></a>

## 6. Worked example: precision and sample size

Suppose a synthetic evaluation correctly identifies 90 of 100 reference-positive participants. The estimated sensitivity is 90%. A normal approximation gives standard error:

```text
SE ≈ sqrt[p_hat(1 - p_hat)/n]
   = sqrt(0.9 × 0.1/100) = 0.03
```

A more appropriate bounded interval, such as the Wilson interval, is approximately 82.6% to 94.5% at 95% confidence. “90% sensitivity” is therefore not a precise known constant. Report the numerator, denominator, interval method, and interval.

For a rough planning exercise, target a margin of error `d = 0.05` around anticipated sensitivity `p = 0.90`:

```text
n_positive ≈ 1.96^2 p(1-p)/d^2
           = 138.3, rounded up to 139 reference-positive participants
```

This is a simple approximation, not a complete clinical sample-size calculation. If only 10% of recruits have the condition, obtaining 139 positive participants would require about 1,390 recruits before accounting for exclusions, missing reference outcomes, clustering, or other design requirements. Precision of specificity, subgroup performance, and external validation may require additional participants.

<a id="section-7-recent-evidence-read-the-design-not-only-the-auc"></a>

## 7. Recent evidence: read the design, not only the AUC

Two original studies illustrate progress toward more demanding evaluation. They concern electronic noses; their results should not be transferred to an unrelated electrochemical architecture.

[Lee et al. (2024)](https://doi.org/10.1186/s12931-024-02840-z) prospectively recruited 231 participants across two centers. Direct transfer to the second site's cohort produced an AUC of 0.61; augmentation and fine-tuning strategies improved reported results. The learning question is how much target-site information each strategy used and what remains independently evaluated. Adaptation can be useful, but an adapted model and an untouched external validation answer different questions.

[Buma et al. (2025)](https://doi.org/10.1016/j.annonc.2025.03.013) evaluated 364 participants with clinical or radiological suspicion of lung cancer in two outpatient settings. For the existing model, reported AUC differed between the COPD subgroup and the full cohort, 0.92 and 0.80 respectively. This is an instructive example of performance depending on the evaluation population. It does not establish effectiveness as a general-population screening program.

These examples support studying cross-site robustness and prospective evaluation as central engineering goals. They do not establish that every breath feature is disease-specific, that calibration transfers automatically, or that a classifier replaces a clinical reference standard. For a current literature review, inspect later independent studies, corrections, and exact deployment conditions rather than constructing a ranking from incomparable headline metrics.

<a id="section-8-calibration-utility-and-uncertainty-in-model-outputs"></a>

## 8. Calibration, utility, and uncertainty in model outputs

A model can rank participants well while producing poorly calibrated probabilities. If outputs near 0.8 correspond to only 50% observed outcomes, decisions based on those probabilities may be inappropriate. Evaluate calibration separately from discrimination, using data that were not used to fit the calibration mapping.

AUC summarizes ranking over thresholds. It does not identify the useful operating point, show how many samples fail, or quantify the consequences of a false reassurance. Include the fixed-threshold confusion matrix, uncertainty intervals, failed-test rate, and performance in relevant subgroups. Decision analysis can compare a proposed pathway with existing alternatives using explicit assumptions about benefits and harms.

An uncertainty estimate from a neural network is not automatically a reliable measure of clinical uncertainty. Test whether it identifies actual failure cases and distribution shifts. A system may need to abstain when input quality or population applicability is insufficient.

<a id="section-9-ethics-privacy-and-scope-of-classroom-work"></a>

## 9. Ethics, privacy, and scope of classroom work

The [World Medical Association Declaration of Helsinki, revised in 2024](https://www.wma.net/policies-post/wma-declaration-of-helsinki/), is a primary ethics framework for medical research involving human participants. An institutionally approved study needs appropriate oversight, consent arrangements, privacy protections, and a justified protocol. This course's exercises use synthetic data or published aggregate evidence and do not authorize human recruitment or clinical testing.

Breath records can contain sensitive inferences even when names are removed. Minimize identifiers, control access, define retention, and document permitted uses. Keep an individual's care separate from an unvalidated classroom model. A scientifically interesting output is not a reason to deliver an unsupported health judgment to a participant.

<a id="section-10-design-decision-carried-forward"></a>

## 10. Design decision carried forward

In the [design studio](../design-studio.md), the student project may produce a validated chemical measurement or a research pattern score. Specify exactly which one it produces and what the user interface may say. Your deliverable is an evidence ladder separating bench performance, analytical validation, clinical validation, and utility; a synthetic participant-flow diagram; and a locked evaluation plan. Compare the evidence required for environmental demonstration with that required for a clinical intended use. Progression requires independent evidence at each level. A mouthpiece and a classifier do not, by themselves, make a diagnostic instrument.

<a id="section-11-exercises-and-worked-answers"></a>

## 11. Exercises and worked answers

1. **Metric distinction.** Is `nA/ppb` clinical sensitivity? **Answer:** no. It is a possible unit of analytical sensitivity; clinical sensitivity is a proportion conditional on reference-positive status.
2. **Prevalence.** With 50% prevalence, 90% sensitivity, and 95% specificity, calculate PPV. **Answer:** `0.45/(0.45 + 0.025) = 94.7%`. The changed predictive value does not mean the instrument changed.
3. **Leakage.** Each participant supplies ten traces, and traces are randomly split. **Answer:** group by participant before fitting any data-dependent preprocessing or model. For deployment across sites or time, include those additional held-out boundaries.
4. **External adaptation.** A model is fine-tuned on half the new site's labels and evaluated on the rest. **Answer:** describe it as target-site adaptation followed by held-out evaluation; do not imply zero-data transfer.
5. **Evidence plan.** A sensor separates two clinical groups in one hospital. **Answer criterion:** propose analytical interference checks, a fixed model and threshold, representative controls, prospective external data, failure accounting, and a plan for testing whether use improves a defined decision.

<!-- course-footer:start -->
---

[Previous: 11 · Calibration and uncertainty](11-calibration-and-uncertainty.md) · [All modules](index.md) · [Next: 13. Arrays, selectivity, and identifiable mixtures](13-arrays-and-selectivity.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
