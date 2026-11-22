---
layout: default
title: 'Build ladder: from models to a physical demonstrator'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](index.md) · [Start](getting-started.md) · [Modules](modules/index.md) · [Labs](labs/index.md) · [**Projects**](projects/index.md) · [Library](references/index.md) · [Site map](navigation.md)

[Course home](index.md) / [Projects](projects/index.md) / Build ladder: from models to a physical demonstrator

<!-- course-navigation:end -->

# Build ladder: from models to a physical demonstrator

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Stage 1: an executable measurement model](#section-stage-1-an-executable-measurement-model)
- [Stage 2: an electrical dummy cell](#section-stage-2-an-electrical-dummy-cell)
- [Stage 3: software and fault handling around a known input](#section-stage-3-software-and-fault-handling-around-a-known-input)
- [Stage 4: a documented commercial or educational sensing element](#section-stage-4-a-documented-commercial-or-educational-sensing-element)
- [Stage 5: characterize the complete sampling path](#section-stage-5-characterize-the-complete-sampling-path)
- [Stage 6: an array and independent validation](#section-stage-6-an-array-and-independent-validation)
- [Stage 7: new materials research](#section-stage-7-new-materials-research)
- [The outcome of the ladder](#section-the-outcome-of-the-ladder)

</details>
<!-- course-toc:end -->

Build one evidence-producing layer at a time. The first three stages can establish substantial engineering competence without custom sensing chemistry. Later stages require the facilities, reference methods, and approvals appropriate to the chosen application. Each stage has an entry condition, an observable output, and a stopping rule.

<a id="section-stage-1-an-executable-measurement-model"></a>

## Stage 1: an executable measurement model

Complete labs 01–05, then run the [integrated worked example](integrated-example.md), which explicitly connects concentration, current, voltage, digitization, and calibrated output. Use its interface table to combine a sample-path response, an interfacial model, a readout model, and a calibration function. Do not directly combine quantities from different labs without defining their physical relationship and units. Keep ground-truth simulated concentration separate from the value available to the inference algorithm. Add disturbances for temperature, humidity, offset drift, and occasional invalid measurements.

**Build artifact:** a locally executable model copied from the Markdown lab blocks, with a parameter table and units.

**Acceptance:** reproduce at least one hand calculation per subsystem, preserve mass balance within the selected model, and show that intentional unit or timestamp errors are detected. Changing a model parameter should produce the scaling predicted by the equations.

**Stopping rule:** if the model needs undisclosed material constants to make a useful prediction, label them unknown and run sensitivity bounds. Do not fill missing properties with a claimed measured value.

<a id="section-stage-2-an-electrical-dummy-cell"></a>

## Stage 2: an electrical dummy cell

A passive resistor-capacitor network allows an instrument to be checked without making any statement about chemistry. One educational example is a series resistance followed by a parallel resistance and capacitor:

```text
terminal A ---- R_s ----+---- R_p ----+---- terminal B
                       |             |
                       +----- C -----+

Illustrative component targets:
R_s = 1 kΩ
R_p = 100 kΩ
C   = 1 µF
```

Use measured component values and tolerances in the prediction. Prefer a suitable nonpolar capacitor for small bidirectional test signals. Keep the excitation and wiring within the instrument manufacturer's ratings; the terminal diagram does not define a universal potentiostat electrode connection. A potentiostat's dummy-cell connection must follow its documented configuration.

For a small ideal voltage step of 10 mV across the two-terminal network, the steady current is `10 mV/(101 kΩ)≈99.0 nA`. The initially uncharged capacitor makes the initial current approach `10 mV/1 kΩ=10 µA` in the ideal model. The time constant under an ideal voltage source is `(R_s || R_p)*C≈0.990 ms`, not `R_p*C`. The impedance branch's characteristic frequency remains `1/(2*pi*R_p*C)≈1.59 Hz`. These different timescales illustrate that the imposed boundary condition matters.

**Build artifact:** passive network, connection diagram, measured component values, expected step and frequency responses, and a readout gain plan.

**Acceptance:** measured response agrees with the network prediction within a justified budget including component tolerance, instrument accuracy, parasitic capacitance, and bandwidth. Verify the instrument does not saturate during the fast transient even if its steady response is tiny.

**Stopping rule:** diagnose disagreement in electronics and wiring before connecting any chemical sensor. A good dummy-cell measurement verifies part of the instrument, not electrochemical specificity.

Public examples of open electrochemical instrumentation include [DStat, Dryden and Wheeler, 2015](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0140349) and [CheapStat, Rowe and colleagues, 2011](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0023783). Use their original documentation and current project licenses when studying a physical implementation. Historical article cost figures are not present-day purchasing estimates.

<a id="section-stage-3-software-and-fault-handling-around-a-known-input"></a>

## Stage 3: software and fault handling around a known input

Feed recorded or synthetic signals through the same data schema intended for real acquisition. At minimum preserve monotonic acquisition time, channel identifier, physical units, instrument range, operating-state label, environmental context, and validity status. Separate missing data from numeric zero.

A useful state model is:

```text
STARTUP -> SELF_CHECK -> READY -> ACQUIRING -> QUALITY_CHECK
QUALITY_CHECK -> VALID_RESULT or UNKNOWN or INVALID
any state -> FAULT when an unrecoverable instrument condition occurs
```

**Build artifact:** a replayable dataset and state-transition table, including recovery paths. No automated action should be attached to a model output unless that action has been explicitly specified and tested.

**Acceptance:** inject disconnections, clipping, stale timestamps, repeated sequence numbers, out-of-range environmental conditions, and absent module identity. Verify the correct state is emitted. Confirm that reprocessing the same data with the same model version reproduces the result.

**Stopping rule:** fix invalid-data handling before optimizing classification accuracy. Faults must not silently become confident negative measurements.

<a id="section-stage-4-a-documented-commercial-or-educational-sensing-element"></a>

## Stage 4: a documented commercial or educational sensing element

Select an authorized, publicly documented element appropriate to the teaching application. A current-output electrochemical module, an optical ambient-gas module, or a liquid conductivity cell can each support useful learning, but their transduction mechanisms differ. The [derivative-project guide](derivative-projects.md) offers alternatives.

Selection starts with requirements: physical quantity, range, supply, interface, response time, environmental limits, calibration requirements, and interpretation boundaries. A digital “air-quality index” should not be relabeled as a specific VOC concentration. A module's output range can exceed the range over which its accuracy is specified.

**Build artifact:** datasheet-derived interface specification, source and license record, environmental logging, and a calibration/check plan. Follow the supplier's handling and electrical instructions. Use an approved educational procedure and reference when quantitative gas exposures would otherwise be required.

**Acceptance:** establish repeatability, blanks or baseline behavior, environmental sensitivity, response delay, and independent comparison where a suitable reference exists. Report the observed domain and avoid extrapolating to untested compounds or mixtures.

**Stopping rule:** absence of a reference or safe controlled challenge limits the project to characterization of reported signals. It does not justify a concentration accuracy claim.

<a id="section-stage-5-characterize-the-complete-sampling-path"></a>

## Stage 5: characterize the complete sampling path

Connect the approved sensing arrangement to a testable inlet, flow path, and optional conditioning or storage. Keep each addition reversible during characterization. Measure the complete path as well as its individual elements; connector interactions and dead volumes can matter.

Use a factorial comparison on paper before experiments: direct path versus proposed path, blank versus approved reference challenge, immediate versus delayed measurement, and low versus high allowed humidity. Add conditions only when the existing test can distinguish the hypotheses.

**Build artifact:** flow schematic, pressure/volume budget, recovery matrix, carryover observations, and documented materials.

**Acceptance:** application-specific recovery and delay limits are met with uncertainty. Distinguish any apparent sensing improvement from sample concentration changes caused by drying or storage.

**Stopping rule:** characterize losses before compensating them in software. A learned correction may fail when conditions move outside the calibration domain.

<a id="section-stage-6-an-array-and-independent-validation"></a>

## Stage 6: an array and independent validation

Introduce extra channels only after specifying their role. Compare the multi-channel system with simple baselines. Hold out devices, acquisition days, or sample batches to match the intended use. Include unknown mixtures and abnormal sample states.

**Build artifact:** grouped data inventory, training and test partition, baseline model, calibrated uncertainty or rejection policy, and full error analysis.

**Acceptance:** improvement survives an independent evaluation with uncertainty intervals and a documented sample domain. The test set must not have guided preprocessing, feature selection, or threshold tuning.

**Stopping rule:** repeated tuning against the test set converts it into development data. Create a new independent evaluation before claiming final performance.

<a id="section-stage-7-new-materials-research"></a>

## Stage 7: new materials research

Custom interfaces require a separate scientific program: material characterization, electrochemical stability, response mechanism, controls, interferents, aging, and reproducibility across preparations. Begin with published procedures and appropriate institutional review. Do not infer a selective medium from an evocative structural drawing or a single favorable electrical trace.

**Build artifact:** a publicly grounded research proposal with an uncertainty-ranked experiment sequence. Maintain independent-development provenance and obtain appropriate IP review before advancing a commercial concept.

**Acceptance:** each proposed mechanism has discriminating controls and repeatable observations. A changed signal alone establishes neither molecular identity nor practical usefulness.

**Stopping rule:** unresolved mechanism, uncontrolled water content, or absent independent replication requires additional science before packaging or product claims.

<a id="section-the-outcome-of-the-ladder"></a>

## The outcome of the ladder

By finishing the relevant stages, students can specify, assemble, debug, and evaluate an instrument appropriate to their evidence and facilities. Their final dossier states which stages were completed physically, which were simulated, and which remain proposals. This distinction makes the work useful to the next engineer who builds on it.

[Return to the design studio](design-studio.md) · [Choose an independent project](derivative-projects.md)

<!-- course-footer:start -->
---

[Previous: Integrated worked example: from a gas input to a valid reading](integrated-example.md) · [Project routes](projects/index.md) · [Next: Nearby projects: useful engineering with distinct architectures](derivative-projects.md)

[Back to top](#page-top) · [Site map](navigation.md) · [Course home](index.md)
<!-- course-footer:end -->
