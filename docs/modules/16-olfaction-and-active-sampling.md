---
layout: default
title: '16. Biological olfaction, plumes, and active sampling'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [**Modules**](index.md) · [Labs](../labs/index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Modules](index.md) / 16. Biological olfaction, plumes, and active sampling

**Module 16 of 18**

<!-- course-navigation:end -->

# 16. Biological olfaction, plumes, and active sampling

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Learning outcomes](#section-learning-outcomes)
- [What biology contributes to engineering intuition](#section-what-biology-contributes-to-engineering-intuition)
- [Structure, function, and device performance are separate evidence layers](#section-structure-function-and-device-performance-are-separate-evidence-layers)
- [Recognition layers face an air-to-interface problem](#section-recognition-layers-face-an-air-to-interface-problem)
- [A plume is a moving, intermittent concentration field](#section-a-plume-is-a-moving-intermittent-concentration-field)
- [Time-of-arrival estimates have demanding assumptions](#section-time-of-arrival-estimates-have-demanding-assumptions)
- [Active sampling changes the information available](#section-active-sampling-changes-the-information-available)
- [Data and ground truth for localization research](#section-data-and-ground-truth-for-localization-research)
- [Design decision carried forward](#section-design-decision-carried-forward)
- [Problems and worked answers](#section-problems-and-worked-answers)

</details>
<!-- course-toc:end -->

Smelling is an active measurement process. The organism moves, draws air across a sensory surface, adapts to recent exposure, and combines chemical evidence with context. Engineering can borrow useful principles without assuming that a sensor array is equivalent to a nose or that one molecular measurement reveals an entire percept.

**Prerequisites:** transport, response dynamics, arrays, probability, and basic vectors. **Suggested effort:** 3 hours of study and 2 hours of simulation.

<a id="section-learning-outcomes"></a>

## Learning outcomes

- Distinguish molecular recognition, electrical transduction, neural coding, and perception.
- Explain why a biological receptor's structure does not establish a working gas sensor.
- Model an airborne signal as transport followed by a sensor response function.
- Identify when two-sensor time differences can and cannot estimate transport velocity.
- Design active sampling and localization experiments with independent ground truth.

<a id="section-what-biology-contributes-to-engineering-intuition"></a>

## What biology contributes to engineering intuition

A receptor does not generally act as a unique barcode reader for one odorant. Overlapping responses across receptors create a distributed code. Changing concentration can change which receptors respond strongly, so identity and concentration are not trivially separable. [Malnic et al., 1999](https://pubmed.ncbi.nlm.nih.gov/10089886/)

An engineering analogy is an array of microphones: each records a mixture of sources, and the pattern across microphones can help infer the scene. The analogy has limits. Chemical interfaces may react irreversibly, saturate, compete for binding, and recover slowly. Mixture responses can be nonlinear, making simple signal superposition unreliable.

Separate the stages:

```text
molecules in air
    -> transport to a hydrated sensory interface
    -> molecular interactions and receptor activation
    -> biochemical and electrical signals
    -> population-level processing
    -> behavioral or perceptual interpretation
```

Mammalian odorant receptors are G protein-coupled receptors. Insect receptor families include different architectures; do not describe every biological olfactory receptor as a mammalian-style GPCR. A biohybrid device must identify which biological component it uses and how recognition reaches an electrical output. [Sato et al., 2008](https://www.nature.com/articles/nature06850)

<a id="section-structure-function-and-device-performance-are-separate-evidence-layers"></a>

## Structure, function, and device performance are separate evidence layers

A receptor structure can reveal a binding environment and motivate hypotheses about interactions. Functional assays then test whether a ligand changes receptor signaling. Device experiments test whether the biological component survives immobilization, remains accessible, and generates a useful measurable response. These are linked but distinct achievements.

A 2023 study resolved the structural basis of recognition in a human odorant receptor. A 2024 study used engineered consensus receptors to obtain additional structural and functional information. These advances support mechanistic questions and design hypotheses; they do not establish lifetime, manufacturing yield, or field robustness for a future biohybrid sensor. [Billesbølle et al., 2023](https://pubmed.ncbi.nlm.nih.gov/36922591/), [de March et al., 2024](https://pubmed.ncbi.nlm.nih.gov/39478229/)

A computational structure prediction is still further removed from validated device behavior. It does not by itself determine ligand affinity, signaling efficacy, vapor delivery, immobilization orientation, or readout sensitivity. Ask which quantities were measured and which were inferred before converting structural insight into an engineering specification.

<a id="section-recognition-layers-face-an-air-to-interface-problem"></a>

## Recognition layers face an air-to-interface problem

An airborne molecule must reach the recognition layer, enter the local medium, and encounter an accessible site. Strong affinity cannot compensate for a sample path that removes the molecule. A layer that binds strongly may respond sensitively but regenerate poorly. A hydrated interface may preserve biological function while becoming highly sensitive to water loss and humidity changes.

For a simple reversible binding model:

```text
dtheta/dt = k_on*c*(1-theta) - k_off*theta

At equilibrium:
theta = c/(K_d + c)
K_d = k_off/k_on
```

`theta` is fractional occupancy, `c` is concentration in the medium at the binding site, `k_on` has reciprocal-concentration reciprocal-time units, and `k_off` has reciprocal-time units. This model assumes independent equivalent sites and one ligand class. Real receptors and mixtures can violate those assumptions.

### Worked example: affinity versus dynamic range

Use synthetic `K_d = 2 micromolar`. At `c = 0.2 micromolar`, occupancy is 0.091; at 2 micromolar it is 0.5; at 20 micromolar it is 0.909. Near saturation, large concentration changes produce small occupancy changes. A sensor with high affinity can therefore have a narrow useful range. If the electrical signal is not proportional to occupancy, a separate transduction model is needed.

The gas-phase concentration cannot be inserted into this equation without a partition or transport relationship. A statement such as “the receptor responds at a liquid concentration” is not automatically an airborne detection limit.

<a id="section-a-plume-is-a-moving-intermittent-concentration-field"></a>

## A plume is a moving, intermittent concentration field

Airflow transports molecules while turbulence stretches and mixes the plume. At a stationary point, concentration may alternate between brief encounters and long gaps. A single instantaneous concentration gradient need not point toward the source.

A simplified advection-diffusion equation is:

```text
partial c/partial t + u dot grad(c) = D*Laplacian(c) + q - k*c
```

Here `c` is amount concentration, `u` is velocity, `D` is a molecular or explicitly modeled effective diffusivity, `q` is a source term per volume per time, and `k` is a first-order loss rate. Using an effective diffusivity to represent turbulence is a model closure, not a universal material constant. Walls, obstacles, buoyancy, changing wind, and source intermittency complicate the field.

A sensor observes this field only after its own response dynamics:

```text
y_i(t) = integral from s=0 to infinity of
         [h_i(s)*c(x_i(t-s), t-s) ds] + b_i(t) + noise_i(t)
```

The response kernel `h_i` represents the combined sampling and sensing process when a linear approximation is reasonable. Motion, spatial averaging, nonlinear chemistry, and saturation may require a richer model. Even this simple expression shows why a delayed reading belongs to a past exposure history, not necessarily the sensor's current location.

<a id="section-time-of-arrival-estimates-have-demanding-assumptions"></a>

## Time-of-arrival estimates have demanding assumptions

For a feature moving unchanged along the line between two fixed sensors, separation `d` and arrival difference `Delta_t` give `u_parallel = d/Delta_t`. This estimates transport along that baseline, not automatically the source direction or distance. The feature must remain recognizable, clocks must be synchronized, and channel dynamics must be comparable.

### Worked example: sensor lag looks like slower airflow

Let two sensors be separated by 0.10 m along a uniform flow of 0.20 m/s. The ideal transport lag is 0.50 s. Suppose their first-order time constants are 2 s and 5 s. For identical step exposures, the 50% crossing delay of each sensor is `tau*ln(2)`.

```text
observed threshold lag
  = transport lag + (tau_2 - tau_1)*ln(2)
  = 0.50 + 3*0.6931
  = 2.579 s

naive inferred speed = 0.10/2.579 = 0.0388 m/s
```

The naive estimate is wrong by more than a factor of five, although the electronics could timestamp every sample perfectly. Swapping the slow and fast sensors can even reverse the sign of the apparent lag. Calibration of sensor dynamics is essential, and uncertainty in that calibration must enter the velocity estimate.

For `u = d/Delta_t`, independent small uncertainties give:

```text
(u_u/u)^2 approximately equals (u_d/d)^2 + (u_Delta_t/Delta_t)^2
```

With `d = 0.10 +/- 0.005 m` and `Delta_t = 0.50 +/- 0.10 s` as standard uncertainties, relative uncertainty is approximately 20.6%. This ignores systematic response mismatch and plume deformation, which can dominate.

Cross-correlation can estimate a lag from whole traces, but a correlation peak is not proof of shared transport. Common electrical noise, humidity changes, and synchronized sampling artifacts also correlate signals. Validate lag estimators with independent flow measurements and known signal delivery before interpreting them spatially.

<a id="section-active-sampling-changes-the-information-available"></a>

## Active sampling changes the information available

Active sampling can mean controlling flow, changing sample presentation, repositioning the sensor, or choosing when to collect another measurement. Each action trades information against time, power, and disturbance of the scene. Drawing air faster can shorten transport delay while changing residence time or drying a sensitive interface.

An active controller should know its goal. Maximizing instantaneous response may favor moving into a locally concentrated filament, while minimizing uncertainty about source location may favor another direction. Vergassola, Villermaux, and Shraiman introduced infotaxis as a search strategy based on expected information gain under sparse cues. Its performance is conditional on the assumed detection and transport model. [Vergassola et al., 2007](https://www.nature.com/articles/nature05464)

For a discrete source-location belief `p_j`, uncertainty can be represented by Shannon entropy:

```text
H = -sum_j p_j*log2(p_j)     [bits]
expected information gain(action)
  = H_before - expected H_after_action
```

Two equally likely source locations have entropy 1 bit. If an ideal action always distinguishes them, expected posterior entropy is zero and the action gains 1 bit. Real sensors miss encounters and produce false positives, so the expected gain is smaller. A model that ignores missed detections may become confidently wrong after a quiet period.

<a id="section-data-and-ground-truth-for-localization-research"></a>

## Data and ground truth for localization research

A plume experiment should record sensor positions, pose uncertainty, wind measurements, timestamps, source operation, and independent concentration or delivery information where feasible. “The robot moved toward the source once” is an observation, not a general localization accuracy estimate. Vary source location, airflow, obstacles, background, and starting position.

Public flow-modulation data provide a useful route to studying temporal information without generating gases in class. The UCI dataset describes 58 time series from a 16-channel metal-oxide array under modulated flow. The transduction and experimental conditions remain specific to that dataset. [UCI, gas sensor array under flow modulation](https://www.archive.ics.uci.edu/dataset/308/gas+sensor+array+under+flow+modulation)

For a synthetic exercise, use a known transport lag and response kernels, then deliberately violate one assumption at a time. The [plume and timing lab](../labs/07-plume-and-timing.md) shows how response mismatch corrupts time differences. It establishes the behavior of the mathematical model, not the accuracy of a physical localization instrument.

<a id="section-design-decision-carried-forward"></a>

## Design decision carried forward

**Choice:** decide whether the device reports only a local sample result or attempts spatial inference. **Criteria:** response time, synchronization, motion uncertainty, available airflow information, and validation cost. **Evidence:** controlled timing tests and independent spatial trials. **Artifact:** a timing budget separating transport, sensor, filter, processing, and communication delays, plus a statement of which spatial conclusions are supported. Add this to the [design studio](../design-studio.md).

<a id="section-problems-and-worked-answers"></a>

## Problems and worked answers

1. **Predicted receptor structure:** What device properties remain unknown? **Answer:** Binding and signaling behavior, sample access, immobilization effects, electrical coupling, selectivity, stability, and calibration transfer.
2. **Persistent binding:** Why can strong binding hurt a reusable sensor? **Answer:** Slow dissociation can increase carryover and recovery time, reducing independent sample throughput.
3. **Two sensors:** Does one measured lag determine a two-dimensional source location? **Answer:** No. It provides at most a constrained transport observation under assumptions; source inversion needs more information.
4. **No detection:** Is silence evidence that no source exists? **Answer:** Only probabilistically and under a validated detection model. Intermittent plumes can create long gaps.
5. **Moving instrument:** Where should a delayed reading be placed on a map? **Answer:** Use a stated observation model and pose history, with uncertainty. Assigning it to the latest position without accounting for lag can smear or displace the inferred plume.

<!-- course-footer:start -->
---

[Previous: 15. Machine learning, uncertainty, and domain shift](15-machine-learning-and-domain-shift.md) · [All modules](index.md) · [Next: 17. Research frontiers and how to read the evidence](17-research-frontiers.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
