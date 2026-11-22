---
layout: default
title: 'Lab 08. Capstone design and evidence studio'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [Modules](../modules/index.md) · [**Labs**](index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Labs](index.md) / Lab 08. Capstone design and evidence studio

**Lab 08 of 8**

<!-- course-navigation:end -->

# Lab 08. Capstone design and evidence studio

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [The engineering challenge](#section-the-engineering-challenge)
- [Route A: a documented teaching measurement system](#section-route-a-a-documented-teaching-measurement-system)
- [Route B: an independent adjacent contribution](#section-route-b-an-independent-adjacent-contribution)
- [Milestones and decision gates](#section-milestones-and-decision-gates)
- [A requirement-to-test matrix to adapt](#section-a-requirement-to-test-matrix-to-adapt)
- [A small worked integration example](#section-a-small-worked-integration-example)
- [Dossier contents](#section-dossier-contents)
- [Review rubric](#section-review-rubric)

</details>
<!-- course-toc:end -->

**Time:** 3–5 weeks, adaptable to a shorter paper-design project. **Prerequisites:** the core curriculum and at least four computational labs. **Format:** a Markdown design dossier, a reproducible computational demonstration, and a design review. No hazardous analyte handling or human sample collection is part of this assignment.

<a id="section-the-engineering-challenge"></a>

## The engineering challenge

Develop a useful contribution to machine olfaction that another engineering team can understand, challenge, and extend. Every output must connect a physical or operational need to a design choice and an observable test. Unsupported performance language earns less credit than a carefully bounded result with an honest uncertainty analysis.

Choose one of two routes. Both require an independent rationale based on public science and a clearly defined scope. See [responsible innovation](../responsible-innovation.md) before choosing an implementation and [derivative project options](../derivative-projects.md) for additional ideas.

<a id="section-route-a-a-documented-teaching-measurement-system"></a>

## Route A: a documented teaching measurement system

Start from either a passive resistor-capacitor teaching circuit, an independently published educational measurement platform, or an authorized commercial sensor with public documentation. Cite the selected platform and distinguish its documented capabilities from your original extension. The project must define these interfaces:

1. **Known input:** identify the electrical standard, synthetic reference, or independently established measurement quantity and its uncertainty.
2. **Measurement boundary:** explain what the selected circuit or documented transducer measures, its valid operating range, and what remains outside its demonstrated capability.
3. **Acquisition:** justify gain, bandwidth, timing, digitization, and saturation checks from that boundary.
4. **Interpretation:** specify calibration, units, uncertainty, and how invalid or out-of-scope observations are handled.
5. **Verification:** compare prediction with known-answer tests and an independent reference where available. Record physical demonstrations separately from simulations.
6. **Original contribution:** identify one useful improvement, its fair baseline, and the evidence needed to assess it.

Additional sampling, storage, multi-channel, packaging, or serviceability work is optional. Include a subsystem only when the selected project requires it and an independent public source supports the implementation. A focused demonstration with trustworthy interfaces is a complete capstone. A design is not stronger merely because it includes more hardware.

The [integrated worked example](../integrated-example.md) provides an abstract unit-consistent signal chain. The [build ladder](../build-ladder.md) supplies staged checks for a physical educational demonstrator.

<a id="section-route-b-an-independent-adjacent-contribution"></a>

## Route B: an independent adjacent contribution

Choose a bounded project that improves an identifiable part of the workflow. Examples include a device-agnostic calibration-transfer tool, a sample-storage loss simulator, a causal timing-analysis library, a sensor-dataset audit, an uncertainty calculator, or a quality-control interface.

Define what enters and leaves the component, who benefits, and what baseline it improves. Connect it to a complete sensing architecture so that its assumptions are visible. A storage model must state its boundary conditions; an ML benchmark must state the unit of independence; a dashboard must distinguish valid negative results from invalid measurements.

Technical differences and independent implementation do not establish legal clearance. Record the public sources and design reasoning used, and keep any required legal or institutional review separate from the engineering evaluation.

<a id="section-milestones-and-decision-gates"></a>

## Milestones and decision gates

| Stage | Required artifact | Gate question |
| --- | --- | --- |
| 1. Intended use | One-page problem statement and operating envelope | Is the output meaningful and testable? |
| 2. Architecture | Block diagram, interface table, alternatives considered | Can sample, signal, energy, and data flows all be followed? |
| 3. Budgets | Mass balance, timing, uncertainty, and energy calculations | Do subsystem assumptions fit together? |
| 4. Evidence | Computational demonstration and source-backed rationale | What has been demonstrated, and what remains proposed? |
| 5. Verification | Requirement-to-test matrix and failure scenarios | Could the design be shown to be wrong? |
| 6. Review | Final dossier, limitations, maintenance and update plan | Can another team reproduce the reasoning? |

A gate can end with a redesign. Discovering that a reservoir loses the target before measurement is a useful engineering result if the evidence is clear and the architecture is revised.

<a id="section-a-requirement-to-test-matrix-to-adapt"></a>

## A requirement-to-test matrix to adapt

The following rows are an optional menu of assessment patterns, not a required collection of hardware features. Select only those relevant to the project, remove irrelevant rows, and add missing requirements. Numerical criteria are illustrative classroom targets, not demonstrated device specifications or universal design recommendations.

| ID | Proposed requirement | Test or analysis | Example acceptance criterion | Evidence status at project start |
| --- | --- | --- | --- | --- |
| R1 | Preserve a representative sample | Mass-balance and wall-loss model with sensitivity analysis | Predicted recovery above 90% over the chosen residence interval | Model only; physical recovery untested |
| R2 | Control sample transfer | Flow, pressure-drop, and dead-volume calculations | Flow and pressure remain within the chosen component limits | Calculation only |
| R3 | Prevent unnoticed storage failure | Leak, permeation, and valve failure scenarios | Every modeled leak exceeding the allowed budget produces a failed-quality state | Simulated fault logic |
| R4 | Read the electrical signal accurately | Known input/reference-circuit simulation | Gain error below 2% within the specified input range | Electronics model only |
| R5 | Separate target and nuisance effects | Synthetic factorial challenge and identifiability analysis | No required concentration direction is unidentifiable in the local model | Conditional mathematical result |
| R6 | Handle missing channels | Drop one channel at a time in evaluation | Report the changed uncertainty or abstain when requirements fail | Computational demonstration |
| R7 | Respect a timing contract | Causal end-to-end timeline and injected-delay tests | All reported latencies include transport and processing definitions | Model and software evidence |
| R8 | Support replacement | Module identity/calibration mismatch scenario | Wrong or missing calibration always blocks a valid chemical result | State-machine test |
| R9 | Avoid unsupported decisions | Unknown sample, saturation, stale data, and low-power scenarios | Each invalid case reaches an explicit invalid/indeterminate state | Software logic evidence |
| R10 | Fit the energy budget | Duty-cycle calculation with sensitivity bounds | Conservative usable energy supports the stated runtime | Calculation; battery testing pending |
| R11 | Generalize beyond development data | Grouped and chronological validation | Meet a predeclared metric and uncertainty target on independent groups | Requires appropriate dataset |
| R12 | Minimize unnecessary data | Data-flow and retention review | Every stored field has a purpose, access rule, and deletion rule | Design review |

Fault detection must use observables the proposed instrument actually has. A simulator may know the true leak rate, but the deployed algorithm cannot receive that hidden ground truth. Identify the pressure, flow, reference, or consistency measurement that makes each fault detectable; otherwise mark the fault as an unresolved limitation.

Use separate columns for predicted value, measured value, uncertainty, and pass/fail. Never fill a measurement column with a simulated number. If a target cannot yet be tested, specify the required equipment, reference, sample population, and confounders without claiming completion.

<a id="section-a-small-worked-integration-example"></a>

## A small worked integration example

Suppose a synthetic sample contains concentration `c_in`, and three transfer stages have modeled recoveries 0.95, 0.97, and 0.98. Overall recovery is `0.95*0.97*0.98 = 0.9031`. A designer who treats each “small” loss separately might overlook that nearly 10% of the initial signal is lost before transduction.

If uncertainty in recovery is appreciable, dividing by 0.9031 does not restore the original information perfectly. It also amplifies uncertainty. If recovery changes with analyte, humidity, or concentration, one universal correction factor is inadequate. The correct next step is to identify which stage dominates variability and design a discriminating test.

Now suppose the electrical response is within range but the sample's humidity exceeds the calibration envelope. A complete system returns an indeterminate result with the relevant reason. It does not silently extrapolate or report an absence. This is a system-level requirement even if every electronic component functions correctly.

<a id="section-dossier-contents"></a>

## Dossier contents

Organize the submission as linked Markdown pages or sections:

- Intended use, stakeholders, operating envelope, and unsupported uses.
- Architecture and sample/signal/data-flow diagrams.
- Decision records comparing at least two alternatives for each major design choice.
- Equations, units, assumptions, budgets, and sensitivity analyses.
- Reproducible code blocks with expected outputs and synthetic-data labels.
- Requirement-to-test matrix and current evidence status.
- Failure-mode table, quality states, and result/alert examples.
- Calibration, replacement, maintenance, and version-control policy.
- Annotated public references with precise support for key assertions.
- Remaining work, including which physical or clinical conclusions are still untested.

Use the [design studio](../design-studio.md) and [build ladder](../build-ladder.md) to assemble the artifacts produced throughout the course. The official [NASA systems-engineering handbook](https://www.nasa.gov/reference/systems-engineering-handbook/) is a useful reference for the distinction between requirements, verification, and validation.

<a id="section-review-rubric"></a>

## Review rubric

| Criterion | Weight | What strong work demonstrates |
| --- | ---: | --- |
| Physical reasoning and units | 20% | Consistent transport, electrochemical, electrical, and uncertainty models |
| Architectural integration | 20% | Interfaces and budgets connect all selected subsystems |
| Experimental and computational evidence | 25% | Reproducible tests, independent evaluation, and honest scope |
| Failure handling and responsible use | 15% | Invalid-state logic, privacy, maintenance, and bounded interpretation |
| Communication and source quality | 10% | Clear Markdown, inspectable calculations, primary references |
| Independent contribution | 10% | A useful question, justified alternatives, and a testable improvement |

A compelling presentation cannot compensate for hidden assumptions. A negative finding with a sound experiment can earn full credit. The strongest submission leaves the next engineering team knowing exactly what to build, what to measure, what might fail, and which conclusions they are entitled to draw.

<!-- course-footer:start -->
---

[Previous: Lab 07. Transport timing and sensor response mismatch](07-plume-and-timing.md) · [All labs](index.md) · [Next: Assessments and evaluation rubrics](../assessments/index.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
