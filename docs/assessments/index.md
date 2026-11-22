---
layout: default
title: 'Assessments and evaluation rubrics'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [Modules](../modules/index.md) · [Labs](../labs/index.md) · [Projects](../projects/index.md) · [Library](../references/index.md) · [Site map](../navigation.md)

[Course home](../index.md) / Assessments and evaluation rubrics

<!-- course-navigation:end -->

# Assessments and evaluation rubrics

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Suggested course weighting](#section-suggested-course-weighting)
- [Lab rubric: 20 points](#section-lab-rubric-20-points)
- [Literature critique rubric: 20 points](#section-literature-critique-rubric-20-points)
- [Capstone rubric: 100 points](#section-capstone-rubric-100-points)
- [Oral defense prompts](#section-oral-defense-prompts)
- [Passing the design objective](#section-passing-the-design-objective)

</details>
<!-- course-toc:end -->

Assessment should reward defensible reasoning, not just correct-looking numbers. Students must specify assumptions, units, evidence, and the limit of their conclusion. The course's north star is a coherent design and the ability to derive useful independent extensions from public science.

[Integrated problem set](problem-set.md) · [Worked solutions](solutions.md) · [Capstone studio](../labs/08-capstone-studio.md)

<a id="section-suggested-course-weighting"></a>

## Suggested course weighting

| Component | Weight | Evidence expected |
| --- | --- | --- |
| Problem sets | 20% | Correct models, derivations, units, and interpretation |
| Computational/design labs | 25% | Reproducibility, numerical checks, failure analysis |
| Literature critique | 15% | Accurate attribution, evidence boundaries, constructive next experiment |
| Midterm | 15% | Independent integration of chemistry, sampling, and measurement |
| Capstone | 25% | Requirements-to-test coherence and honest validation |

<a id="section-lab-rubric-20-points"></a>

## Lab rubric: 20 points

| Criterion | Points | Full-credit behavior |
| --- | --- | --- |
| Question and assumptions | 4 | Defines a measurable question and states the domain of its model |
| Calculation and units | 5 | Reproducible work with a correct independent check |
| Interpretation | 5 | Connects outputs to the physical question without overclaiming |
| Failure analysis | 3 | Identifies a plausible alternative explanation and discriminating test |
| Design artifact | 3 | Converts learning into a justified decision for the final system |

A calculation that is numerically correct but dimensionally inconsistent cannot receive full calculation credit. A report that treats synthetic data as experimental evidence cannot receive full interpretation credit until corrected.

<a id="section-literature-critique-rubric-20-points"></a>

## Literature critique rubric: 20 points

Award 4 points each for clear scientific question, accurate evidence summary, methods/control analysis, fair comparison with an alternative, and a falsifiable next experiment. A strong critique identifies what a paper contributes before identifying what it leaves unresolved. Distinguish an omission from an error; the authors may not have intended to address your application.

Require students to state whether they read the full article, supplementary methods, or only an abstract. Credit a careful abstract-level reading with appropriately narrow conclusions. Do not reward invented methodological detail.

<a id="section-capstone-rubric-100-points"></a>

## Capstone rubric: 100 points

| Criterion | Points | Review question |
| --- | --- | --- |
| Intended use and requirements | 10 | Is the primary quantity and decision clearly defined? |
| Mechanistic reasoning | 15 | Does the design connect molecular interaction to an observable with competing explanations addressed? |
| Sampling and interface design | 15 | Are transport, conditioning, storage, and module interactions quantified? |
| Readout and instrumentation | 10 | Are gain, noise, bandwidth, reference, and saturation considered? |
| Calibration and inference | 15 | Are independent validation, drift, unknown samples, and uncertainty handled? |
| Build and verification | 15 | Is there an executable staged build plan and a requirements-to-test matrix? |
| Independent extension | 10 | Is a useful derivative grounded in public sources with a distinct architecture and documented provenance? |
| Communication and limitations | 10 | Can another engineer reproduce the reasoning and distinguish demonstrated results from proposals? |

For a software-only derivative, apply the same principles to data provenance, model assumptions, interfaces, numerical correctness, and scope of validation. Do not penalize a justified choice to omit new sensing chemistry.

<a id="section-oral-defense-prompts"></a>

## Oral defense prompts

1. Which unknown is most likely to invalidate your design, and what is the smallest experiment that addresses it?
2. If humidity and target concentration change together, what breaks first?
3. What evidence supports the proposed interfacial mechanism beyond a fitted electrical curve?
4. Which module replacement would require recalibration, and why?
5. How does the system behave when it receives an unfamiliar sample or a disconnected channel?
6. What did your best validation result actually generalize across?
7. Which alternative architecture would you choose if your preferred material failed?
8. Which parts of the project have independent public provenance, and what review remains before commercialization?

<a id="section-passing-the-design-objective"></a>

## Passing the design objective

A student demonstrates the central objective by deriving the architecture from requirements, not by reproducing a diagram. They must be able to explain why a component is present, what could replace it, what failure it introduces, and how its contribution is measured. They must also identify one useful adjacent project whose evidence and implementation can be developed independently.

[Open the problem set](problem-set.md) · [Return to design studio](../design-studio.md)

<!-- course-footer:start -->
---

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
