---
layout: default
title: 'Lab 04: calibration and uncertainty'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [Modules](../modules/index.md) · [**Labs**](index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Labs](index.md) / Lab 04: calibration and uncertainty

**Lab 04 of 8**

<!-- course-navigation:end -->

# Lab 04: calibration and uncertainty

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Question](#section-question)
- [Calculation](#section-calculation)
- [Tasks](#section-tasks)
- [Worked interpretation](#section-worked-interpretation)
- [Design decision carried forward](#section-design-decision-carried-forward)

</details>
<!-- course-toc:end -->

**Time:** 3 hours. **Preparation:** Modules 10–11 and introductory statistics.

<a id="section-question"></a>

## Question

What is established by a good linear calibration, and what remains unknown? Fit invented measurements, inspect residuals, compute an illustrative blank-based detection estimate, and examine a new-day offset that the original regression cannot remove.

The concentration unit is a fictitious arbitrary concentration unit, abbreviated `cu`. Response is nA. Neither represents a particular chemical system.

| c (cu) | Response (nA) |
| --- | --- |
| 0 | 1.1 |
| 1 | 2.8 |
| 2 | 5.1 |
| 3 | 6.9 |
| 4 | 9.2 |
| 5 | 10.8 |
| 6 | 13.1 |
| 7 | 14.9 |

<a id="section-calculation"></a>

## Calculation

```python
from math import sqrt
from statistics import mean, stdev
x = [0,1,2,3,4,5,6,7]
y = [1.1,2.8,5.1,6.9,9.2,10.8,13.1,14.9]
xb, yb = mean(x), mean(y)
Sxx = sum((v-xb)**2 for v in x)
m = sum((a-xb)*(b-yb) for a,b in zip(x,y))/Sxx
b = yb-m*xb
res = [v-(b+m*c) for c,v in zip(x,y)]
s = sqrt(sum(e*e for e in res)/(len(x)-2))
blank = [0.97,1.02,1.01,0.99,1.03,0.98]
s_blank = stdev(blank)
illustrative_lod = 3*s_blank/abs(m)
y_unknown = 7.05
c_est = (y_unknown-b)/m
# Local delta-method approximation, one future response, no x uncertainty.
u_c = s/abs(m)*sqrt(1+1/len(x)+(c_est-xb)**2/Sxx)
print(f"slope={m:.6f} nA/cu intercept={b:.6f} nA")
print(f"residual SD={s:.6f} nA")
print("residuals:", [round(v,6) for v in res])
print(f"illustrative 3s blank estimate={illustrative_lod:.6f} cu")
print(f"unknown estimate={c_est:.6f} cu approximate u={u_c:.6f} cu")
print(f"0.5 nA new-day offset creates error={0.5/m:.6f} cu")
assert 1.9 < m < 2.1
assert 2.9 < c_est < 3.1
```

The fit should yield a slope near 2 nA/cu and an unknown estimate near 3 cu. The code's uncertainty is an illustrative local approximation using the linear calibration residuals and leverage. It assumes independent homoscedastic response errors, negligible reference-concentration uncertainty, an adequate linear model, and a future observation from the same population. It is not a complete uncertainty budget.

<a id="section-tasks"></a>

## Tasks

1. Derive the least-squares slope and intercept from the two normal equations.
2. Plot the residuals or inspect their signs. Is a high coefficient of determination enough to establish low-concentration detection?
3. Explain why the separate blank standard deviation is much smaller than the calibration residual standard deviation in this invented example. What evidence would be needed before using it for detection performance?
4. Add 0.5 nA to every reading on a new day. Evaluate the concentration error if the old calibration is used unchanged.
5. Identify the covariance between estimated slope and intercept. Explain how the compact prediction-uncertainty expression accounts for calibration leverage without treating those parameters as independent.
6. Design a study to determine whether the response variance increases with concentration. Describe when a weighted fit might be appropriate.

<a id="section-worked-interpretation"></a>

## Worked interpretation

A small blank fluctuation can coexist with poor between-run reproducibility. The `3*s_blank/m` calculation illustrates a common convention; it does not establish false-positive and false-negative probabilities for the whole method. The calibration contains few low-level measurements and no independent recovery, selectivity, storage, or device-to-device assessment.

A 0.5 nA offset produces approximately 0.25 cu error at every concentration in this linear model. Repeating the unknown many times reduces independent random scatter but does not remove that offset. A new-day blank or check standard can detect some changes, though a zero check alone cannot establish that gain and selectivity remain stable.

For homoscedastic least squares, `cov(b,m)=-xb*s^2/Sxx`. Ignoring this term while propagating slope and intercept independently can produce misleading intervals. The leverage term in the code comes from the fitted response variance at a specified concentration; inverse calibration also requires attention to its nonlinear character when slope uncertainty is substantial.

<a id="section-design-decision-carried-forward"></a>

## Design decision carried forward

Prepare a calibration table covering reference provenance, levels, replicates, device groups, humidity/temperature conditions, blanks, independent test samples, and acceptance criteria. Identify which uncertainty terms are random, shared, or correlated. Choose an explicit recalibration trigger.

<!-- course-footer:start -->
---

[Previous: Lab 03: impedance and identifiability](03-impedance-and-identifiability.md) · [All labs](index.md) · [Next: Lab 05: array diversity and shared error](05-array-design.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
