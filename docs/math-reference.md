---
layout: default
title: 'Mathematics and dimensional reference'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](index.md) · [Start](getting-started.md) · [Modules](modules/index.md) · [Labs](labs/index.md) · [Projects](projects/index.md) · [Library](references/index.md) · [Site map](navigation.md)

[Course home](index.md) / Mathematics and dimensional reference

<!-- course-navigation:end -->

# Mathematics and dimensional reference

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Units and constants](#section-units-and-constants)
- [Composition and ideal gases](#section-composition-and-ideal-gases)
- [Equilibrium and kinetics](#section-equilibrium-and-kinetics)
- [Transport and partitioning](#section-transport-and-partitioning)
- [Fluidics](#section-fluidics)
- [Electrical response and spectra](#section-electrical-response-and-spectra)
- [Calibration and uncertainty](#section-calibration-and-uncertainty)
- [Detection and decisions](#section-detection-and-decisions)
- [Arrays and inverse problems](#section-arrays-and-inverse-problems)
- [Three sanity checks before reporting a number](#section-three-sanity-checks-before-reporting-a-number)

</details>
<!-- course-toc:end -->

This page collects the course's working models. It is a reminder of assumptions, not a substitute for the derivations in the modules. Concentration examples and component values are pedagogical choices, not operating specifications for a device.

<a id="section-units-and-constants"></a>

## Units and constants

| Symbol or quantity | Meaning | Typical SI unit |
| --- | --- | --- |
| c | Amount concentration | mol m^-3 |
| x | Mole fraction | Dimensionless |
| p, P | Partial and total pressure | Pa |
| T | Thermodynamic temperature | K |
| E, eta | Electrode potential and overpotential | V, with a stated reference |
| I, j | Current and current density | A; A m^-2 |
| D | Diffusion coefficient | m^2 s^-1 |
| Q | Volumetric flow rate, at specified conditions | m^3 s^-1 |
| C | Capacitance; avoid confusing with concentration | F |
| R_s, R_ct | Solution and charge-transfer resistance | Ω |
| u, U | Standard and expanded uncertainty in metrology | Same unit as measurand |
| v | Mean flow velocity here | m s^-1 |

Useful approximate constants: `R = 8.31446 J mol^-1 K^-1`, `F = 96485.3 C mol^-1`, `k_B = 1.380649e-23 J K^-1`. Use sufficient precision for the exercise; do not report more significant figures than the input uncertainty supports. The SI definitions and unit conventions are maintained in the [BIPM SI Brochure](https://www.bipm.org/en/publications/si-brochure).

<a id="section-composition-and-ideal-gases"></a>

## Composition and ideal gases

```text
x = n_target / n_total
ppmv = x * 10^6                    ppbv = x * 10^9
p_target = x * P
c_gas = p_target / (R*T)
mass concentration = c_gas * molar mass
```

The ideal-gas relation is an approximation; volume ratios correspond to mole ratios for ideal gases at the same temperature and pressure. Report whether water is included in `n_total`. At `T=298.15 K`, `P=100000 Pa`, and `x=1e-6`, concentration is approximately `4.03e-5 mol m^-3`. For a fictitious molar mass of `50 g mol^-1`, this is about `2.02 mg m^-3`.

<a id="section-equilibrium-and-kinetics"></a>

## Equilibrium and kinetics

For the reduction convention `Ox + n e^- -> Red`:

```text
E = E0 + (R*T/(n*F)) * ln(a_Ox/a_Red)
eta = E - E_equilibrium
j = j0 * [exp(alpha_a*n*F*eta/(R*T))
          - exp(-alpha_c*n*F*eta/(R*T))]
```

The Nernst relation concerns equilibrium activities. The Butler–Volmer form describes a particular electrode-kinetics model; its parameters and transfer-coefficient conventions must be stated. Concentration gradients, uncompensated resistance, adsorption, and multi-step reactions can invalidate a naive fit. At 298.15 K, a decade increase in the activity ratio changes the equilibrium potential by approximately `59.16/n mV`.

<a id="section-transport-and-partitioning"></a>

## Transport and partitioning

```text
J = -D * dc/dz                         one-dimensional diffusive flux
partial c/partial t = D * partial^2 c/partial z^2
rms displacement in one dimension = sqrt(2*D*t)
characteristic transport time ~ L^2/D  scale estimate, not exact t90
c_liquid = Hcp * p_gas                 Hcp in mol m^-3 Pa^-1
K_lg = c_liquid/c_gas = Hcp*R*T         ideal gas, same concentration basis
```

For gas-to-liquid equilibrium, Henry constants require a defined solvent, temperature, and convention. A water value is not an ionic-liquid value. See the author-maintained [Henry's-law compilation](https://acp.copernicus.org/articles/23/10901/2023/). At `L=100 µm` and `D=1e-10 m^2 s^-1`, `L^2/D = 100 s`; changing the length by ten changes the timescale by one hundred.

For an ideal planar diffusion-limited potential step:

```text
I(t) = n*F*A*c_bulk*sqrt(D/(pi*t))
```

This Cottrell result assumes suitable boundary conditions, fast interfacial reaction, and semi-infinite diffusion. Its singularity at zero time is not a physical current specification. Electrode geometry, double-layer charging, finite kinetics, and instrumentation govern the early response.

<a id="section-fluidics"></a>

## Fluidics

```text
v = Q / A_tube
Re = rho*v*d / mu
Pe = v*L/D
residence time = V/Q
Delta P = 128*mu*L*Q/(pi*d^4)
```

The last expression is Hagen–Poiseuille pressure drop for steady fully developed laminar flow of a Newtonian incompressible fluid in a circular tube. Gas use requires pressure changes small enough for the approximation or a compressible-flow treatment. Entries, filters, bends, valves, and pulsation contribute separately.

For a perfectly mixed chamber:

```text
V * dc/dt = Q*(c_in - c) - k_loss*V*c
steady c/c_in = (Q/V)/(Q/V + k_loss)
tau = 1/(Q/V + k_loss)
```

Loss can make the observed response faster while decreasing recovery. A short apparent time constant is not automatically good sample handling.

<a id="section-electrical-response-and-spectra"></a>

## Electrical response and spectra

```text
I_C = C * dE/dt
Z_R = R
Z_C = 1/(j*omega*C) = -j/(omega*C)
omega = 2*pi*f
Z = R_s + R_ct/(1 + j*omega*R_ct*C_dl)
f_peak = 1/(2*pi*R_ct*C_dl)
```

Here `j=sqrt(-1)`; it is not current density. A common Nyquist convention plots `-Im(Z)` against `Re(Z)`. State your sign convention. The simple circuit's semicircle needs neither a chemical identification nor a unique microscopic interpretation.

```text
TIA output-voltage change magnitude = |I| * R_f
ideal transimpedance magnitude = R_f
ideal ADC step = V_span / 2^N
resistor voltage-noise density = sqrt(4*k_B*T*R)
```

An ADC's nominal bit depth does not determine actual system resolution. Noise bandwidth, amplifier current noise, reference drift, and effective number of bits matter. Noise density must be integrated over the relevant transfer function to obtain an RMS noise.

<a id="section-calibration-and-uncertainty"></a>

## Calibration and uncertainty

For a linear signal model `y = b + m*c`:

```text
c_est = (y-b)/m
u_c^2 ≈ (u_y/m)^2 + (u_b/m)^2 + ((y-b)*u_m/m^2)^2
```

This simplified expression neglects covariance. In an actual fitted calibration, slope and intercept are commonly correlated; use the full covariance propagation or a suitable numerical model. The [JCGM publications](https://www.bipm.org/en/committees/jc/jcgm/publications) provide the authoritative metrology framework.

```text
variance(mean of n independent equal-variance observations) = sigma^2/n
variance(mean with equal pairwise correlation rho)
  = sigma^2 * [rho + (1-rho)/n]
```

If `rho=0.5` and `n=10`, variance is `0.55*sigma^2`, not `0.10*sigma^2`. Replication is most valuable when it introduces independent evidence.

<a id="section-detection-and-decisions"></a>

## Detection and decisions

```text
sensitivity = TP/(TP+FN)
specificity = TN/(TN+FP)
precision or PPV = TP/(TP+FP)
PPV = Se*p / [Se*p + (1-Sp)*(1-p)]
```

A sensitivity evaluated in a biased cohort may not transfer to the intended population. Prevalence `p` alone cannot repair a nonrepresentative validation study.

<a id="section-arrays-and-inverse-problems"></a>

## Arrays and inverse problems

```text
y = A*c + b + epsilon
least-squares estimate, when appropriate:
  c_hat = (A^T*A)^-1 * A^T*(y-b)
```

The explicit inverse is a mathematical description, not the preferred numerical implementation for large problems. Full column rank is necessary for an unconstrained unique estimate in this linear model. Poor conditioning amplifies noise even when an inverse exists. Nonnegative concentrations constrain a model but do not create missing physical information.

<a id="section-three-sanity-checks-before-reporting-a-number"></a>

## Three sanity checks before reporting a number

1. **Dimensions:** Does a voltage emerge in volts and a concentration in the intended concentration unit?
2. **Limits:** What happens at zero concentration, infinite flow, zero noise, or identical sensor channels?
3. **Interpretation:** Is the answer an equilibrium value, a transient response, a fitted parameter, or a population-level performance metric?

[Return to the curriculum](curriculum.md) · [Apply these models in the labs](labs/index.md)

<!-- course-footer:start -->
---

[Back to top](#page-top) · [Site map](navigation.md) · [Course home](index.md)
<!-- course-footer:end -->
