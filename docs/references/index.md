---
layout: default
title: 'Research library and evidence-reading guide'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [Modules](../modules/index.md) · [Labs](../labs/index.md) · [Projects](../projects/index.md) · **Library** · [Site map](../navigation.md)

[Course home](../index.md) / Research library and evidence-reading guide

<!-- course-navigation:end -->

# Research library and evidence-reading guide

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Reading maps](#section-reading-maps)
- [A reading sequence for a new researcher](#section-a-reading-sequence-for-a-new-researcher)
- [Four kinds of statement to mark in your notebook](#section-four-kinds-of-statement-to-mark-in-your-notebook)
- [Literature critique worksheet](#section-literature-critique-worksheet)
- [Comparing research fairly](#section-comparing-research-fairly)
- [Source and reuse practice](#section-source-and-reuse-practice)

</details>
<!-- course-toc:end -->

The bibliography is organized around engineering questions rather than a single ranking of technologies. Each linked reading map identifies the source, what it contributes, and the limits of using it. Primary research papers support reported experimental findings. Official terminology, metrology, component documentation, and reporting guidance support definitions and engineering practice.

**Research checkpoint: 22 November 2026.** This is a curated teaching library, not an exhaustive systematic review. Recent papers are included when they help explain a concrete advance or unresolved question. “State of the art” here means understanding the strongest relevant approaches and their evidence boundaries, not declaring a universal best sensor.

<a id="section-reading-maps"></a>

## Reading maps

| Reading map | Questions it addresses |
| --- | --- |
| [Fundamentals](fundamentals.md) | What drives electrochemistry? How do interfaces and ionic media behave? What can electrical methods establish? |
| [Systems and validation](systems-and-validation.md) | How do sampling, conditioning, storage, electronics, uncertainty, and clinical study design affect a result? |
| [Olfaction and data](olfaction-and-data.md) | What do arrays add? What can biological coding teach us? Which contemporary research and datasets are informative? |
| [Data and reproducibility](data-and-reproducibility.md) | What data can a student use, what do they represent, and how should analyses be reproduced? |
| [Independent adjacent projects](../derivative-projects.md) | Which publicly grounded extensions are feasible with accessible tools? |

<a id="section-a-reading-sequence-for-a-new-researcher"></a>

## A reading sequence for a new researcher

Start with a definition or a simple physical model. Read the relevant module and reproduce its worked example. Then choose one foundational primary paper, one recent primary paper, and one engineering or validation source. The goal is to connect mechanism, implementation, and evidence rather than accumulate unrelated citations.

For electrochemical interfaces, compare a thermodynamic explanation with an actual structural or electrical experiment. For gas sampling, compare an ideal transport equation with a paper measuring material-dependent recovery. For machine learning, inspect dataset provenance before examining model performance. For health-related sensing, separate the analytical measurement from the study's population and reference outcome.

<a id="section-four-kinds-of-statement-to-mark-in-your-notebook"></a>

## Four kinds of statement to mark in your notebook

| Label | Meaning | Example of appropriate wording |
| --- | --- | --- |
| Established relationship with assumptions | A defined model applied within its domain | “Under the ideal-gas approximation, partial pressure is mole fraction times total pressure.” |
| Reported observation | A result attributed to a specific study | “The authors observed this behavior in the tested materials and conditions.” |
| Interpretation | An explanation compatible with available evidence | “This response is consistent with a transport limitation, but another control is needed.” |
| Proposal | An untested extension or next experiment | “A reference channel might reduce humidity sensitivity; this should be tested across devices.” |

A paper's conclusion may combine these categories. Separate them before reusing the result in a design. Favor the narrowest accurate interpretation. A successful component test should not silently become an instrument-level performance statement.

<a id="section-literature-critique-worksheet"></a>

## Literature critique worksheet

For each assigned paper, record:

1. The scientific question and the engineering decision it could inform.
2. Sample phase, target species, concentration basis, reference conditions, and any preparative steps.
3. Device count, material batches, independent samples, repeated measurements, and acquisition days.
4. Measured quantities versus fitted, inferred, simulated, or nominal quantities.
5. Controls that challenge the favored mechanism and alternatives that remain plausible.
6. Sensitivity, selectivity, response/recovery, detection limit, and uncertainty definitions.
7. Environmental conditions and whether mixtures, drift, and unknown samples were tested.
8. Data partitions and whether preprocessing, feature selection, or thresholds used test information.
9. Available raw data, code, supplementary methods, reuse terms, corrections, and retractions.
10. One decisive follow-up experiment and the result that would change your interpretation.

State your access basis. An abstract can verify a paper's identity and broad result; it cannot support a detailed methods audit. When full text is unavailable, choose a narrower discussion or an accessible alternative. Do not reconstruct unobserved methods from a familiar title.

<a id="section-comparing-research-fairly"></a>

## Comparing research fairly

Use a table with one column per operating condition and metric definition. A detection limit measured with a long integration time is not directly comparable with one from a brief pulse. A result from a dry pure gas differs from a humid mixture. One device measured a thousand times differs from a thousand independent devices. A test set containing neighboring samples from the same acquisition can answer a different question from a held-out manufacturing batch.

Treat publicly reported advantages as hypotheses about your use case until you have matched the conditions. This discipline does not diminish new research; it makes its contribution easier to identify and reproduce.

<a id="section-source-and-reuse-practice"></a>

## Source and reuse practice

Link to the original paper or official documentation near the supported statement. Preserve author names, year, title, and persistent identifiers where available. Avoid copying large passages or figures; write your own explanation and use original diagrams. Dataset access does not automatically imply unrestricted redistribution or commercial use. Source code, hardware files, article text, and data may each carry different terms.

The course provides short source annotations and independently constructed examples. Its numerical teaching examples should never be cited as experimental performance data.

[Explore current research](../modules/17-research-frontiers.md) · [Open the journal-club rubric](../assessments/index.md)

<!-- course-footer:start -->
---

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
