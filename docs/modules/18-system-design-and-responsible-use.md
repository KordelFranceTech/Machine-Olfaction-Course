---
layout: default
title: '18. Complete system design and responsible use'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [**Modules**](index.md) · [Labs](../labs/index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Modules](index.md) / 18. Complete system design and responsible use

**Module 18 of 18**

<!-- course-navigation:end -->

# 18. Complete system design and responsible use

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Learning outcomes](#section-learning-outcomes)
- [Start with the decision the instrument supports](#section-start-with-the-decision-the-instrument-supports)
- [Derive the architecture from the measurement requirement](#section-derive-the-architecture-from-the-measurement-requirement)
- [Select the interface and readout together](#section-select-the-interface-and-readout-together)
- [Allocate system budgets](#section-allocate-system-budgets)
- [Treat alerts as decisions with consequences](#section-treat-alerts-as-decisions-with-consequences)
- [Verification follows interfaces and failure paths](#section-verification-follows-interfaces-and-failure-paths)
- [Privacy, security, and the smallest useful dataset](#section-privacy-security-and-the-smallest-useful-dataset)
- [Manufacturing, maintenance, and sustainability](#section-manufacturing-maintenance-and-sustainability)
- [Two capstone routes](#section-two-capstone-routes)
- [Design decision carried forward](#section-design-decision-carried-forward)
- [Problems and worked answers](#section-problems-and-worked-answers)

</details>
<!-- course-toc:end -->

A measurement system is complete when its selected physical or computational input, acquisition, interpretation, and user decision fit together. The goal of this module is to derive that architecture from requirements and turn every important assumption into a verification task. The result is an engineering design package, not a claim that an unbuilt device already performs as intended.

**Prerequisites:** all core modules. **Suggested effort:** 3 hours of study and a multiweek design project.

<a id="section-learning-outcomes"></a>

## Learning outcomes

- Translate an intended use into measurable requirements and interfaces.
- Assemble a coherent architecture from sampling through alerts.
- Budget uncertainty, delay, energy, and sample losses across the system.
- Distinguish a chemical result, an invalid measurement, and an unsupported inference.
- Produce a reviewable design with verification evidence, limitations, and a maintenance plan.

<a id="section-start-with-the-decision-the-instrument-supports"></a>

## Start with the decision the instrument supports

Specify who uses the instrument, what sample it receives, what output is needed, and what action follows. “Measure a reproducible electrical response to a controlled reference sample” is a valid educational goal. “Diagnose a disease” requires a much larger clinical evidence program. The latter is not achieved by assembling a working electrochemical circuit.

Write requirements so that another team can determine whether they were met. “Fast” becomes a maximum time from sample arrival at the inlet to a valid result under stated conditions. “Selective” becomes an interference challenge with concentration ratios, environmental bounds, and acceptance criteria. “Portable” becomes mass, dimensions, runtime, and handling requirements.

NASA's systems-engineering handbook provides an official framework for connecting requirements, design, verification, and validation. Adapt the discipline to the scale of a student project rather than copying aerospace process overhead. [NASA Systems Engineering Handbook](https://www.nasa.gov/reference/systems-engineering-handbook/)

<a id="section-derive-the-architecture-from-the-measurement-requirement"></a>

## Derive the architecture from the measurement requirement

```text
known reference, documented transducer, or synthetic input
  -> a defined measurement boundary
  -> acquisition with units, timing, and quality flags
  -> calibration and uncertainty evaluation
  -> a result within scope, an indeterminate result, or a fault

Project-dependent support: power, data provenance, maintenance,
user interface, and any independently justified sample handling
```

Choose a public educational platform, a passive electrical teaching circuit, or an authorized commercial measurement module as the starting point. Describe the actual interfaces and operating limits of that choice. A software-only contribution can use a fully specified synthetic input instead.

Sampling and materials studies elsewhere in the course provide tools for evaluating particular projects. They are separate trade studies, not mandatory components of one prescribed instrument. For example, a transport simulation can investigate residence-time bias without specifying hardware, while a dummy-cell instrument can establish readout accuracy without chemical sampling.

Treat portability and interchangeability as optional requirements. If either is necessary, explain the additional uncertainty, service, and validation burden using the selected platform's public documentation. Where components are exchanged, verify their identity and applicable calibration before interpreting a measurement.

<a id="section-select-the-interface-and-readout-together"></a>

## Select the interface and readout together

Choose materials by the required chemical interactions, transport, stability, and manufacturability. An electrolyte's conductivity alone does not establish selectivity. A material that produces a large response but fails to recover may be suited to cumulative exposure rather than repeated independent samples. State whether the intended signal is Faradaic current, potential, impedance, or another validated observable.

Excitation and readout must fit the electrochemical model. A current measurement needs an appropriate front end and dynamic range. Impedance requires stable small-signal acquisition over a justified frequency range. A reference electrode must be treated as a physical component with limitations, not an ideal software constant. Use published, independently justified operating principles; do not substitute unexplained settings for a design rationale.

Arrays should allocate channels to distinct needs: repeated channels for precision and fault checks, diverse responses for discrimination, and environmental or blank references for nuisance monitoring. The choice should be supported by conditioning and covariance analysis from [Module 13](13-arrays-and-selectivity.md).

<a id="section-allocate-system-budgets"></a>

## Allocate system budgets

### Worked example: energy is usually a system property

Consider a synthetic design with the following average electrical loads:

| Function | Power |
| --- | ---: |
| Sensor interface and analog readout | 12 mW |
| Processor and local storage | 18 mW |
| Environmental measurements | 3 mW |
| Communication, duty-cycle average | 7 mW |
| Sample-flow actuator, duty-cycle average | 160 mW |
| Total | 200 mW |

A battery with nominal energy 3.7 Wh and usable fraction 0.8 provides 2.96 Wh. Idealized runtime is `2.96/0.200 = 14.8 h`, before additional temperature, aging, peak-current, and conversion effects not included in the usable fraction. Reducing the analog readout by half saves only 6 mW, about 3% of total power. Improving sample-flow duty cycle may matter more, provided it does not compromise measurement quality.

### Worked example: end-to-end uncertainty and delay

Suppose independent relative standard uncertainties are 3% from reference concentration, 4% from sample transfer, 5% from electrical calibration, and 6% from environmental correction. The combined relative standard uncertainty is:

```text
u_rel = sqrt(0.03^2 + 0.04^2 + 0.05^2 + 0.06^2)
      = 0.0927, or 9.27%
```

This is not a complete uncertainty budget if systematic model discrepancy or covariance is omitted. If the same temperature estimate affects both sample transfer and correction, independence may be false.

For timing, suppose transport requires 1.5 s, the sensing stage needs 4 s to reach the decision criterion, processing requires 0.1 s, and communication adds up to 0.4 s. A conservative serial budget is 6.0 s. Some stages overlap, but credit for overlap requires a defined timeline and evidence. The sample interval alone does not describe result latency.

<a id="section-treat-alerts-as-decisions-with-consequences"></a>

## Treat alerts as decisions with consequences

A robust state machine can distinguish warming up, ready, acquiring, evaluating, valid result, indeterminate, and fault. A stale value should not remain on screen as though it were a new measurement. A failed reference check should not produce a “negative” chemical result.

Thresholds require a defined decision problem. Consider false positives, false negatives, abstentions, persistence, hysteresis, and the action expected of the user. Majority voting cannot eliminate common-cause interference. A machine-learning probability is not a safety assurance.

For learned components, NIST's AI Risk Management Framework offers a voluntary structure for organizing risks and evidence throughout the lifecycle. It supports disciplined assessment; it does not certify a sensor's accuracy or suitability. [NIST AI RMF](https://www.nist.gov/itl/ai-risk-management-framework)

<a id="section-verification-follows-interfaces-and-failure-paths"></a>

## Verification follows interfaces and failure paths

A requirement-to-test matrix connects each design choice to observable evidence. Tests should include normal operation and the conditions under which the system must refuse to interpret the sample.

| Requirement area | Example evidence | Failure to challenge |
| --- | --- | --- |
| Representative sampling | Transfer model and recovery measurements | Wall losses, leaks, dead volume, condensation |
| Conditioning | Before/after analyte recovery and humidity record | Filter or drying step removes useful signal |
| Storage and valves | Retention, leak, and pressure-flow characterization | Backflow, permeation, incomplete emptying |
| Electrochemical readout | Reference circuit and calibration checks | Saturation, reference drift, unstable excitation |
| Array interpretation | Mixture and interference tests across devices | Correlated drift, failed channel, unknown mixture |
| Processing | Synthetic known-answer tests and independent data | Leakage, noncausal delay, stale calibration |
| Result and alert | State-transition and usability scenarios | Invalid sample displayed as a valid negative |
| Portability | Runtime, handling, and thermal evidence | Battery sag, connector movement, enclosure heating |
| Maintenance | Replacement and update procedure | Wrong calibration or version after service |

Verification asks whether the implementation meets its specifications. Validation asks whether those specifications and resulting behavior satisfy the intended use. Passing a simulated current test verifies part of the electronics; it does not validate sample chemistry.

<a id="section-privacy-security-and-the-smallest-useful-dataset"></a>

## Privacy, security, and the smallest useful dataset

Chemical signals can reveal information about people, workplaces, or activities, even without a person's name attached. Decide what data are needed, where they are processed, who can access them, and when they are deleted. A local summary may satisfy the task without uploading raw traces and location histories.

NIST's Privacy Framework provides a structured way to consider privacy risks from data processing. For a teaching project, a concise data-flow map and retention policy can make those decisions explicit. [NIST Privacy Framework](https://www.nist.gov/privacy-framework)

Connected devices also need a security plan for identity, configuration, data protection, software updates, and status reporting. NIST IR 8259A describes a core baseline of IoT device cybersecurity capabilities. Select relevant controls based on the actual architecture and threat model. [NIST IR 8259A](https://csrc.nist.gov/pubs/ir/8259/a/final)

<a id="section-manufacturing-maintenance-and-sustainability"></a>

## Manufacturing, maintenance, and sustainability

A successful laboratory unit does not reveal the distribution of production units. Plan incoming checks, device-to-device calibration transfer, shelf storage, replacement intervals, and end-of-life handling. Separate consumable sample-contact components from reusable electronics when that improves hygiene, serviceability, or waste management, while accounting for the additional connector and calibration burden.

Maintenance needs a trigger: elapsed time, failed reference check, known exposure history, or uncertainty exceeding a limit. “Recalibrate when performance seems bad” is not a reproducible policy. Record changes to hardware, firmware, features, and models so that a result can be interpreted later.

<a id="section-two-capstone-routes"></a>

## Two capstone routes

**Documented teaching measurement system:** choose a passive circuit, a publicly documented educational platform, or an authorized commercial module. Specify its input/output contract, acquisition, calibration, quality states, and verification matrix. Include additional subsystems only when the chosen use case and independent public evidence justify them.

**Independent adjacent project:** choose a useful subsystem, analysis tool, or educational instrument from [derivative projects](../derivative-projects.md). Define its interfaces to a larger device, establish an independent design rationale, and test the improvement against a fair baseline. Read [responsible innovation](../responsible-innovation.md); changing a design does not by itself establish freedom to operate.

Both routes culminate in the [capstone studio](../labs/08-capstone-studio.md), with an evidence package rather than unsupported performance promises.

<a id="section-design-decision-carried-forward"></a>

## Design decision carried forward

**Choice:** freeze the proposed architecture and its supported output contract. **Criteria:** traceable requirements, coherent budgets, independent evidence, and manageable failure consequences. **Evidence:** calculations, computational tests, public-source rationale, and a plan for the physical validation still needed. **Artifact:** a design dossier containing the architecture, interface definitions, requirements matrix, uncertainty and timing budgets, data policy, maintenance plan, and clearly separated demonstrated and proposed capabilities.

<a id="section-problems-and-worked-answers"></a>

## Problems and worked answers

1. **Every subsystem passes:** Can the integrated instrument still fail? **Answer:** Yes. Interfaces, timing, sample losses, thermal coupling, and calibration mismatches can create system failures absent from isolated tests.
2. **Drying improves signal:** What must be checked before adopting it? **Answer:** Analyte recovery, mixture distortion, repeatability, humidity dependence, and effects on the interpretation model.
3. **Module replacement:** What metadata must stay linked? **Answer:** Device and module identity, calibration version, firmware/model version, installation time, and required reference checks.
4. **Low battery:** Should a compromised measurement become a negative result? **Answer:** No. The state machine should report an invalid or unavailable result when the measurement requirements are not met.
5. **Useful derivative:** What makes a subsystem contribution credible? **Answer:** A specific need, independent implementation, explicit interfaces, a fair baseline, reproducible evidence, and honest limits on what the test establishes.

<!-- course-footer:start -->
---

[Previous: 17. Research frontiers and how to read the evidence](17-research-frontiers.md) · [All modules](index.md) · [Next: Projects: choose, build, and verify](../projects/index.md)

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
