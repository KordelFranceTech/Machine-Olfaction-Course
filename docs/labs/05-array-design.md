---
layout: default
title: 'Lab 05: array diversity and shared error'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [Modules](../modules/index.md) · [**Labs**](index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Labs](index.md) / Lab 05: array diversity and shared error

**Lab 05 of 8**

<!-- course-navigation:end -->

# Lab 05: array diversity and shared error

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Question](#section-question)
- [Calculation](#section-calculation)
- [Tasks and reasoning](#section-tasks-and-reasoning)
- [Experimental extension on paper](#section-experimental-extension-on-paper)
- [Design decision carried forward](#section-design-decision-carried-forward)

</details>
<!-- course-toc:end -->

**Time:** 2–3 hours. **Preparation:** Modules 13–14 and basic matrix algebra.

<a id="section-question"></a>

## Question

Which is more useful: several channels that measure almost the same thing, or fewer channels that respond differently? This lab separates two tasks often conflated in array design: reducing noise on one estimate and identifying several unknown components.

Use the linear synthetic model `y=A*c`. The two unknown concentrations are dimensionless teaching quantities. Three candidate response matrices are:

```text
A_diverse = [[1.0, 0.2], [0.1, 1.0]]
A_nearly_parallel = [[1.0, 0.9], [1.0, 0.91]]
A_duplicate = [[1.0, 1.0], [2.0, 2.0]]
```

The first matrix provides substantially different response directions. The second is invertible but nearly redundant. The third is rank deficient.

<a id="section-calculation"></a>

## Calculation

```python
from math import sqrt
def measure(A, c):
    return [sum(a*b for a,b in zip(row,c)) for row in A]
def solve2(A, y):
    a,b = A[0]
    c,d = A[1]
    det = a*d-b*c
    if abs(det) < 1e-12:
        return None
    return [(d*y[0]-b*y[1])/det, (-c*y[0]+a*y[1])/det]
true_c = [1.0, 2.0]
matrices = {
    "diverse": [[1.0,0.2],[0.1,1.0]],
    "nearly_parallel": [[1.0,0.9],[1.0,0.91]],
    "duplicate": [[1.0,1.0],[2.0,2.0]],
}
for name,A in matrices.items():
    y = measure(A,true_c)
    disturbed = [y[0]+0.02,y[1]-0.02]
    estimate = solve2(A,disturbed)
    print(name, "clean", y, "estimated", estimate)
# Equal variance and equal pairwise correlation model for replicated channels.
for rho in [0.0,0.2,0.8]:
    for n in [1,4,16]:
        sd_of_mean = sqrt(rho+(1-rho)/n)
        print(f"rho={rho:.1f} n={n:2d} relative_SD={sd_of_mean:.4f}")
assert solve2(matrices["duplicate"],[3,6]) is None
```

The diverse matrix gives estimates close to `[1,2]` after a small disturbance. The nearly parallel matrix yields a very different answer, including a negative inferred component in this example. Nonnegative constrained fitting can prevent negative output but does not manufacture independent information. The duplicate matrix has no unique two-component solution.

<a id="section-tasks-and-reasoning"></a>

## Tasks and reasoning

**1. Calculate determinants.** They are 0.98, 0.01, and zero. Determinant magnitude depends on scaling and is not a universal conditioning metric, but it is enough to expose the contrast in these equally scaled examples.

**2. Interpret the negative estimate.** It is a symptom of an ill-conditioned inverse problem under disturbance, not evidence that a gas has negative concentration. Possible remedies include a better response basis, more independent measurements, justified constraints, or reporting that the mixture is not identifiable.

**3. Analyze replication.** For equal variance and pairwise correlation 0.8, increasing from one channel to sixteen reduces relative standard deviation only to about 0.9014. With independent noise, sixteen channels would reduce it to 0.25. Shared environmental response dominates the first case.

**4. Distinguish voting from quantification.** A majority vote can improve a binary decision when channel errors are sufficiently independent and their individual performance is adequate. It does not by itself identify a mixture, correct concentration bias, or reject a common contaminant affecting every channel.

**5. Add a nuisance variable.** Extend `c` to include humidity. Explain why two independent outputs cannot generally identify three unconstrained unknowns. A humidity measurement can supply additional information, but its error and the validity of the response model must be included.

<a id="section-experimental-extension-on-paper"></a>

## Experimental extension on paper

Design a mixture grid with two targets, blanks, plausible interferents, and changing humidity. Separate the devices and days used to fit the response matrix from those used to evaluate it. Include combinations outside the training grid and decide in advance which should be rejected as out of scope. Record concentrations and their reference uncertainty; a class label alone is insufficient for quantitative mixture recovery.

<a id="section-design-decision-carried-forward"></a>

## Design decision carried forward

Choose which channels in your architecture provide redundancy, which provide diversity, and which observe nuisance conditions. State the incremental evidence each adds. Eliminate channels justified only by quantity, appearance, or an improvement on a leaked validation split.

<!-- course-footer:start -->
---

[Previous: Lab 04: calibration and uncertainty](04-calibration-and-uncertainty.md) · [All labs](index.md) · [Next: Lab 06. Drift, leakage, and honest validation](06-drift-and-validation.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
