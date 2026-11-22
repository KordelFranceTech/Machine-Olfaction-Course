---
layout: default
title: 'Teaching guide and seminar plans'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](index.md) · [Start](getting-started.md) · [Modules](modules/index.md) · [Labs](labs/index.md) · [Projects](projects/index.md) · [Library](references/index.md) · [Site map](navigation.md)

[Course home](index.md) / Teaching guide and seminar plans

<!-- course-navigation:end -->

# Teaching guide and seminar plans

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Before the first meeting](#section-before-the-first-meeting)
- [A repeatable class structure](#section-a-repeatable-class-structure)
- [Demonstrations that expose misconceptions](#section-demonstrations-that-expose-misconceptions)
- [Journal-club sequence](#section-journal-club-sequence)
- [A design review midway through the course](#section-a-design-review-midway-through-the-course)
- [Managing different resource levels](#section-managing-different-resource-levels)
- [Assessing independent innovation](#section-assessing-independent-innovation)
- [Adaptation and accessibility](#section-adaptation-and-accessibility)
- [End-of-course reflection](#section-end-of-course-reflection)

</details>
<!-- course-toc:end -->

Teach the course as a connected design problem. Students should repeatedly move between a physical model, a measured or simulated observation, and a decision about a device. This is especially valuable in mixed cohorts: an electrical engineer may understand noise but miss sample chemistry, while a chemist may understand redox behavior but overlook feedback and data leakage.

The intended outcome is an engineer who can derive a complete sensing architecture and also recognize useful independent extensions. The [design studio](design-studio.md) supplies the integration sequence; the [derivative projects](derivative-projects.md) supply alternatives for different facilities and interests.

<a id="section-before-the-first-meeting"></a>

## Before the first meeting

Ask students to attempt the diagnostic and bring an example of a measurement they trust. Have them identify the quantity, reference, uncertainty, and decision attached to it. A thermometer, a battery meter, or a weather record is enough. This establishes that measurement is an inference process before the chemistry becomes specialized.

Create groups with complementary backgrounds. Assign rotating roles: mechanism reviewer, units reviewer, data-provenance reviewer, and design integrator. These are responsibilities, not permanent disciplinary identities.

<a id="section-a-repeatable-class-structure"></a>

## A repeatable class structure

For a 90-minute meeting:

1. Spend 10 minutes on an observable puzzle, such as a faster response accompanied by lower recovery.
2. Spend 20 minutes developing the minimum physical model and writing its assumptions.
3. Spend 20 minutes on a worked example with an independent unit or limiting-case check.
4. Spend 20 minutes comparing competing explanations or design options in small groups.
5. Spend 15 minutes updating the design notebook with a decision and verification criterion.
6. Use the last 5 minutes for an exit question: what observation would change today's conclusion?

Shorter meetings can split the calculation and design discussion. Avoid using all available time to introduce more equations; students need to decide when an equation is appropriate.

<a id="section-demonstrations-that-expose-misconceptions"></a>

## Demonstrations that expose misconceptions

**A sensor with a perfect fit and the wrong story.** Generate an RC spectrum and invite several physical interpretations. Ask what additional observation would distinguish them. Then discuss why better residuals do not establish a unique mechanism.

**A faster sample path with a worse sample.** Use Lab 02 to show that loss lowers a plateau and can shorten the time to reach 90% of that plateau. Ask each group to define the response metric before comparing designs.

**An array with more channels but less useful information.** Compare duplicated and independent response vectors in Lab 05. Introduce common-mode humidity error. Ask why majority voting may fail even when each channel appears individually reliable.

**An excellent classifier that learned the acquisition schedule.** Use Lab 06. Let students inspect the data dictionary and predict the result before running the split. Require them to define the deployment question that each split answers.

**A clinically impressive percentage with weak predictive value.** Work the prevalence example without attaching it to a disease or device. Ask why population selection and reference methods must be inspected before transporting sensitivity and specificity.

<a id="section-journal-club-sequence"></a>

## Journal-club sequence

Use three meetings rather than one broad “latest research” presentation.

**Meeting 1: mechanism.** Select an interfacial or materials paper. Students identify what was measured directly and what was inferred. Each proposes a competing explanation and one independent observable.

**Meeting 2: instrument.** Select a sampling, electronics, or array paper. Students construct a requirements-to-test table and list conditions needed for the headline result.

**Meeting 3: generalization.** Select a drift or external-validation study. Students reconstruct the unit of independence, data partitions, and uncertainty. They propose the next evaluation matching a new intended use.

Use the [reading maps](references/index.md) to choose accessible sources. If full methods are unavailable, narrow the assignment explicitly. Do not ask students to make a reproducibility judgment from an abstract alone.

<a id="section-a-design-review-midway-through-the-course"></a>

## A design review midway through the course

By the end of sampling and electronics, every group should have a measurement contract, mechanism diagram, transport budget, sample-path sketch, and signal/noise allocation. The mid-course review asks whether these artifacts agree.

A useful review catches mismatched timescales: a model that expects rapid pulses while a thick film takes tens of seconds to equilibrate; a high-gain readout that saturates during charging; a storage plan that changes the quantity being calibrated; or a classifier trained on labels unavailable at inference time.

Require each group to remove or redesign at least one unjustified feature. The purpose is to demonstrate that understanding can simplify a system.

<a id="section-managing-different-resource-levels"></a>

## Managing different resource levels

A computer-only cohort can complete the model, data, and validation portions of the capstone. A teaching electronics laboratory can add the dummy-cell stage. A chemistry laboratory can extend the course using institutionally approved procedures, appropriate reference materials, and trained supervision. No core objective requires custom ionic-liquid synthesis, hazardous gas preparation, human sampling, or disease inference.

For software-focused students, insist on a physical source model and a clear data dictionary. For hardware-focused students, insist on independent validation and reproducibility. For materials-focused students, insist on a complete sample and electrical measurement chain.

<a id="section-assessing-independent-innovation"></a>

## Assessing independent innovation

The derivative proposal should begin with a useful result and two possible architectures. Students must identify which public principles they use, what they independently created, and what they copied or imported under specific terms. They should present a bounded acceptance test, not a promise of commercial superiority.

The [responsible-innovation guide](responsible-innovation.md) is a documentation workflow. Students are not expected to provide a legal opinion. Their responsibility is to preserve provenance, exclude confidential information, and accurately state the scope of any review.

<a id="section-adaptation-and-accessibility"></a>

## Adaptation and accessibility

Use the glossary actively when words have multiple meanings, especially sensitivity, bias, reference, and concentration. Ask students to explain an equation in ordinary language before deriving it. Provide the same information in text and tables; do not make color or a complex interactive visualization the only route to understanding.

The equations and diagrams remain readable as plain Markdown. Learners can reproduce the numerical examples with a calculator. Assessment should allow an equally rigorous non-programming derivation for early labs, while the final computational work should still be reproducible.

<a id="section-end-of-course-reflection"></a>

## End-of-course reflection

Ask students to revisit their first device sketch. For every changed component, record which physical insight or evidence caused the change. Then ask them to explain a second useful system using the same principles but a different architecture. That comparison demonstrates transferable engineering understanding.

[Use the semester schedule](curriculum.md) · [Open assessment rubrics](assessments/index.md)

<!-- course-footer:start -->
---

[Back to top](#page-top) · [Site map](navigation.md) · [Course home](index.md)
<!-- course-footer:end -->
