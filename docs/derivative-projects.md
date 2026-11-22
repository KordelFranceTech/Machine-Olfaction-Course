---
layout: default
title: 'Nearby projects: useful engineering with distinct architectures'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](index.md) · [Start](getting-started.md) · [Modules](modules/index.md) · [Labs](labs/index.md) · [**Projects**](projects/index.md) · [Library](references/index.md) · [Site map](navigation.md)

[Course home](index.md) / [Projects](projects/index.md) / Nearby projects: useful engineering with distinct architectures

<!-- course-navigation:end -->

# Nearby projects: useful engineering with distinct architectures

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Choose by the useful result](#section-choose-by-the-useful-result)
- [1. Calibration and drift workbench](#section-1-calibration-and-drift-workbench)
- [2. Impedance teaching instrument and dummy-cell kit](#section-2-impedance-teaching-instrument-and-dummy-cell-kit)
- [3. Sample-path and storage simulator](#section-3-sample-path-and-storage-simulator)
- [4. Humidity and recovery audit kit](#section-4-humidity-and-recovery-audit-kit)
- [5. Ambient carbon-dioxide logger](#section-5-ambient-carbon-dioxide-logger)
- [6. Metal-oxide classification classroom](#section-6-metal-oxide-classification-classroom)
- [7. Aqueous conductivity teaching system](#section-7-aqueous-conductivity-teaching-system)
- [8. Materials evidence explorer](#section-8-materials-evidence-explorer)
- [9. Active-sampling and search simulator](#section-9-active-sampling-and-search-simulator)
- [Turning a project into a defensible capstone](#section-turning-a-project-into-a-defensible-capstone)

</details>
<!-- course-toc:end -->

The skills in this curriculum support many useful systems. A student can contribute measurement software, educational instruments, sample-handling analysis, environmental data tools, or autonomous sampling methods without attempting every subsystem of a complete chemical-identification instrument at once.

The nine projects below are **technical project proposals, not determinations of freedom to operate**. Public evidence and an independently documented architecture are valuable starting points; they do not establish legal clearance. Every proposal has an unassessed IP status. Use the [responsible-innovation workflow](responsible-innovation.md) before external release or commercialization.

<a id="section-choose-by-the-useful-result"></a>

## Choose by the useful result

| Project | Useful deliverable | Main architecture | Planning effort | Resource level |
| --- | --- | --- | --- | --- |
| 1. Calibration and drift workbench | Reproducible evaluation of calibration failure | Synthetic data and statistical software | 2–3 weeks | Existing computer |
| 2. Impedance teaching instrument | Validated measurement of passive circuits | Low-voltage electronics and resistor/capacitor standards | 4–6 weeks | Moderate; bench access |
| 3. Sample-path simulator | Compare delay, loss, and storage tradeoffs | Mass-balance and diffusion models | 2–4 weeks | Existing computer |
| 4. Humidity and recovery audit kit | Quantify housing and airflow effects | Commercial humidity modules and approved benign test conditions | 3–5 weeks | Low to moderate |
| 5. Ambient carbon-dioxide logger | Reliable environmental time series | Commercial optical gas module and data logger | 3–4 weeks | Low to moderate |
| 6. Metal-oxide classification classroom | Demonstrate classification and domain shift | Public data; optional purchased sensor modules | 2–5 weeks | Computer first; optional hardware |
| 7. Aqueous conductivity teaching system | Understand calibration and temperature effects | Commercial conductivity cell and aqueous standards | 3–5 weeks | Moderate; teaching laboratory |
| 8. Materials evidence explorer | Compare studies without losing conditions | Structured public-source database | 2–4 weeks | Existing computer |
| 9. Active-sampling simulator | Compare sensing policies under limited resources | Simulated field, sensor dynamics, and planning | 4–6 weeks | Existing computer |

These are planning estimates for a pair of students contributing about six hours each per week. They are not current prices, procurement quotes, or promises of completion time. “Low” assumes a few purchased development modules; “moderate” assumes additional standards, fixtures, or shared test equipment. Reuse institutional instruments where possible.

For each project, first complete the requirements and verification stages in the [build ladder](build-ladder.md). Record a useful minimum result before adding optional complexity. A well-characterized limitation is an acceptable engineering outcome.

<a id="section-1-calibration-and-drift-workbench"></a>

## 1. Calibration and drift workbench

**Useful outcome:** a teaching and research tool that shows when a calibration ceases to support its stated uncertainty. The architecture is software operating on synthetic signals, with an optional public-data extension.

**Public basis:** [Croarkin's NIST measurement-process characterization chapter](https://www.nist.gov/publications/nistsematech-engineering-statistics-handbook-chapter-2-measurement-process) covers calibration, repeatability, and stability. The [scikit-learn documentation on leakage](https://scikit-learn.org/stable/common_pitfalls.html) explains why preprocessing must be fitted using training data. These support the concepts; the proposed workbench is an original classroom exercise.

**Build plan and artifacts:**

1. Define a synthetic response `y = a_device + b_device c + h RH + d t + noise`, with units and a saved random seed. Create independent device, day, and exposure identifiers.
2. Implement a baseline linear calibration and a version that models a known humidity term. Preserve the uncorrected data.
3. Compare random-row evaluation with device-held-out and forward-in-time evaluation. Keep model selection separate from final testing.
4. Produce residual plots, interval-coverage plots, and a drift report. Deliver a generator specification, data dictionary, versioned analysis, and short user guide.

**Acceptance tests:** in a noiseless case, recover the injected coefficients to numerical tolerance; in repeated simulations, quantify coverage of nominal intervals; verify that a held-out device is absent from preprocessing and fitting; demonstrate a deliberate failure when an unmodeled drift term is introduced. An inflated random-split score should be explained rather than celebrated.

**Dependencies and limits:** Modules 01, 13–16 as selected through the curriculum; basic programming and statistics. Synthetic success establishes correct behavior under the generator, not physical sensor performance. **IP clearance:** unassessed; record software and data licenses and review any later product-specific adaptation.

<a id="section-2-impedance-teaching-instrument-and-dummy-cell-kit"></a>

## 2. Impedance teaching instrument and dummy-cell kit

**Useful outcome:** an instrument or instrument adapter that measures known passive networks and teaches the difference between a waveform, a transfer function, and a physical mechanism. Its initial architecture contains a controlled low-voltage source, measurement channels, and resistor/capacitor networks.

**Public basis:** [Dryden and Wheeler's DStat paper](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0140349) and [Rowe and colleagues' CheapStat paper](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0023783) provide public electrochemical-instrument design examples. They are architectural reading, not evidence that either unmodified design supports the proposed impedance frequency range or accuracy.

**Build plan and artifacts:**

1. Start with a simulated resistor, capacitor, and parallel RC branch. Predict magnitude and phase analytically using Module 06.
2. Select an existing teaching instrument or a documented open-hardware base after reviewing its current license and component availability. Define voltage, current, and bandwidth limits before construction.
3. Measure passive dummy cells at frequencies chosen to bracket their time constants. Estimate amplitude and phase from synchronized channels.
4. Deliver the electrical schematic, wiring diagram, uncertainty budget, calibration record, and a workbook that compares prediction with observation.

**Acceptance tests:** resistor phase should agree with zero within a declared tolerance; RC corner frequencies should agree with component measurements and their uncertainties; deliberate clipping must be flagged; reversing the frequency sweep should expose drift; calibration and test networks should differ. Set numerical tolerances from the available equipment, then hold them fixed during evaluation.

**Dependencies and limits:** electronics supervision, Modules 02, 04, and 06, and access to an independent meter or oscilloscope. Begin with isolated, current-limited low-voltage equipment. Passing passive-network tests does not establish electrochemical-cell performance. **IP clearance:** unassessed; review the particular hardware, firmware, and software licenses before distributing a modified design.

<a id="section-3-sample-path-and-storage-simulator"></a>

## 3. Sample-path and storage simulator

**Useful outcome:** a calculator that shows how inlet volume, flow, partitioning, and wall retention change a sample before it reaches a transducer. Its architecture is a chain of physical models with explicit boundaries.

**Public basis:** [Sander's Henry-law compilation](https://acp.copernicus.org/articles/23/10901/2023/) provides rigorous partition conventions for water. Module 03 supplies independently derived chamber and diffusion calculations. The simulator must distinguish measured material constants from hypothetical classroom values.

**Build plan and artifacts:**

1. Implement a well-mixed chamber, a transport delay, and a reversible wall-storage compartment as separate components.
2. Connect components using conserved molar flow. Include a sealed-storage mode in which leakage or wall uptake changes composition over time.
3. Allow the user to compare two geometries and inspect each stage's response to the same concentration pulse.
4. Export a Markdown report with equations, parameter provenance, a mass balance, response/recovery metrics, and sensitivity to uncertain parameters.

**Acceptance tests:** recover the analytical first-order response when wall interactions are disabled; conserve total modeled material in a closed loss-free system; approach zero outlet loss as the wall capacity approaches zero; show convergence when the time step is reduced. Check that changing a Henry-law convention without converting units triggers an error.

**Dependencies and limits:** Module 03 and numerical integration. A useful minimum project needs no gas-handling hardware. Wall coefficients fitted to one substance or material are not transferable without evidence. A well-mixed chamber model cannot establish the behavior of a complex three-dimensional inlet.

**Extension:** use the tool to propose the most informative experiment for distinguishing slow chamber turnover from slow surface release. This turns a simulator into an experimental-planning aid. **IP clearance:** unassessed; review any imported model implementation or later physical assembly separately.

<a id="section-4-humidity-and-recovery-audit-kit"></a>

## 4. Humidity and recovery audit kit

**Useful outcome:** a kit that measures how an enclosure, inlet, or sensor placement changes humidity response and recovery. The architecture combines purchased humidity/temperature modules, timestamps, and a replaceable benign airflow fixture.

**Public basis:** the [Sensirion SHT40 product page and linked documentation](https://sensirion.com/products/catalog/SHT40) provide an example of a commercial digital humidity/temperature module. Use the current datasheet's electrical and environmental limits for the purchased variant; the project does not assume every module has the same accuracy.

**Build plan and artifacts:**

1. Log two modules side by side to establish their offset and temporal agreement.
2. Place one in a candidate enclosure and retain one as a comparison sensor. Use only instructor-approved ambient or controlled water-vapor conditions with no intentional condensation on electronics.
3. Repeat transitions in randomized order, swap the sensors between positions, and distinguish position effects from device effects.
4. Deliver the fixture drawing, synchronization check, raw records, recovery definition, and a report comparing response delay and hysteresis.

**Acceptance tests:** timestamps remain monotonic; missing data and communication failures are flagged; device swapping preserves or reverses the observed difference as predicted; repeatability is reported across multiple transitions; the report identifies whether the comparison sensor is fast enough to resolve the effect. Define recovery as a specified distance from a stable baseline rather than an impression from a plot.

**Dependencies and limits:** Modules 01 and 03; approved teaching-laboratory conditions. Use existing institutional humidity references when quantitative accuracy is required. This project evaluates humidity transport and instrumentation; it does not establish VOC recovery, sterilization, or a clinical sampling process. **IP clearance:** unassessed; purchased-component use and any original fixture design require their own review before product release.

<a id="section-5-ambient-carbon-dioxide-logger"></a>

## 5. Ambient carbon-dioxide logger

**Useful outcome:** an environmental logger with reliable records, transparent calibration settings, and a clearly bounded interpretation. The architecture uses a purchased optical CO₂ module, a controller, local storage, and a ventilated enclosure.

**Public basis:** the [Sensirion SCD40 documentation](https://sensirion.com/products/catalog/SCD40) describes a commercial photoacoustic NDIR CO₂ sensor. The manufacturer distinguishes a specified measurement range from the wider output range. That distinction is a useful engineering lesson; a reported number is not necessarily within the guaranteed accuracy region.

**Build plan and artifacts:**

1. Read the module documentation and record supply requirements, communication checks, timing, compensation inputs, and calibration modes.
2. Implement logging with units, device identity, firmware version, pressure/temperature metadata where relevant, and explicit quality flags.
3. Compare colocated measurements with an independently characterized reference over normal ambient variation. Evaluate enclosure placement and self-heating.
4. Produce a dashboard or Markdown report that separates raw observations, any corrections, and periods outside the validated operating envelope.

**Acceptance tests:** reconnect after a controlled communication interruption without silently fabricating samples; preserve configuration across a restart; identify stale readings; compare error against the combined device/reference uncertainty; demonstrate that automatic baseline correction settings match the intended environment rather than accepting defaults blindly.

**Dependencies and limits:** basic embedded programming and environmental logging. This is an ambient observational project: no breath collection, deliberate CO₂ accumulation, or exposure challenge is required. CO₂ data alone do not identify every indoor contaminant or determine a person's health. **IP clearance:** unassessed; a legitimate purchased component is a practical integration route, but its purchase does not establish clearance for every surrounding system or use.

<a id="section-6-metal-oxide-classification-classroom"></a>

## 6. Metal-oxide classification classroom

**Useful outcome:** an educational demonstration of how broad sensor responses can support restricted classification while failing under domain shift. Begin with software using a public dataset; add commercial modules only after the evaluation plan works.

**Public basis:** [Vergara's UCI Gas Sensor Array Drift Dataset](https://archive.ics.uci.edu/dataset/224/gas+sensor+array+drift+dataset) contains measurements from a multi-sensor gas-discrimination experiment. Its current license section conflicts with legacy research-only wording; consult the [dataset notes](references/olfaction-and-data.md) and resolve reuse terms before redistribution or commercial use. A [commercial SGP40 module](https://sensirion.com/products/catalog/SGP40) is an optional integration example; its processed VOC output should not be relabeled as a universal compound-specific concentration.

**Build plan and artifacts:**

1. Read the dataset documentation and identify the exposure, feature, and batch units before splitting data.
2. Implement a simple baseline classifier and a chronological evaluation. Fit scaling and feature selection only within training data.
3. Compare performance across batches, including class-specific errors and uncertainty. Include a deliberately shifted or unfamiliar class in a separate rejection exercise.
4. Deliver an analysis card, provenance record, confusion matrices, and a demonstration explaining why good within-batch accuracy can coexist with poor later performance.

**Acceptance tests:** a batch cannot appear on both sides of a batch-held-out evaluation; shuffled labels should remove real predictive signal within statistical variation; results are reproducible from a pinned environment; the display identifies unknown or out-of-scope inputs. Do not require a predetermined high score as the success criterion.

**Dependencies and limits:** classification and validation modules; no hazardous gas generation is necessary. Public features may not contain every variable needed to diagnose drift. An optional hardware extension must use approved benign conditions and its own labeled study. **IP clearance:** unassessed; satisfy dataset attribution and inspect code/module terms, then review any proposed commercial application separately.

<a id="section-7-aqueous-conductivity-teaching-system"></a>

## 7. Aqueous conductivity teaching system

**Useful outcome:** a practical demonstration that an electrical measurement becomes a chemical quantity only through geometry, calibration, and controlled conditions. The architecture uses a commercial conductivity cell or meter, temperature measurement, and certified or instructor-approved aqueous standards.

**Public basis:** [NIST's conductivity reference-material publication](https://doi.org/10.6028/NIST.SP.260-142) explains the measurement basis and standards. [NIST's calibration procedures, including conductivity-meter verification](https://nvlpubs.nist.gov/nistpubs/ir/2019/NIST.IR.8250.pdf), provide an example of a documented metrology workflow. These are reference methods, not a claim that a classroom implementation attains NIST uncertainty.

**Build plan and artifacts:**

1. Define the expected conductivity range and choose a cell appropriate to it. Record the cell constant and temperature convention.
2. Verify the instrument using an independent standard near the working range, following the standard supplier's and laboratory's instructions.
3. Examine repeat measurements, temperature dependence, and carryover using approved aqueous solutions. Keep sample identities and handling history.
4. Produce a calibration curve, uncertainty budget, cleaning/recovery record, and an explanation of the relation `kappa = K_cell/R`.

**Acceptance tests:** an independent check standard agrees within a predeclared tolerance justified by uncertainty; temperature is recorded for every result; repeatability and between-day differences are separated; a known carryover event is detectable. If an experimental low-voltage interface is added, validate it on passive loads first.

**Dependencies and limits:** Modules 01, 04, and 06; teaching-laboratory supervision. Conductivity is generally nonspecific: different ionic mixtures can produce similar readings. The project is not a potable-water safety test. **IP clearance:** unassessed; document the purchased cell, interface design, firmware, and intended use before external distribution.

<a id="section-8-materials-evidence-explorer"></a>

## 8. Materials evidence explorer

**Useful outcome:** a searchable evidence table that prevents inappropriate comparison of sensing-material results. The architecture is a structured literature database with condition-aware filters and links to original sources.

**Public basis:** the [NIST Chemistry WebBook](https://webbook.nist.gov/chemistry/), [Sander's partition database](https://henrys-law.org/henry/), and the [foundations bibliography](references/fundamentals.md) illustrate different kinds of chemical and electrochemical evidence. Link to sources and record short original summaries rather than copying articles or figures wholesale.

**Build plan and artifacts:**

1. Define a schema for material identity, measured quantity, units, temperature, water content, electrode configuration, method, sample count, and uncertainty.
2. Add an explicit evidence type: measured, modeled, inferred, or missing. Store the citation and exact location supporting each imported number.
3. Implement comparison rules that flag incompatible units, undefined detection limits, different matrices, and absent conditions.
4. Deliver at least twenty carefully checked records, a schema guide, an audit log, and three worked examples where an apparently strong comparison becomes inconclusive after checking conditions.

**Acceptance tests:** independently recheck a random subset against the original sources; incompatible units cannot be silently averaged; unknown conditions remain unknown; a corrected paper can supersede a value without erasing the old provenance; filters never imply that omitted studies were negative results.

**Dependencies and limits:** careful reading and data modeling. Twenty curated records can be more useful than thousands of unverified extracted claims. This is an evidence-management tool, not a recommendation that one material is universally superior. **IP clearance:** unassessed; respect database and article licenses, and keep confidential laboratory information out of the public record.

<a id="section-9-active-sampling-and-search-simulator"></a>

## 9. Active-sampling and search simulator

**Useful outcome:** a reproducible comparison of where and when to sample when sensor response, energy, and time are limited. The architecture combines a simulated concentration field, a delayed/noisy sensor model, and several movement or sampling policies.

**Public basis:** [Vergassola, Villermaux, and Shraiman's 2007 infotaxis paper](https://doi.org/10.1038/nature05464) introduced an information-based search strategy for intermittent cues. It motivates one policy class; it does not guarantee that the same strategy dominates under every field or sensor model.

**Build plan and artifacts:**

1. Implement a small spatial grid with a known source and a documented stochastic observation model. Keep simulation truth separate from the agent's information.
2. Add sensor response/recovery dynamics, missed detections, and energy costs for motion and sampling.
3. Compare random search, a simple concentration-following policy, and an information-seeking policy under matched budgets.
4. Deliver reproducible trial seeds, success/time/energy distributions, ablation studies, and a report of the conditions in which each policy fails.

**Acceptance tests:** the agent cannot read hidden source coordinates; all policies receive the same permissible observations; performance is evaluated across many seeds and held-out field settings; a zero-information case behaves sensibly; slower recovery changes observations before it changes the policy's decisions. Report confidence intervals and censored trials that never locate the source.

**Dependencies and limits:** probability, numerical methods, and the transport/dynamics modules. A simulation result is evidence about the modeled world, not field-robot performance. An initial project needs no mobile hardware or chemical release. **IP clearance:** unassessed; check imported algorithms and software licenses, and assess any later physical system and application on its own facts.

<a id="section-turning-a-project-into-a-defensible-capstone"></a>

## Turning a project into a defensible capstone

Choose one project, then use the [capstone studio](labs/08-capstone-studio.md) to assemble requirements, architecture, a verification matrix, a provenance record, and a demonstration. The minimum demonstration should answer one useful question with a declared error or limitation. A second subsystem should be added only when it helps answer that question.

The strongest transfer of learning is visible when a student can explain why a different physical architecture requires different calibration, controls, and interpretation. Reusing the reasoning from the [design studio](design-studio.md) is encouraged. Reusing an unsupported performance assertion is not a substitute for measurement.

<!-- course-footer:start -->
---

[Previous: Build ladder: from models to a physical demonstrator](build-ladder.md) · [Project routes](projects/index.md) · [Next: Responsible innovation and independent design records](responsible-innovation.md)

[Back to top](#page-top) · [Site map](navigation.md) · [Course home](index.md)
<!-- course-footer:end -->
