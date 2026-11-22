---
layout: default
title: 'Lab 02: transport, recovery, and storage'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [Modules](../modules/index.md) · [**Labs**](index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Labs](index.md) / Lab 02: transport, recovery, and storage

**Lab 02 of 8**

<!-- course-navigation:end -->

# Lab 02: transport, recovery, and storage

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Question](#section-question)
- [Calculation](#section-calculation)
- [Tasks](#section-tasks)
- [Worked answers](#section-worked-answers)
- [Engineering discussion](#section-engineering-discussion)
- [Design decision carried forward](#section-design-decision-carried-forward)

</details>
<!-- course-toc:end -->

**Time:** 2–3 hours. **Preparation:** Modules 03 and 07–09.

<a id="section-question"></a>

## Question

Can a sampling chamber produce a faster electrical response while delivering less of the target? This lab separates equilibration speed, transport loss, and sample preservation. Everything is synthetic and dimensionless except the explicitly stated time and volume variables.

Consider a perfectly mixed 20 mL chamber fed at 5 mL/s by a stream whose normalized concentration changes from zero to one. A first-order loss process removes target at rate constant `k`. The model is:

```text
dc/dt = (Q/V)*(c_in-c) - k*c
c(t) = c_in * a/(a+k) * [1-exp(-(a+k)*t)]
a = Q/V
```

This model deliberately omits spatial gradients, saturating adsorption, back-desorption, and nonlinear sensing. It is a useful starting point whose limitations are part of the assignment.

<a id="section-calculation"></a>

## Calculation

```python
from math import exp, log
V = 20.0  # mL
Q = 5.0   # mL/s
rate = Q/V
for loss in [0.0, 0.05, 0.25]:
    tau = 1/(rate+loss)
    recovery = rate/(rate+loss)
    t90_own_plateau = -log(0.1)*tau
    print(f"loss={loss:.2f}/s tau={tau:.3f}s "
          f"recovery={recovery:.3f} t90={t90_own_plateau:.3f}s")
    for t in [0, 2, 5, 10, 20]:
        c = recovery*(1-exp(-t/tau))
        print(f"  t={t:2d}s c={c:.4f}")
# After collection: a separate, sealed storage model.
k_store = 0.002  # 1/s, invented effective loss
for seconds in [0, 60, 300, 600]:
    print(f"storage {seconds:3d}s fraction={exp(-k_store*seconds):.4f}")
assert abs(exp(-k_store*300)-0.5488116361) < 1e-9
```

For loss rates 0, 0.05, and 0.25 per second, recovery is respectively 1, 0.8333, and 0.5. Time constants are 4, 3.3333, and 2 seconds. A faster approach to a lower plateau can therefore conceal a worse sample path. The reported `t90` is 90% of each path's own plateau, not 90% of the inlet concentration.

<a id="section-tasks"></a>

## Tasks

1. Derive the steady-state value by setting `dc/dt=0`.
2. Derive the complete step response using an integrating factor or separation after shifting by the steady state.
3. Increase flow to 10 mL/s at fixed volume and `k=0.05/s`. Calculate recovery and time constant. Explain what the model omits about pressure drop and power.
4. Determine the maximum storage time that preserves at least 95% of target under `k_store=0.002/s`.
5. Design a control that would reveal target contamination originating from the chamber itself.
6. Replace irreversible loss with a reversible surface reservoir. Sketch the additional state equation and predict a qualitative effect during a blank purge.

<a id="section-worked-answers"></a>

## Worked answers

At 10 mL/s, `a=0.5/s`, recovery is `0.5/0.55=0.9091`, and time constant is `1/0.55=1.8182 s`. The benefit comes with unmodeled pumping requirements and possibly altered interface dynamics.

The preservation condition is `exp(-k*t)>=0.95`, giving `t<=-ln(0.95)/k=25.65 s`. This is only a result of the invented first-order model. A real storage qualification needs time-resolved recovery measurements across analytes, humidity, temperature, material lots, and blank conditions.

A reversible model could include surface amount `s` with `ds/dt=k_ads*c-k_des*s`, using units and area/volume factors consistently. Release during a clean-gas purge can produce a long tail. Measuring only the loading phase would miss the memory effect.

<a id="section-engineering-discussion"></a>

## Engineering discussion

A smaller chamber does not always improve the whole measurement. It can reduce residence time while changing the flow field, the amount of sample available, and the relative contribution of surfaces. A low-permeability bag can still have seal leaks. A valve can prevent reverse bulk flow while contributing adsorption and dead volume. Separate the failure mechanisms in the test plan.

<a id="section-design-decision-carried-forward"></a>

## Design decision carried forward

Draw the sample path with a volume and residence-time estimate for each section. Define recovery and storage criteria before choosing a reservoir or conditioning element. Add procedural blanks, immediate-versus-delayed comparisons, and a carryover challenge to the verification matrix.

<!-- course-footer:start -->
---

[Previous: Lab 01: units and the measurement chain](01-units-and-measurement.md) · [All labs](index.md) · [Next: Lab 03: impedance and identifiability](03-impedance-and-identifiability.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
