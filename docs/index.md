---
layout: default
title: 'Electrochemical sensing and machine olfaction'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
**Home** · [Start](getting-started.md) · [Modules](modules/index.md) · [Labs](labs/index.md) · [Projects](projects/index.md) · [Library](references/index.md) · [Site map](navigation.md)

<!-- course-navigation:end -->

# Electrochemical sensing and machine olfaction

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [The learning tree](#section-the-learning-tree)
- [What you will be able to do](#section-what-you-will-be-able-to-do)
- [Choose a route](#section-choose-a-route)
- [A note about evidence](#section-a-note-about-evidence)

</details>
<!-- course-toc:end -->

**Learn how molecules become measurements, and how measurements become useful decisions.**

A camera receives light. A microphone receives pressure waves. A chemical sensor must do something more physically intimate: bring molecules to a material, allow a molecular interaction, and measure the resulting change. The chemistry, plumbing, electronics, and inference all become part of the instrument.

This curriculum develops those connections at university engineering level. Its central question is practical: **what evidence would make a chemical measurement trustworthy outside the experiment that first demonstrated it?**

| Start here | What you will find |
| --- | --- |
| [New to the course](getting-started.md) | Prerequisite diagnostic and a first design exercise |
| [Study the 18 modules](modules/index.md) | Six subject groups with a guided lesson sequence |
| [Practice in the labs](labs/index.md) | Eight computational and engineering-design assignments |
| [Choose a project](projects/index.md) | Documented teaching systems, simulations, and independent extensions |
| [Find a specific topic](navigation.md) | Every page, grouped by subject and searchable with browser Find |

<a id="section-the-learning-tree"></a>

## The learning tree

```text
Electrochemical sensing and machine olfaction
|
+-- Molecular foundations
|   +-- Concentration, chemical identity, and measurement
|   +-- Thermodynamics, redox, and reference potentials
|   +-- Diffusion, convection, and phase partitioning
|
+-- Sensing interfaces
|   +-- Electrodes, double layers, and adsorption
|   +-- Ionic liquids, water, and material selection
|   +-- Current, potential, and impedance measurements
|
+-- Sampling and instruments
|   +-- Tubes, flow, filters, and humidity
|   +-- Storage, valves, modularity, and contamination
|   +-- Potentiostats, noise, digitization, and embedded systems
|
+-- Evidence and inference
|   +-- Calibration, uncertainty, and detection limits
|   +-- Arrays, signal features, and model validation
|   +-- Drift, unknown mixtures, and changing environments
|
+-- Applications and research
    +-- Breath research and clinical evidence
    +-- Biological olfaction and active sampling
    +-- Emerging materials, realistic benchmarks, and design tradeoffs
```

The branches share a trunk: an end-to-end measurement chain. A sophisticated classifier cannot restore an analyte lost in a sampling tube. A selective interaction cannot compensate for an unstable reference electrode. A low instrumental noise floor cannot establish clinical usefulness. The course shows how to connect each local result to the whole system.

<a id="section-what-you-will-be-able-to-do"></a>

## What you will be able to do

By the end, you should be able to derive a simple electrochemical response model, design a sampling path around its assumptions, choose an electrical measurement mode, construct an uncertainty budget, evaluate an array's information content, and defend a validation plan. You should also be able to read a new paper and identify which part of that chain it actually demonstrates.

The program includes:

- Eighteen modules with worked examples and exercises.
- Eight labs spanning units, transport, impedance, calibration, array design, drift, plume timing, and a system capstone.
- An integrated signal-chain example, staged build ladder, and nine independent derivative-project proposals.
- A mathematics reference, glossary, instructor guide, and assessments with solutions.
- Annotated references and a guide to public data, including explicit limits on transferring results between sensing technologies.

The central design outcome is to derive the architecture from its requirements, explain why every subsystem is necessary, and propose useful independently documented variations. Follow the [design studio](design-studio.md), run the [integrated example](integrated-example.md), and develop a project through the [build ladder](build-ladder.md).

<a id="section-choose-a-route"></a>

## Choose a route

| Your goal | Suggested entrance |
| --- | --- |
| Learn the complete engineering chain | [Full curriculum and semester schedule](curriculum.md) |
| Enter from electrical engineering or computer science | [Chemistry and transport bridge](getting-started.md) followed by modules 01–06 |
| Enter from chemistry or materials science | Modules 01–06 as review, then [electronics](modules/10-electronics-and-embedded-systems.md), [calibration](modules/11-calibration-and-uncertainty.md), and [inference](modules/15-machine-learning-and-domain-shift.md) |
| Evaluate a published device result | [Evidence-reading guide](references/index.md) and [system design](modules/18-system-design-and-responsible-use.md) |
| Run a seminar or project course | [Teaching guide](teaching-guide.md) and [capstone studio](labs/08-capstone-studio.md) |

<a id="section-a-note-about-evidence"></a>

## A note about evidence

The course distinguishes physical laws used with explicit assumptions, engineering approximations, individual research demonstrations, and capabilities awaiting validation. An equation is useful only over its stated domain. A reported detection limit belongs to the particular procedure that produced it. An observed association between a breath pattern and a health condition does not by itself establish a diagnosis.

Computational labs use clearly identified synthetic data unless a public dataset is explicitly introduced. They are designed for learning and model criticism. They do not constitute device validation, clinical practice, or instructions for human sampling.

**Research checked: 22 November 2026.** Begin with the [prerequisite diagnostic](getting-started.md), or go directly to [Module 01: molecules and measurement](modules/01-molecules-and-measurement.md).

<!-- course-footer:start -->
---

[Back to top](#page-top) · [Site map](navigation.md) · [Course home](index.md)
<!-- course-footer:end -->
