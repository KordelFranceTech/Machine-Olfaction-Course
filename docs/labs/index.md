---
layout: default
title: 'Computational and design laboratories'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [Modules](../modules/index.md) · **Labs** · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / Computational and design laboratories

<!-- course-navigation:end -->

# Computational and design laboratories

These labs build the habit of predicting a response, calculating it independently, and then deciding whether the prediction answers the engineering question. Most exercises run with Python's standard library. Code appears in the Markdown so that the course remains portable; copy a complete Python block into a local script or notebook cell.

**All numerical datasets embedded in the labs are synthetic unless explicitly identified otherwise.** Their results demonstrate model behavior, not the performance of an actual sensor. Public datasets are linked separately with provenance and licensing caveats.

| Lab | Question | Main artifact | Preparation |
| --- | --- | --- | --- |
| [01. Units and the measurement chain](01-units-and-measurement.md) | How much material reaches the instrument? | Unit audit and mass-balance worksheet | 01–02 |
| [02. Transport, loss, and storage](02-transport-and-storage.md) | Can a fast response conceal poor recovery? | Response and storage model | 03, 07–09 |
| [03. Impedance and identifiability](03-impedance-and-identifiability.md) | What can a spectrum distinguish? | Equivalent-circuit comparison and experimental plan | 04–06 |
| [04. Calibration and uncertainty](04-calibration-and-uncertainty.md) | What does a concentration estimate actually mean? | Fit, residual analysis, and uncertainty budget | 10–11 |
| [05. Array diversity and shared error](05-array-design.md) | When is another channel worth adding? | Mixing-matrix and redundancy analysis | 13–14 |
| [06. Drift and validation](06-drift-and-validation.md) | Can a model survive a new acquisition batch? | Honest validation protocol | 14–15 |
| [07. Plume timing](07-plume-and-timing.md) | Is a measured delay caused by transport or sensing? | Timing model with ambiguity analysis | 16 |
| [08. Capstone studio](08-capstone-studio.md) | Can the complete design be defended? | Requirements, architecture, evidence, tests, and limitations | Complete course |

<a id="section-standard-lab-report"></a>

## Standard lab report

Include the question, model and assumptions, units, reproducible calculation, numerical results, interpretation, one falsifying test, and the decision carried into your design notebook. Show at least one manual calculation that checks the code. Report errors you find and explain how you corrected them.

For a physical extension, use the [build ladder](../build-ladder.md). Institutionally approved apparatus and procedures are required before chemical or biological experimentation. No core assessment requires collecting breath, exposing a person to a test vapor, handling a hazardous target, or synthesizing a sensing material.

[Read the data guide](../references/data-and-reproducibility.md) · [Review assessment rubrics](../assessments/index.md)

<!-- course-footer:start -->
---

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
