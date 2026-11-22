---
layout: default
title: 'Public data, provenance, and reproducibility'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [Modules](../modules/index.md) · [Labs](../labs/index.md) · [Projects](../projects/index.md) · [**Library**](index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Library](index.md) / Public data, provenance, and reproducibility

<!-- course-navigation:end -->

# Public data, provenance, and reproducibility

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Four data sources and what they can teach](#section-four-data-sources-and-what-they-can-teach)
- [Synthetic data as a controlled experiment](#section-synthetic-data-as-a-controlled-experiment)
- [Minimum data dictionary](#section-minimum-data-dictionary)
- [Partition before processing](#section-partition-before-processing)
- [Reproducibility record](#section-reproducibility-record)
- [Data-quality exercises](#section-data-quality-exercises)

</details>
<!-- course-toc:end -->

A useful dataset is an experimental record with a meaning, not just a matrix. Before selecting a modeling method, determine what each row represents, how the input was generated, how the reference was established, and which observations share a device, sample, or acquisition session.

<a id="section-four-data-sources-and-what-they-can-teach"></a>

## Four data sources and what they can teach

| Resource | Appropriate educational use | Important boundary |
| --- | --- | --- |
| [NIST Chemistry WebBook, SRD 69](https://webbook.nist.gov/chemistry/) | Look up thermochemical, vapor-pressure, spectral, or other property records and trace their references | Data availability differs by compound and property; conditions and uncertainties must be preserved |
| [Sander's Henry-law compilation, 2023](https://acp.copernicus.org/articles/23/10901/2023/) | Practice partition-coefficient conventions, unit conversion, and source-quality comparison | These compiled values are for water as solvent; do not substitute them for a different sensing medium |
| [UCI gas-sensor drift dataset](https://archive.ics.uci.edu/dataset/224/gas+sensor+array+drift+dataset) | Study batch separation, changing response, classification baselines, and validation design | Metal-oxide array data do not establish electrochemical performance; inspect terms before reuse |
| [UCI drift data with concentration labels](https://archive.ics.uci.edu/dataset/270/gas+sensor+array+drift+dataset+at+different+concentrations) | Compare classification with concentration estimation and calibration-transfer questions | Supplied features are not interchangeable with raw electrochemical traces; retain acquisition grouping |

The original experimental context for the drift resources is described by [Fonollosa, Rodríguez-Luján, and Huerta, 2015](https://doi.org/10.1016/j.dib.2015.01.003). The repository pages contain both a current license section and legacy restrictions whose wording is inconsistent. The course therefore links to the records without redistributing the data. Resolve permitted use with the responsible source before redistribution or commercial reuse.

<a id="section-synthetic-data-as-a-controlled-experiment"></a>

## Synthetic data as a controlled experiment

The core labs use invented systems with known equations and explicit assumptions. This makes it possible to deliberately introduce drift, label confounding, sensor delay, and shared error. Synthetic data are valuable precisely because you know how they were generated. They cannot establish the frequency of those mechanisms in real use.

Record the generator, parameters, random seed when applicable, and whether test conditions differ from training conditions. Keep the simulated truth available for evaluation but hidden from the inference function. A model accidentally given the true concentration, future samples, or batch outcome is solving a different problem from a deployed instrument.

A simulated classifier can obtain 100% accuracy and still be a poor scientific demonstration if the labels were encoded directly into an input field. The lab report should describe what information was available at decision time.

<a id="section-minimum-data-dictionary"></a>

## Minimum data dictionary

The following is a proposed schema, not a file format you must adopt.

| Field | Meaning | Example type |
| --- | --- | --- |
| record_id | Unique record identity | String |
| acquisition_id | One physically coherent acquisition | String |
| sample_id | Underlying sample identity | String |
| device_id and module_id | Instrument and interchangeable element identity | String |
| batch_id | Manufacturing or experimental grouping, explicitly defined | String |
| time_monotonic_s | Acquisition time for ordering and intervals | Float, seconds |
| time_utc | Optional wall-clock time for cross-system provenance | Timestamp with timezone |
| channel_id | Physical measurement channel | String |
| measured_quantity | Current, potential, impedance component, or other observable | Controlled vocabulary |
| value and unit | Measured numeric value and unit | Float and string |
| environmental_context | Temperature, humidity, pressure, flow, and their units | Structured fields |
| reference_value | Independently established target/reference result | Value plus method |
| reference_uncertainty | Uncertainty and convention for the reference | Value plus definition |
| quality_status | Valid, clipped, missing, unstable, fault, or other defined state | Enumeration |
| calibration_id and model_id | Versions used to interpret the record | String |
| split_group | Grouping relevant to a predeclared validation design | String |

Do not put personal health information into an educational dataset by default. If a clinical study is genuinely part of the project, its consent, governance, access, and retention practices require a separate institutionally approved plan.

<a id="section-partition-before-processing"></a>

## Partition before processing

Decide what “new” means in the intended application. For a new instrument, hold out instruments. For future operation, hold out later periods. For a new hospital, hold out sites. For repeated measurements from a person or sample, keep that entity on one side of the partition.

Fit scaling, imputation, baseline selection rules, feature selection, model parameters, and decision thresholds using only the permitted development data. Preserve a final independent evaluation. A normalization computed over the whole dataset can leak information even when the classifier never directly sees test labels.

Use a manifest table in a Markdown report to state the exact group membership and reason for each split. When the dataset is too small to support the intended evaluation, describe that limit instead of presenting an optimistic random split as field evidence.

<a id="section-reproducibility-record"></a>

## Reproducibility record

For every result, retain:

- Source URL or identifier and access date.
- Dataset version and a file hash if a download is authorized.
- Current license or terms, plus unresolved restrictions.
- Data dictionary, exclusions, unit conversions, and missing-data treatment.
- Development and evaluation partitions.
- Exact code, dependency versions, parameters, and random seeds.
- Baseline results, uncertainty intervals, failed cases, and interpretation limits.

The lab examples are self-contained enough to reproduce without downloading data. Optional external-data projects should keep their downloaded data outside the published course unless redistribution rights and sensitivity have been reviewed.

<a id="section-data-quality-exercises"></a>

## Data-quality exercises

**Unit collision.** Combine a hypothetical channel in nA with one in A. Show how a naive distance classifier is dominated by numerical scale, and explain why scaling must be learned within the training partition.

**Acquisition confounding.** Assign each class to a different day and add an unrelated day-specific offset. Compare a random row split with a held-out day. Explain which result answers the intended deployment question.

**Reference uncertainty.** Perturb nominal concentrations within a known uncertainty distribution. Determine whether the model is resolving differences smaller than the reference permits. An overprecise model output cannot create a more accurate reference.

**Unknown mixture.** Train on isolated substances and evaluate mixtures. Compare forced classification with a declared unknown state. Explain why the appropriate behavior depends on the intended use.

[Continue to machine learning](../modules/15-machine-learning-and-domain-shift.md) · [Open drift lab](../labs/06-drift-and-validation.md)

<!-- course-footer:start -->
---

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
