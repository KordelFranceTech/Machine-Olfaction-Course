---
layout: default
title: 'Design studio: derive an integrated sensing system'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](index.md) · [Start](getting-started.md) · [Modules](modules/index.md) · [Labs](labs/index.md) · [**Projects**](projects/index.md) · [Library](references/index.md) · [Site map](navigation.md)

[Course home](index.md) / [Projects](projects/index.md) / Design studio: derive an integrated sensing system

<!-- course-navigation:end -->

# Design studio: derive an integrated sensing system

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Begin with an application, not a component](#section-begin-with-an-application-not-a-component)
- [How the architecture emerges](#section-how-the-architecture-emerges)
- [Twelve design questions](#section-twelve-design-questions)
  - [1. Define the measurement contract](#section-1-define-the-measurement-contract)
  - [2. Choose a defensible interfacial mechanism](#section-2-choose-a-defensible-interfacial-mechanism)
  - [3. Close the molecular mass balance](#section-3-close-the-molecular-mass-balance)
  - [4. Choose the electrical experiment](#section-4-choose-the-electrical-experiment)
  - [5. Evaluate sample transport when relevant](#section-5-evaluate-sample-transport-when-relevant)
  - [6. Audit storage as an optional case study](#section-6-audit-storage-as-an-optional-case-study)
  - [7. Design the measurement electronics](#section-7-design-the-measurement-electronics)
  - [8. Decide how much array diversity is needed](#section-8-decide-how-much-array-diversity-is-needed)
  - [9. Construct a calibration and validation strategy](#section-9-construct-a-calibration-and-validation-strategy)
  - [10. Evaluate practical constraints](#section-10-evaluate-practical-constraints)
  - [11. Design decisions and alarms](#section-11-design-decisions-and-alarms)
  - [12. Defend and revise the whole system](#section-12-defend-and-revise-the-whole-system)
- [Example requirements-to-test matrix](#section-example-requirements-to-test-matrix)
- [What counts as completion?](#section-what-counts-as-completion)

</details>
<!-- course-toc:end -->

A student who completes this course should be able to start with a measurement problem and derive a coherent device architecture. This studio makes that outcome explicit. It asks you to justify every block, define the interfaces between blocks, and propose measurements that could show the design is wrong.

The goal is a **design dossier and a staged, testable demonstrator**. Demonstrating electronics, molecular detection, mixture identification, and clinical usefulness are separate milestones. The course's mathematical examples are not specifications for a particular chemistry or commercial instrument.

<a id="section-begin-with-an-application-not-a-component"></a>

## Begin with an application, not a component

Choose an educational use case such as comparing known benign sample classes in an approved laboratory, studying environmental variation with an authorized commercial module, or investigating a simulated chemical measurement chain. For an independent adjacent project, use the [derivative track](derivative-projects.md). Define the decision a user would make from the result and the consequence of an invalid reading.

Write the problem as a testable statement:

> Within a stated sample matrix and environmental range, estimate or classify a defined quantity with a specified uncertainty, response time, and rejection rule, using a reproducible sampling and calibration procedure.

Avoid substituting “detect anything” for a measurand. A target list is not yet a specification: you need concentration range, interferents, mixtures, temperature, humidity, intended operators, and reference methods. If health interpretation is proposed, keep the chemical-measurement study separate from any population-level clinical question.

<a id="section-how-the-architecture-emerges"></a>

## How the architecture emerges

Choose a publicly documented teaching platform, a passive test circuit, an authorized commercial sensor, or an original computational model. Define what enters the project and what observations are actually available. Its architecture follows from that boundary rather than from a fixed feature list.

```text
known input or independently documented transducer
             -> acquisition and quality checks
             -> calibrated interpretation with uncertainty
             -> bounded result or explicit invalid state

Every interface records units, timing, assumptions, and provenance.
```

The scientific modules supply a toolbox: transport models can test a sampling assumption; electrochemical methods can distinguish responses; array theory can expose missing information; validation methods can challenge generalization. Select only the tools required by the project. A component that adds complexity without supporting the intended result should be omitted.

The twelve decisions below are a menu for a design dossier. Mark each applicable, optional, or out of scope. A dummy-cell instrument need not add gas handling; a transport simulator need not fabricate electrodes; a literature audit need not become a portable instrument.

<a id="section-twelve-design-questions"></a>

## Twelve design questions

<a id="section-1-define-the-measurement-contract"></a>

### 1. Define the measurement contract

Use Module 01 to distinguish gas-phase mole fraction, dissolved concentration, a response feature, and a class label. Choose one primary measurand and list the transformations between it and the electronics. Decide the concentration basis and reference conditions. Your artifact is a one-page measurement contract with units, range, and limits of intended use.

A good contract is specific enough that two laboratories could disagree quantitatively about whether it was met. “Fast,” “selective,” and “accurate” are aspirations until you define their tests.

<a id="section-2-choose-a-defensible-interfacial-mechanism"></a>

### 2. Choose a defensible interfacial mechanism

From Modules 02–05, propose how the target could change a measurable quantity. Separate redox current, adsorption, double-layer charging, bulk conductivity, and other plausible mechanisms. Identify which are hypotheses and which have independent supporting observations.

If a liquid medium is considered, compare phase state, ionic conductivity, viscosity, target partitioning, water uptake, electrode compatibility, and electrochemical stability. A materials table should contain both measured properties and missing data. Do not assign specificity from a chemical name, a simulation image, or an electrical response to one pure substance.

Your artifact is a mechanism diagram plus a falsification experiment. For example, a humidity-only control may challenge the interpretation of a conductivity change, while an orthogonal surface measurement may be needed to support a structural explanation.

<a id="section-3-close-the-molecular-mass-balance"></a>

### 3. Close the molecular mass balance

Use Module 03 and Lab 01 to estimate delivered amount, equilibrium uptake, and transport times. Put gas-side flow, interfacial transfer, diffusion through the sensing medium, and reaction in the same chain. Distinguish an upper bound on molecular supply from the actual fraction detected.

Your artifact is a transport budget. State which stage likely controls response and recovery. If no stage is known to dominate, design a perturbation study: vary flow, thickness, or electrode scale independently and compare the predicted scaling. Do not vary several coupled quantities and attribute the result to only one.

<a id="section-4-choose-the-electrical-experiment"></a>

### 4. Choose the electrical experiment

Use Module 06 to decide what current, potential, or impedance measurement can distinguish your hypotheses. Define the reference, bandwidth, observation duration, amplitude-selection logic, and conditions for a stationary small-signal interpretation. Select settings from independently characterized behavior, not from a desire to produce a visually striking curve.

Your artifact is a measurement protocol specification, including saturation checks, blanks, stability tests, and a rule for rejecting invalid fits. Numerical stimulus settings remain experimental design variables that require electrochemical qualification for the chosen materials.

<a id="section-5-evaluate-sample-transport-when-relevant"></a>

### 5. Evaluate sample transport when relevant

When sample transport is part of the selected project, use Modules 07–08 to calculate velocity, Reynolds number, residence time, pressure drop, and possible losses. Analyze an independently documented experiment or an explicitly synthetic geometry. Geometry alone does not establish chemical recovery or representative sampling.

Your artifact is a flow-path schematic with dimensions expressed as design variables, a volume budget, and a recovery test. Evaluate optional filtration and drying through paired upstream/downstream evidence. Treat water as both an interferent and a constituent affecting chemistry and sample concentration.

<a id="section-6-audit-storage-as-an-optional-case-study"></a>

### 6. Audit storage as an optional case study

Use Module 09 to evaluate a published storage study or a synthetic loss model when delayed analysis is relevant. Identify which observations distinguish contamination, retention, and changing sample composition. Keep the storage study independent of the core demonstrator unless its intended use requires integration.

Your artifact is an evidence table with conditions, holding times, recovery, blanks, uncertainty, and remaining questions. Explain what extra evidence would be needed before using the result in a different sampling procedure.

<a id="section-7-design-the-measurement-electronics"></a>

### 7. Design the measurement electronics

Use Module 10 to translate the expected signal range into analog gain, bandwidth, and digitization requirements. Estimate output swing, resistor noise, amplifier bias/current noise, offset, and reference stability. Include parasitic coupling from pumps, wireless communication, and power supplies.

Your artifact is a block diagram with signal levels and an uncertainty/noise allocation. First verify it with the electrical dummy-cell stage in the [build ladder](build-ladder.md). A channel must carry a timestamp and unit label, not just a numeric value.

<a id="section-8-decide-how-much-array-diversity-is-needed"></a>

### 8. Decide how much array diversity is needed

Use Module 13 to separate redundancy for repeatability from diversity for resolving targets and interferents. Write a local response matrix where appropriate. Check rank and sensitivity to perturbations; then identify where the linear approximation fails.

Your artifact is a channel-role table: primary target information, replication, reference/background information, or environmental context. A shared humidity error should appear explicitly in the covariance model. Adding channels is justified only if it improves the evidence needed for the intended inference.

<a id="section-9-construct-a-calibration-and-validation-strategy"></a>

### 9. Construct a calibration and validation strategy

Use Modules 11, 14, and 15 to define calibration levels, groups, environmental coverage, and independent validation. Fit preprocessing within training groups. Reserve entire devices, days, batches, or sites when those define the intended generalization challenge.

Your artifact is a partition diagram and calibration lifecycle. Include unknown mixtures and invalid samples. Decide how drift is detected and how a replaced module obtains an appropriate calibration. A model update must have a version and an independent acceptance evaluation.

<a id="section-10-evaluate-practical-constraints"></a>

### 10. Evaluate practical constraints

Derive power, space, handling, and maintenance requirements from the chosen use case. Consider a bench instrument and a portable implementation as alternatives when both are relevant. Use public documentation for any selected components and identify how their operating limits affect the project.

Your artifact is a constraint table and an interface-control document for the selected implementation. Interchangeability, when required, needs its own compatibility and calibration tests. It is not a default requirement for every project.

<a id="section-11-design-decisions-and-alarms"></a>

### 11. Design decisions and alarms

Use Modules 10, 12, and 18 to separate a valid positive result, a valid negative result, an unknown sample, an invalid measurement, and an instrument fault. Define persistence, hysteresis, and latching only after considering their effects on delay and false alarms. Specify which faults require user action and which allow a controlled retry.

Your artifact is a state-transition table with fault-injection tests. The system should never convert a sensor-disconnection fault into a confident negative result. A positive chemical indication must not silently become a medical diagnosis.

<a id="section-12-defend-and-revise-the-whole-system"></a>

### 12. Defend and revise the whole system

Use Module 17 to compare your approach with credible alternatives. Present the strongest reason your preferred design might fail. Then choose the smallest decisive experiment that would reduce that uncertainty.

Your artifact is the final dossier: problem statement, public scientific basis, architecture, interfaces, calculations, calibration plan, source provenance, verification matrix, and limitations. Include an independently developed alternative architecture using the same underlying physical insight.

<a id="section-example-requirements-to-test-matrix"></a>

## Example requirements-to-test matrix

The requirements below are an optional menu. Select applicable rows, omit unrelated functions, and choose quantitative limits justified by the project. The rows do not prescribe a combined device architecture.

| Requirement | Design consequence | Verification evidence |
| --- | --- | --- |
| Representative sample at the sensing region | Minimize and characterize losses | Paired reference measurements through complete sample path |
| Response within an application-defined time | Allocate transport, sensing, filtering, and decision delay | Measured step/pulse responses plus timestamp audit |
| Quantitation over a stated range | Suitable chemistry, gain, reference, and calibration | Independent samples across range and nuisance conditions |
| Distinguish target from an interference panel | Mechanistic selectivity or informative array | Mixture study with held-out groups |
| Stable behavior after module exchange | Defined interfaces and calibration association | Blind module-swap challenge with independent check standards |
| Detect invalid measurement | Quality metrics and explicit state handling | Disconnection, saturation, flow, and drift fault injection |
| Preserve stored sample within a specified tolerance | Appropriate materials, seals, and time limit | Time-dependent recovery and contamination study |
| Portable operating duration | Power allocation and duty-cycle strategy | Measured energy budget over realistic sequence |

<a id="section-what-counts-as-completion"></a>

## What counts as completion?

A complete course project has an executable model, a credible physical build plan, a clearly bounded demonstration, and a verification record. It states what has been tested and what remains a hypothesis. A fully assembled object without traceable calibration is incomplete; a high-scoring classifier without a sample-integrity model is incomplete; a materials result without an instrument-level error budget is incomplete.

For innovation beyond the core architecture, complete the [independent derivative track](derivative-projects.md) and [responsible-innovation worksheet](responsible-innovation.md). Technical differentiation and public provenance are necessary design disciplines; they do not establish legal clearance.

[Continue to the build ladder](build-ladder.md) · [Open the capstone lab](labs/08-capstone-studio.md)

<!-- course-footer:start -->
---

[Previous: Projects: choose, build, and verify](projects/index.md) · [Project routes](projects/index.md) · [Next: Integrated worked example: from a gas input to a valid reading](integrated-example.md)

[Back to top](#page-top) · [Site map](navigation.md) · [Course home](index.md)
<!-- course-footer:end -->
