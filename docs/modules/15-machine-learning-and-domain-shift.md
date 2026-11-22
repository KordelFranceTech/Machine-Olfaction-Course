---
layout: default
title: '15. Machine learning, uncertainty, and domain shift'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [**Modules**](index.md) · [Labs](../labs/index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Modules](index.md) / 15. Machine learning, uncertainty, and domain shift

**Module 15 of 18**

<!-- course-navigation:end -->

# 15. Machine learning, uncertainty, and domain shift

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Learning outcomes](#section-learning-outcomes)
- [Define the task before choosing the algorithm](#section-define-the-task-before-choosing-the-algorithm)
- [The unit of independence controls the evaluation](#section-the-unit-of-independence-controls-the-evaluation)
- [Build a simple baseline that can fail transparently](#section-build-a-simple-baseline-that-can-fail-transparently)
- [A four-part development protocol](#section-a-four-part-development-protocol)
- [Performance is a collection of quantities](#section-performance-is-a-collection-of-quantities)
- [Probability calibration and abstention](#section-probability-calibration-and-abstention)
- [Drift and the moving measurement function](#section-drift-and-the-moving-measurement-function)
- [Public data as a methods laboratory](#section-public-data-as-a-methods-laboratory)
- [Design decision carried forward](#section-design-decision-carried-forward)
- [Problems and worked answers](#section-problems-and-worked-answers)

</details>
<!-- course-toc:end -->

A classifier can be excellent at recognizing the circumstances of an experiment while being poor at recognizing chemistry. If one gas is measured on Monday and another on Friday, a model may learn drift. If one class is always humid, it may learn water. The central engineering problem is to define the future decision first and then design a dataset that tests that decision honestly.

**Prerequisites:** vectors, basic probability, calibration, arrays, and feature extraction. **Suggested effort:** 3 hours of study and 3 hours for the linked lab.

<a id="section-learning-outcomes"></a>

## Learning outcomes

- Specify a prediction target, unit of independence, and deployment population.
- Separate training, model selection, calibration, and final evaluation.
- Compare physically motivated baselines with flexible models.
- Explain drift, domain shift, open-set recognition, and abstention.
- Report performance with its coverage, uncertainty, and failure conditions.

<a id="section-define-the-task-before-choosing-the-algorithm"></a>

## Define the task before choosing the algorithm

Chemical classification, concentration regression, anomaly detection, and medical inference are different tasks. A model trained to distinguish pure laboratory gases cannot automatically quantify mixtures or determine why a person produced a breath signal. Its target label must match the question the device is intended to answer.

A useful specification has five parts: input measurements, output, sample population, operating conditions, and acceptable consequences of error. For example: “Using a valid, quality-checked array exposure, distinguish synthetic class A from class B within the stated temperature and humidity envelope; otherwise return indeterminate.” This is testable. “Recognize odors” is too broad to support an experimental design.

Separate chemical identity from perceptual description. Molecular-structure models can predict aspects of human odor descriptions, but they operate on molecular information rather than directly measuring an unknown environment. Lee and colleagues' principal odor map study is an important example of structure-to-perception learning, with a defined prospective evaluation. It does not supply a universal decoder for arbitrary sensor voltages or all mixtures. [Lee et al., 2023](https://pubmed.ncbi.nlm.nih.gov/37651511/)

<a id="section-the-unit-of-independence-controls-the-evaluation"></a>

## The unit of independence controls the evaluation

Suppose one exposure produces 1,000 time samples. Those samples share the same delivered gas, device, chamber, and preparation. Splitting the rows at random puts highly related observations into both training and test sets. The apparent sample count is 1,000, but the number of independent exposures is one.

Potential grouping variables include exposure, collection session, person, sample reservoir, sensor cartridge, manufacturing lot, and site. The correct split depends on the intended generalization. If the device must work on a new cartridge, holding out new time windows from an old cartridge is insufficient. If it must work next month, a random split across all months hides the temporal challenge.

Official cross-validation tools distinguish group-aware and time-aware splitting. Their availability does not choose the right grouping for you; that comes from the data-generating process. [scikit-learn, cross-validation](https://scikit-learn.org/stable/modules/cross_validation.html)

### Worked example: why many windows are not many experiments

Assume 20 exposures, each divided into 100 adjacent windows. A row-level split can provide 1,600 training windows and 400 test windows while exposing the model to every exposure during training. A group split might instead use 16 whole exposures for training and four for testing. Both have 2,000 rows, but only the second asks whether patterns transfer to unseen exposures.

Even the group split leaves uncertainty when there are only four test exposures. If all four are correct, that is encouraging but not a precise estimate of reliability. The evaluation should report four independent test exposures, not claim certainty from hundreds of overlapping windows.

<a id="section-build-a-simple-baseline-that-can-fail-transparently"></a>

## Build a simple baseline that can fail transparently

Start with a constant predictor, then a physically motivated linear model, then a modest nonlinear model if needed. For classification, nearest-centroid or regularized logistic regression can reveal whether classes are already separable. For regression, compare against predicting the training mean and against the calibration model from the measurement physics.

A nearest-centroid classifier uses the average feature vector for each class and predicts the closest centroid under a specified metric. Standardization is often needed, but its means and scales must be estimated from training data. Fit imputation, feature selection, and normalization within the training pipeline. [scikit-learn, preprocessing pitfalls](https://scikit-learn.org/stable/common_pitfalls.html)

A neural network is reasonable when the dataset and question justify its flexibility, such as learning temporal patterns from many independent exposures. It also introduces more opportunities for tuning, hidden shortcuts, and overfitting. Architecture size is not evidence that the model learned chemistry.

<a id="section-a-four-part-development-protocol"></a>

## A four-part development protocol

1. **Training:** fit model parameters using the designated development data.
2. **Validation:** select features, regularization, architecture, and stopping rules using independent development groups or nested cross-validation.
3. **Calibration and threshold selection:** estimate probability calibration and choose decision thresholds using held-out data without touching the final test labels.
4. **Final test:** evaluate the frozen pipeline once on independent data representing the intended deployment challenge.

When data are scarce, the roles can be implemented by nested grouped folds, but all reported choices must remain inside the appropriate outer training partition. A final test set becomes development data once its outcomes repeatedly guide model changes. Preserve a genuinely new evaluation after substantial revision.

<a id="section-performance-is-a-collection-of-quantities"></a>

## Performance is a collection of quantities

For a two-class example, treat A as the positive class. Suppose the following counts arise from 100 independent synthetic cases:

| True class | Predicted A | Predicted B |
| --- | ---: | ---: |
| A | 45 | 5 |
| B | 10 | 40 |

Accuracy is `(45 + 40)/100 = 0.85`. Sensitivity is `45/50 = 0.90`; specificity is `40/50 = 0.80`; positive predictive value is `45/55 = 0.818`. These answer different questions. Changing class prevalence changes predictive values even if conditional error rates remain the same.

For regression, report residuals against concentration, humidity, time, device, and predicted value. A single root-mean-square error can hide a large bias near the decision boundary. Report units and the tested range. Extrapolation beyond that range is a new scientific question.

Confidence intervals should respect the dependence structure. Resampling windows independently from the same exposure yields overly narrow intervals. Resample independent groups when using a grouped bootstrap, and explain what population those groups represent.

<a id="section-probability-calibration-and-abstention"></a>

## Probability calibration and abstention

A score of 0.9 is useful as a probability only if cases with similar scores have approximately the stated frequency of the event in the relevant population. Guo and colleagues demonstrated that strong classification performance can coexist with poor probability calibration and studied post-processing approaches. Their experiments were not a validation of any chemical sensor. [Guo et al., 2017](https://proceedings.mlr.press/v70/guo17a.html)

Temperature scaling changes neural-network logits before the softmax. It can improve calibration on held-out data but does not create knowledge of unseen chemicals or protect against arbitrary domain shift. Reliability diagrams, Brier scores, and negative log-likelihood provide complementary checks. Report sample counts within bins rather than only a smooth curve.

An abstaining model returns “indeterminate” when evidence is insufficient. Define separately: invalid measurement, outside-calibration conditions, unknown response pattern, and ambiguous supported classes. These states can require different actions.

### Worked example: accuracy among accepted cases

A system evaluates 100 cases, accepts 90, and gets 80 of the accepted cases correct. Its coverage is 90%; its accuracy among accepted cases is `80/90 = 88.9%`; it makes a correct accepted decision on 80% of all cases. Reporting only 88.9% hides the ten abstentions. If the rejected cases systematically come from one environment or user group, that matters to both utility and equity.

Novelty detection estimates whether a new observation resembles the reference distribution. It is not a chemical identification method: an unfamiliar vector can result from a new gas, a failed sensor, or a changed environment. [scikit-learn, novelty and outlier detection](https://scikit-learn.org/stable/modules/outlier_detection.html)

<a id="section-drift-and-the-moving-measurement-function"></a>

## Drift and the moving measurement function

Drift can change the baseline, sensitivity, selectivity, dynamics, or noise. Label shift changes the class proportions; covariate shift changes the inputs; a changing relationship between inputs and labels creates a more difficult problem. These categories can overlap in sensor systems.

Blank subtraction can remove some additive drift but cannot generally fix changing sensitivity. Suppose the original response is `y = 2*c + b`. If aging changes it to `y = c + b_new`, subtracting a new blank leaves a factor-of-two concentration error when the old calibration slope is used. Reference measurements at multiple concentrations are needed to detect this change.

Adaptive learning requires a source of trustworthy information. Updating a model using its own unverified predictions can reinforce errors. A maintenance policy should specify which references or labels authorize an update, how it is validated, and how rollback works. Preserve the old model and record the changed operating domain.

<a id="section-public-data-as-a-methods-laboratory"></a>

## Public data as a methods laboratory

The UCI drift dataset contains 13,910 measurements from 16 metal-oxide sensors for six gases; an extension includes concentration labels. These are useful for developing evaluation methods, not for establishing electrochemical device performance. The repository pages currently contain a CC BY 4.0 license statement alongside legacy research-only wording. Resolve intended reuse terms with the repository or data creators before redistribution or commercial use; this curriculum does not redistribute the data. [UCI drift dataset](https://archive.ics.uci.edu/dataset/224/gas+sensor+array+drift+dataset), [concentration extension](https://archive.ics.uci.edu/dataset/270/gas+sensor+array+drift+dataset+at+different+concentrations)

For a temporal benchmark, retain batch metadata, specify training and testing batches, and distinguish a frozen model from an adaptation method. If adaptation accesses unlabeled future inputs, state that explicitly. If it accesses future labels, include the labeling cost. Performance numbers from protocols with different information access are not directly comparable.

<a id="section-design-decision-carried-forward"></a>

## Design decision carried forward

**Choice:** define the device's output contract and the conditions that cause abstention. **Criteria:** independent generalization, required latency, false-alarm cost, missed-event cost, and available calibration labels. **Evidence:** grouped and chronological evaluation, calibration curves, unknown-class challenges, and error analysis by device and environment. **Artifact:** a model card specifying target, inputs, splits, versions, operating envelope, rejection rules, metrics, and update policy. Attach it to the [design studio](../design-studio.md).

<a id="section-problems-and-worked-answers"></a>

## Problems and worked answers

1. **Same person, different breaths:** Can breaths from one person appear in both training and test for a new-person evaluation? **Answer:** No. Hold out people, and consider site and collection session as additional grouping variables.
2. **New cartridge:** A model performs well on future days using the same cartridge. What remains untested? **Answer:** Manufacturing variation and transfer to unseen cartridges or lots.
3. **Baseline adaptation:** Does a new blank correct a sensitivity decrease? **Answer:** No. A blank constrains an offset, not the response slope or selectivity.
4. **Unknown mixture:** A model outputs 0.99 for A on an A+B mixture never seen before. Is this calibrated evidence? **Answer:** Not without a validation domain containing comparable mixtures; high confidence can occur outside the training distribution.
5. **Best algorithm:** A complex model improves random-split accuracy but loses on a future-device test. Which is preferable? **Answer:** Prefer the model supported by the deployment-relevant test, considering uncertainty and operational cost. More complexity is not itself an advantage.

<!-- course-footer:start -->
---

[Previous: 14. Signal processing, time response, and features](14-signal-processing-and-features.md) · [All modules](index.md) · [Next: 16. Biological olfaction, plumes, and active sampling](16-olfaction-and-active-sampling.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
