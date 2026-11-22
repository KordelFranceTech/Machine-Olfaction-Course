---
layout: default
title: 'Curriculum map and learning pathways'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](index.md) · [Start](getting-started.md) · [Modules](modules/index.md) · [Labs](labs/index.md) · [Projects](projects/index.md) · [Library](references/index.md) · [Site map](navigation.md)

[Course home](index.md) / Curriculum map and learning pathways

<!-- course-navigation:end -->

# Curriculum map and learning pathways

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [The design outcome](#section-the-design-outcome)
- [Audience, preparation, and workload](#section-audience-preparation-and-workload)
- [Modules and their engineering questions](#section-modules-and-their-engineering-questions)
- [Competencies across the tree](#section-competencies-across-the-tree)
- [Sixteen-week semester](#section-sixteen-week-semester)
- [Shorter pathways](#section-shorter-pathways)
- [Assessment philosophy](#section-assessment-philosophy)

</details>
<!-- course-toc:end -->

This course treats a chemical sensing instrument as a sequence of transformations. A molecule is transported, partitions into a material, changes an interfacial process, produces an electrical response, and is interpreted in context. Every transformation can introduce ambiguity. Learning to locate and quantify that ambiguity is the central engineering skill.

<a id="section-the-design-outcome"></a>

## The design outcome

Maintain a cumulative [design-studio dossier](design-studio.md) while studying. The endpoint is a complete, justified measurement project and a staged demonstrator selected from public teaching platforms, documented commercial modules, or original computational models. Its required interfaces and tests follow from the chosen use case. The [integrated example](integrated-example.md) makes the subsystem interfaces executable. The [build ladder](build-ladder.md) connects computation to physical verification.

Then transfer the principles to one of [nine nearby projects](derivative-projects.md), or propose another equally concrete independent extension. Each project needs public provenance, acceptance tests, and the review record described in [responsible innovation](responsible-innovation.md). Architectural differences are engineering evidence, not legal clearance.

<a id="section-audience-preparation-and-workload"></a>

## Audience, preparation, and workload

The intended level is senior undergraduate or beginning graduate engineering. Useful preparation includes general chemistry, first-order differential equations, complex numbers, elementary circuit analysis, matrix algebra, and introductory probability. The [getting-started diagnostic](getting-started.md) identifies gaps without requiring all learners to repeat their strongest subjects.

Plan for **120–160 hours** for the full course, depending on programming experience and the depth of the capstone. This is a proposed teaching workload, not an accredited credit equivalence. Reading a module, reproducing its calculations, and answering its exercises usually requires 3–5 hours. Labs require another 2–4 hours each. Literature discussion and the capstone use the remaining time. Instructors can replace selected exercises with deeper experiments under institutionally approved arrangements.

<a id="section-modules-and-their-engineering-questions"></a>

## Modules and their engineering questions

| Module | Main question | Skills developed | Prerequisites |
| --- | --- | --- | --- |
| [01. Molecules and measurement](modules/01-molecules-and-measurement.md) | What exactly is being measured? | Concentration units, VOC terminology, measurand definition, dimensional analysis | General chemistry and algebra |
| [02. Thermodynamics and redox](modules/02-thermodynamics-and-redox.md) | What drives electron transfer? | Electrochemical potentials, equilibrium, kinetics, reference electrodes | 01; logarithms |
| [03. Transport and partitioning](modules/03-transport-and-partitioning.md) | How do molecules reach the active region? | Diffusion, convection, partition coefficients, characteristic times | 01; differential equations |
| [04. Electrode interfaces](modules/04-electrode-interfaces.md) | Where does the electrical response originate? | Double layers, adsorption, Faradaic and capacitive processes | 02–03; basic circuits |
| [05. Ionic liquids and materials](modules/05-ionic-liquids-and-materials.md) | How does the sensing medium change performance? | Material-property tradeoffs, water effects, stability, evidence for structure | 02–04 |
| [06. Electrochemical methods](modules/06-electrochemical-methods.md) | Which experiment separates competing explanations? | Voltammetry, time-domain response, impedance, model identifiability | 02–05; complex numbers |
| [07. Sampling and fluidics](modules/07-sampling-and-fluidics.md) | Does the sample arriving at the sensor represent its source? | Flow scaling, residence time, tubing losses, pressure drop | 03 |
| [08. Humidity, filtration, and conditioning](modules/08-humidity-filtration-and-conditioning.md) | What changes when a sample is cleaned or dried? | Water balance, aerosol/gas distinction, recovery, conditioning controls | 03, 07 |
| [09. Storage and modularity](modules/09-sample-storage-and-modularity.md) | Can a sample and sensor module be moved without changing the result? | Sorption, permeation, seals, valves, compressibility, contamination controls | 07–08 |
| [10. Electronics and embedded systems](modules/10-electronics-and-embedded-systems.md) | Can the instrument resolve and correctly label the response? | Potentiostats, transimpedance gain, noise, ADCs, timestamps, fault handling | 04, 06; circuits |
| [11. Calibration and uncertainty](modules/11-calibration-and-uncertainty.md) | How close is the reported value to the defined measurand? | Calibration, blanks, limits of detection, propagation of uncertainty | 01, 06, 10; statistics |
| [12. Breath sensing and clinical evidence](modules/12-breath-sensing-and-clinical-evidence.md) | What evidence connects a chemical pattern to health? | Sampling confounders, independent cohorts, prevalence, clinical reporting | 07–11; conditional probability |
| [13. Arrays and selectivity](modules/13-arrays-and-selectivity.md) | What does an additional sensor actually add? | Redundancy, diversity, matrix rank, interference, common-mode effects | 04–06, 11; linear algebra |
| [14. Signal processing and features](modules/14-signal-processing-and-features.md) | Which transformations preserve the information needed? | Baselines, filtering, temporal and spectral features, uncertainty | 06, 10–11, 13 |
| [15. Machine learning and domain shift](modules/15-machine-learning-and-domain-shift.md) | Will the inference survive a new day, device, or population? | Grouped validation, drift, calibration transfer, unknown samples | 11, 13–14; basic ML |
| [16. Olfaction and active sampling](modules/16-olfaction-and-active-sampling.md) | What can biology and motion teach chemical instruments? | Combinatorial coding, dynamic plumes, timing, sensing actions | 03, 07, 13–15 |
| [17. Research frontiers](modules/17-research-frontiers.md) | Which advances solve a demonstrated system bottleneck? | Critical comparison of current research and technology families | Core modules |
| [18. System design and responsible use](modules/18-system-design-and-responsible-use.md) | What must be specified before a device is useful? | Requirements, lifecycle, alarms, failure modes, validation strategy | Core modules |

<a id="section-competencies-across-the-tree"></a>

## Competencies across the tree

Use this index to connect disciplines with demonstrable engineering skills. A student project selects the subsystems needed for its own stated purpose; the course does not prescribe one physical device layout.

| Competency | Teaching location | Evidence of learning |
| --- | --- | --- |
| Define and quantify a measurand | 01–02, 11 | Unit ledger, reference convention, and uncertainty statement |
| Explain an interfacial observation | 02–06 | Mechanism comparison with independent controls and explicit limitations |
| Model transport and sample integrity | 03, 07–09 | Conserved mass balance, timescale analysis, and recovery study |
| Design and check an electrical measurement | 06, 10 | Dummy-circuit response, gain/noise budget, and invalid-state tests |
| Extract information from multiple observations | 13–15 | Identifiability analysis, leakage-free validation, and uncertainty estimates |
| Evaluate evidence for an application | 11–12, 17 | Public-paper critique separating component results from intended-use evidence |
| Reason about dynamic sensing | 14, 16 | Causal timing analysis and independently specified simulation |
| Develop an independent engineering project | 18 and the design studio | Publicly documented architecture, interface contract, and requirements-to-test matrix |

<a id="section-sixteen-week-semester"></a>

## Sixteen-week semester

The course works well as two discussions and one computation/design session per week. Adjacent modules can be taught together when an institution has longer meetings.

| Week | Main study | Studio or assessment |
| --- | --- | --- |
| 1 | Diagnostic, 01 | Lab 01: units and the measurement chain |
| 2 | 02 | Derive a potential shift and critique a reference choice |
| 3 | 03 | Lab 02: transport and storage |
| 4 | 04–05 | Material evidence comparison |
| 5 | 06 | Lab 03: impedance and identifiability |
| 6 | 07 | Fluidics design review |
| 7 | 08–09 | Sampling failure analysis; capstone proposal |
| 8 | 10 | Electronics budget; midterm problems |
| 9 | 11 | Lab 04: calibration and uncertainty |
| 10 | 12 | Diagnostic evidence journal club |
| 11 | 13 | Lab 05: array diversity and correlation |
| 12 | 14–15 | Lab 06: drift and validation |
| 13 | 16 | Lab 07: plume timing |
| 14 | 17 | Research-frontier presentations |
| 15 | 18 | Lab 08: capstone studio and peer review |
| 16 | Integration | Capstone defense and final assessment |

<a id="section-shorter-pathways"></a>

## Shorter pathways

**Eight-week engineering bridge.** Pair 01–02, 03–04, 05–06, 07–09, 10–11, 13–15, 12/16/17, and 18. Complete labs 01, 03, 04, 06, and the capstone. This is an intensive route; it assumes students can independently review the omitted exercises.

**Materials-to-system seminar.** Use 02–06 as the core and assign 07–11 as the system audit. Each student brings one independently sourced materials paper and identifies an experiment missing between its result and a reliable instrument.

**Data-science bridge.** Study 01, 03, 06, 07, and 11 before 13–16. Require a physical explanation for each feature and every nuisance variable. Complete labs 02, 04, 05, and 06. A model score must always be accompanied by its partitioning rule and the population to which the score applies.

<a id="section-assessment-philosophy"></a>

## Assessment philosophy

Suggested weighting is 20% problem sets, 25% labs, 15% literature critique, 15% midterm, and 25% capstone. In an independent study, replace grades with the same rubric and record unresolved assumptions.

An excellent submission is reproducible, dimensionally consistent, honest about uncertainty, and specific about the next experiment. A numerical result without units or an unstated validation split is incomplete even when its final number looks plausible. See the [assessment guide](assessments/index.md) and [teaching guide](teaching-guide.md).

[Begin the prerequisite diagnostic](getting-started.md) · [Begin Module 01](modules/01-molecules-and-measurement.md)

<!-- course-footer:start -->
---

[Back to top](#page-top) · [Site map](navigation.md) · [Course home](index.md)
<!-- course-footer:end -->
