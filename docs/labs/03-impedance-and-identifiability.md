---
layout: default
title: 'Lab 03: impedance and identifiability'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [Modules](../modules/index.md) · [**Labs**](index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Labs](index.md) / Lab 03: impedance and identifiability

**Lab 03 of 8**

<!-- course-navigation:end -->

# Lab 03: impedance and identifiability

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Question](#section-question)
- [Calculation](#section-calculation)
- [Tasks](#section-tasks)
- [Worked reasoning](#section-worked-reasoning)
- [Optional extension](#section-optional-extension)
- [Design decision carried forward](#section-design-decision-carried-forward)

</details>
<!-- course-toc:end -->

**Time:** 3 hours. **Preparation:** Modules 04–06 and complex numbers.

<a id="section-question"></a>

## Question

How much of an interface can you infer from a finite frequency range? You will generate a synthetic spectrum, inspect its limits, and show why a frequency range far above the characteristic frequency cannot reliably estimate charge-transfer resistance.

Use the simple model:

```text
Z(f) = R_s + R_ct / (1 + j*2*pi*f*R_ct*C)
```

The numerical choices `R_s=100 Ω`, `R_ct=10000 Ω`, and `C=1 µF` describe an educational electrical model. They are not a chemical device recipe. The model contains no diffusion element and cannot establish which species is present.

<a id="section-calculation"></a>

## Calculation

```python
from math import pi, atan2, degrees
Rs = 100.0
Rct = 10000.0
C = 1e-6
def z(f, rct=Rct):
    return Rs + rct/(1+1j*2*pi*f*rct*C)
peak = 1/(2*pi*Rct*C)
print(f"characteristic frequency: {peak:.6f} Hz")
print("f_Hz Re_ohm minusIm_ohm magnitude_ohm phase_deg")
for f in [0.1, 1, 10, peak, 100, 1000, 10000]:
    value = z(f)
    print(f"{f:.6g} {value.real:.4f} {-value.imag:.4f} "
          f"{abs(value):.4f} {degrees(atan2(value.imag,value.real)):.4f}")
for f in [0.1, 10000]:
    difference = abs(z(f, 20000)-z(f, 10000))
    print(f"effect of doubling Rct at {f:g} Hz: {difference:.6f} ohm")
assert abs(z(peak).real-5100.0) < 1e-8
assert abs(-z(peak).imag-5000.0) < 1e-8
```

The peak frequency is approximately 15.9155 Hz. At that frequency the point is `(5100,5000)` when plotted as real impedance versus negative imaginary impedance. At low frequency the real part approaches 10,100 Ω; at high frequency it approaches 100 Ω. Doubling `R_ct` produces a large low-frequency change but a very small change at 10 kHz.

<a id="section-tasks"></a>

## Tasks

1. Derive the real and imaginary parts by multiplying by the complex conjugate.
2. Verify the semicircle equation after subtracting `R_s`.
3. Imagine that the absolute complex-impedance uncertainty is 1 Ω at 10 kHz. Compare it with the difference produced by doubling `R_ct`. What follows about estimating that parameter from only high-frequency points?
4. Increase capacitance tenfold. Predict the frequency shift before running the code.
5. Propose two physically different mechanisms that could change the observed capacitance.
6. Explain why repeated spectra taken during ongoing uptake might violate the model's assumptions.

<a id="section-worked-reasoning"></a>

## Worked reasoning

Writing `x=omega*R_ct*C` gives `Re(Z)=R_s+R_ct/(1+x^2)` and `-Im(Z)=R_ct*x/(1+x^2)`. The semicircle's center lies at `R_s+R_ct/2` and its radius is `R_ct/2`. Increasing capacitance by ten shifts the characteristic frequency downward by ten while retaining the ideal circle's diameter.

At high frequency, the parallel branch tends toward the capacitor impedance. A parameter that scarcely changes the predicted output relative to uncertainty is poorly constrained. More decimal places in a nonlinear fit do not solve that problem. Access to lower frequencies may help, provided the physical system remains stationary long enough to measure them.

Changes in wetting, accessible area, interfacial composition, dielectric response, or electrode roughness can alter an effective capacitance. Electrical evidence alone does not distinguish all of them. A second measurement or a controlled perturbation is needed.

<a id="section-optional-extension"></a>

## Optional extension

Add a series lead resistance and compare it with changing `R_s`; they are indistinguishable in this ideal electrical response. Then ask what separate experiment could identify them. This demonstrates structural nonidentifiability: some ambiguities remain even with noise-free data.

<a id="section-design-decision-carried-forward"></a>

## Design decision carried forward

Specify the frequency window, perturbation size, equilibration checks, and independent controls needed for your intended inference. Include a rule that rejects model parameters when the spectrum does not constrain them. Connect this rule to the instrument's “invalid measurement” state.

<!-- course-footer:start -->
---

[Previous: Lab 02: transport, recovery, and storage](02-transport-and-storage.md) · [All labs](index.md) · [Next: Lab 04: calibration and uncertainty](04-calibration-and-uncertainty.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
