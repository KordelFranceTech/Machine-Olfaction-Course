---
layout: default
title: '08 · Humidity, filtration, and conditioning'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [**Modules**](index.md) · [Labs](../labs/index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Modules](index.md) / 08 · Humidity, filtration, and conditioning

**Module 08 of 18**

<!-- course-navigation:end -->

# 08 · Humidity, filtration, and conditioning

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Learning outcomes](#section-learning-outcomes)
- [1. Relative humidity is not water concentration](#section-1-relative-humidity-is-not-water-concentration)
- [2. Worked example: cooling a humid gas](#section-2-worked-example-cooling-a-humid-gas)
- [3. How water changes an electrochemical measurement](#section-3-how-water-changes-an-electrochemical-measurement)
- [4. Filtration and drying solve different problems](#section-4-filtration-and-drying-solve-different-problems)
- [5. Worked example: dilution and a misleading recovery value](#section-5-worked-example-dilution-and-a-misleading-recovery-value)
- [6. Recovery, blanks, capacity, and history](#section-6-recovery-blanks-capacity-and-history)
- [7. Environmental confounding can imitate selectivity](#section-7-environmental-confounding-can-imitate-selectivity)
- [8. Research reading and evidence discipline](#section-8-research-reading-and-evidence-discipline)
- [Design decision carried forward](#section-design-decision-carried-forward)
- [9. Exercises and worked answers](#section-9-exercises-and-worked-answers)

</details>
<!-- course-toc:end -->

Water is often one of the largest chemical components entering a sensing system and one of the strongest influences on its response. Removing it can simplify one problem while creating another: a dryer may also remove the molecules of interest. Good conditioning design asks what transformation the sample can tolerate, not merely whether the electronics look more stable afterward.

**Level and time:** upper-division undergraduate; 5–7 hours. **Prerequisites:** [sampling and fluidics](07-sampling-and-fluidics.md), gas mixtures, elementary phase equilibrium, and [ionic liquids and materials](05-ionic-liquids-and-materials.md).

<a id="section-learning-outcomes"></a>

## Learning outcomes

- Convert among water partial pressure, relative humidity, and mole fraction.
- Determine whether a proposed temperature change risks condensation.
- Distinguish particle filtration, gas adsorption, water removal, and dilution.
- Design recovery and blank tests for a conditioning stage.
- Identify confounding when humidity correlates with the target label.

<a id="section-1-relative-humidity-is-not-water-concentration"></a>

## 1. Relative humidity is not water concentration

Relative humidity, RH, compares actual water partial pressure with saturation vapor pressure at the same temperature:

```text
RH_fraction = p_water / p_sat(T)
y_water = p_water / P_total
```

The same amount of water vapor can have different RH values at different temperatures. The same RH can correspond to different water concentrations. Consequently, an RH value without temperature is insufficient for reconstructing gas composition. Water activity at an equilibrium surface may be related to RH under appropriate conditions, but the interior of an electrolyte can lag the surrounding gas and exhibit composition-dependent behavior.

The [NIST Chemistry WebBook water entry](https://webbook.nist.gov/cgi/cbook.cgi?ID=C7732185&Mask=4&Type=ANTOINE&Plot=on) gives vapor-pressure correlations and their temperature intervals. Use a correlation only in its stated range and match the pressure units; different Antoine coefficient sets do not all use the same units.

The dew point is the temperature at which the current water partial pressure equals the saturation vapor pressure. Cooling below that point creates a liquid phase if nucleation and surfaces permit. Once droplets form, the sample is no longer a simple gas mixture: soluble analytes can partition into the liquid, particles can be captured, and wetted surfaces acquire new memory effects.

<a id="section-2-worked-example-cooling-a-humid-gas"></a>

## 2. Worked example: cooling a humid gas

Consider a hypothetical inlet at `34 °C`, `90% RH`, and `101.3 kPa`. Use approximate saturation pressures `p_sat(34 °C) = 5.32 kPa` and `p_sat(22 °C) = 2.64 kPa`.

```text
p_water,in = 0.90 × 5.32 = 4.79 kPa
y_water,in = 4.79/101.3 = 0.0473 = 4.73%

If cooled to 22 °C without removing water:
RH_required = 4.79/2.64 = 1.81, or 181%
```

The hypothetical 181% is a warning that a single equilibrium gas phase cannot retain that water loading at 22 °C. At equilibrium near the same total pressure, the saturated outlet gas contains approximately `2.61%` water by mole. For an exact condensate mass balance, conserve dry-gas moles rather than subtracting two wet mole fractions as though total gas moles stayed constant.

On a basis of one mole of dry gas:

```text
n_water,in / n_dry = 0.0473/(1 - 0.0473) = 0.04965
n_water,out / n_dry = 0.0261/(1 - 0.0261) = 0.02680
condensed water ≈ 0.02285 mol per mol dry gas
```

The result establishes a condensation risk; it does not predict where droplets appear, how fast they grow, or how an analyte partitions into them. Those require heat-transfer, surface, and solubility information. In particular, a sensor inside a housing may be colder than the temperature probe installed at the inlet.

<a id="section-3-how-water-changes-an-electrochemical-measurement"></a>

## 3. How water changes an electrochemical measurement

Several mechanisms can occur together:

- Water uptake changes electrolyte composition, viscosity, conductivity, and diffusion.
- Interfacial adsorption changes capacitance and the apparent impedance spectrum.
- Water participates in chemical or electrochemical reactions for some material systems.
- Condensation changes active area, contacts, and local transport.
- Humidity changes gas partitioning into the sensing film and surrounding polymers.

These mechanisms predict different time scales and signatures. An immediate resistance change followed by a slow baseline drift suggests more than one process. Measuring only RH at the inlet cannot identify which one dominates. Pair environmental data with electrical observables and repeat controlled changes in both directions.

Avoid a universal correction such as “subtract `a × RH`.” A more defensible local model is:

```text
response = b + s_c c + s_h h + s_ch c h + error
```

Here `h` is a clearly defined humidity variable, ideally with temperature and pressure recorded. The interaction term means humidity changes the analyte sensitivity itself. Calibrating humidity at zero analyte and then applying the correction everywhere misses that interaction.

<a id="section-4-filtration-and-drying-solve-different-problems"></a>

## 4. Filtration and drying solve different problems

A particulate filter separates particles according to mechanisms such as interception, diffusion, and impaction. It is not generally a molecular sieve for all VOCs. Conversely, an adsorbent that removes certain vapors may have little value for removing fine particles. A droplet can carry dissolved compounds; removing the droplet changes the sampled chemical inventory even when the filter passes the corresponding vapor.

A specification should therefore distinguish gas-phase concentration, particle-associated material, and total material. If the measurand is gas-phase analyte, the filter must preserve gas recovery while reducing particles. If the intended measurand includes particle-associated material, removing particles changes the question being answered.

Humidity treatment can involve several strategies:

| Strategy | Useful effect | Main question to test |
| --- | --- | --- |
| Temperature control | Avoids cold spots or stabilizes RH | Does heating change partitioning or chemistry? |
| Membrane drying | Transfers water across a membrane | Which target compounds also transfer? |
| Desiccant stage | Takes up water | Is uptake capacity stable, and are analytes retained? |
| Cooling/condensation | Removes water as liquid | Which compounds dissolve in condensate? |
| Dry-gas dilution | Reduces water and analyte concentrations | Is the dilution ratio measured accurately? |
| Computational compensation | Retains the original sample path | Is the model valid across environmental conditions? |

The original comparison by [Sang-Woo Lee and colleagues](https://doi.org/10.3390/chemosensors11030188) found that VOC recovery depended on both the moisture-removal device and the compounds tested. Its results justify testing analyte recovery; they do not establish a universally best dryer for every sensor, concentration, or mixture.

<a id="section-5-worked-example-dilution-and-a-misleading-recovery-value"></a>

## 5. Worked example: dilution and a misleading recovery value

A humid sample flows at `60 mL/min` and mixes with `140 mL/min` of nominally analyte-free dry gas, with both flows expressed at the same conditions. The sample fraction is:

```text
f = Q_sample / (Q_sample + Q_dry) = 60/200 = 0.30
c_mixed = f c_sample
```

An original `200 ppb` analyte becomes `60 ppb` before any wall loss. If a downstream measurement gives `54 ppb`, the conditioning train's recovery relative to the expected diluted concentration is `54/60 = 90%`. Dividing by the undiluted `200 ppb` gives `27%`, which confounds intentional dilution and unintentional loss.

Now suppose both flow meters have independent relative standard uncertainties of `2%`. Propagate the uncertainty in `f = Q_s/(Q_s + Q_d)`:

```text
u(f)^2 = [Q_d/(Q_s+Q_d)^2]^2 u(Q_s)^2
       + [Q_s/(Q_s+Q_d)^2]^2 u(Q_d)^2

u(Q_s) = 1.2 mL/min
u(Q_d) = 2.8 mL/min
u(f) = 0.00594
u(f)/f = 1.98%
```

This is already a meaningful uncertainty before accounting for reference concentration, mixing completeness, or detector calibration. Flow correlations can change the result; shared calibration errors should not be treated as independent merely because two meters are present.

<a id="section-6-recovery-blanks-capacity-and-history"></a>

## 6. Recovery, blanks, capacity, and history

Define recovery against an independent reference and a stated basis:

```text
recovery_j = measured amount of species j after stage
             / expected amount entering stage
```

For continuous flow, compare molar flux or correctly corrected concentration. For a stored sample, account for volume changes. A recovery greater than 100% can indicate desorption of a previous sample, background contamination, calibration bias, or uncertainty; it is not necessarily a beneficial concentration effect.

A useful conditioning study includes a blank before exposure, several input levels, repeated blanks afterward, and a humidity sequence in both increasing and decreasing directions. Include the age or cumulative exposure of a consumable stage. A desiccant that works when new can fail gradually as its capacity is consumed. A filter can change pressure drop as it loads, altering the sampling flow and time response.

The [EPA TO-15A method collection](https://www.epa.gov/amtic/compendium-methods-determination-toxic-organic-compounds-ambient-air) is useful for studying how an established analytical workflow treats cleanliness, moisture, and validation together. Its acceptance criteria belong to its specified analytical method; do not copy them into another instrument without an intended-use justification.

Storage research also shows that water can change during the waiting period. [Beauchamp et al.](https://doi.org/10.1088/1752-7155/2/4/046001) measured both VOC and humidity changes in sampling bags. A humidity reading obtained only when a bag is filled may therefore fail to describe the sample reaching the detector later.

<a id="section-7-environmental-confounding-can-imitate-selectivity"></a>

## 7. Environmental confounding can imitate selectivity

Imagine every positive-class sample is warm and humid, while every control is cool and dry. A classifier can achieve high apparent accuracy by recognizing water or temperature. That result does not establish recognition of the intended analyte. If the same environmental arrangement persists during random cross-validation, the error can survive sophisticated modeling.

Build a factorial design: multiple target concentrations crossed with multiple humidities, temperatures, and realistic interferents. Use independent preparation days and randomized measurement order. Include environmental-only baselines. If RH alone performs as well as the full sensor array, investigate the experimental design before celebrating the model.

For a computational activity, generate data from the interaction model in Section 3. Train one regression with only concentration and humidity, and another with their interaction. Test both at humidity values held out from training. Interpret the result as a model-adequacy demonstration, not evidence that the synthetic coefficients describe a real material.

<a id="section-8-research-reading-and-evidence-discipline"></a>

## 8. Research reading and evidence discipline

Read the moisture-pretreatment paper as a comparison under specified test conditions. Identify the measurement method, tested compounds, recovery definition, and flow conditions before quoting any percentage. Then propose one experiment that could reverse the ranking of the devices, such as changing analyte polarity or the measurement time scale. This is a productive way to engage with state-of-the-art apparatus work: understand the boundary of demonstrated performance.

The [ERS technical standard](https://doi.org/10.1183/13993003.00965-2016) offers additional context for breath collection and pretreatment. Use it to identify reporting variables, while recognizing that chemistry-specific recovery still requires measurement. Neither a named filter grade nor a familiar dryer brand substitutes for validation of the actual sample path.

<a id="section-design-decision-carried-forward"></a>

## Design decision carried forward

In the [design studio](../design-studio.md), choose whether the student project retains, controls, dilutes, or removes water, and whether particulate filtration is needed for its stated measurand. Compare an unconditioned path with a proposed conditioning path using the same hypothetical sample composition. The deliverable is a water balance, a condensation-risk calculation, a component-order diagram, and an analyte-recovery validation matrix. Specify capacity and pressure-drop changes over component life. Required evidence includes independent downstream analyte measurement, humidity and temperature at relevant locations, and blanks before and after exposure. Reject a conditioning choice if it improves electrical stability while destroying the information needed for the intended measurement. Pass the resulting flow, humidity, and recovery constraints to the storage and calibration stages.

<a id="section-9-exercises-and-worked-answers"></a>

## 9. Exercises and worked answers

1. **RH versus concentration.** At `25 °C`, take `p_sat = 3.17 kPa`. What is the water mole fraction at `50% RH` and `101.3 kPa`? **Answer:** `0.5 × 3.17/101.3 = 0.0156`, or approximately 1.56%.
2. **Wet and dry basis.** A wet mixture contains 100 ppb target and 4% water by mole. What is its dry-basis target fraction, assuming only water is removed? **Answer:** `100/(1 - 0.04) = 104.2 ppb`. This conversion does not account for target losses to a real dryer.
3. **Capacity.** A hypothetical stage retains `0.30 g` of water before its specified endpoint and receives `0.010 g/min`. Estimate its ideal capacity time. **Answer:** 30 min. Real breakthrough is distributed and depends on kinetics and operating conditions; 30 min is not a validated replacement interval.
4. **Interference.** A filter reduces the sensor signal by 20%, but an independent gas reference is unchanged. **Answer:** possibilities include removal of aerosols, altered humidity or flow, filter-generated interference, and detector baseline changes. The observation alone does not establish target loss.
5. **Design critique.** “The dried samples classify better, so drying improves chemical selectivity.” **Answer:** improved classification may result from lower noise or altered confounding. Establish recovery and independently vary humidity and analyte before making the selectivity inference.

<!-- course-footer:start -->
---

[Previous: 07 · Sampling and fluidics](07-sampling-and-fluidics.md) · [All modules](index.md) · [Next: 09 · Sample storage and modularity](09-sample-storage-and-modularity.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
