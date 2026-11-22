---
layout: default
title: 'References: arrays, olfaction, data, and systems'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [Modules](../modules/index.md) · [Labs](../labs/index.md) · [Projects](../projects/index.md) · [**Library**](index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Library](index.md) / References: arrays, olfaction, data, and systems

<!-- course-navigation:end -->

# References: arrays, olfaction, data, and systems

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Arrays and public chemical-sensor data](#section-arrays-and-public-chemical-sensor-data)
- [Biological and computational olfaction](#section-biological-and-computational-olfaction)
- [Selected 2024–2026 device research](#section-selected-20242026-device-research)
- [Signal processing and machine learning](#section-signal-processing-and-machine-learning)
- [System design, reference data, and responsible operation](#section-system-design-reference-data-and-responsible-operation)
- [How to maintain this reading map](#section-how-to-maintain-this-reading-map)

</details>
<!-- course-toc:end -->

This reading map supports Modules 13–18 and Labs 06–08. Sources were checked on **22 November 2026**. Primary studies support the specific observations described in the lessons; official documentation supports implementation and engineering process. Short annotations explain what each source is useful for and what it does not establish.

“Abstract-level” means metadata and an accessible primary abstract or publisher summary were checked, rather than a complete methods audit. “Documentation” means the official source was inspected. The curriculum's synthetic calculations and code are original teaching examples, not reproduced experimental results. Access restrictions and link behavior can change.

<a id="section-arrays-and-public-chemical-sensor-data"></a>

## Arrays and public chemical-sensor data

**O1. Fonollosa, J., Rodríguez-Luján, I., and Huerta, R. (2015). _Chemical gas sensor array dataset_. Data in Brief 3, 85–89.** [Primary article record](https://pubmed.ncbi.nlm.nih.gov/26217723/) · [DOI](https://doi.org/10.1016/j.dib.2015.01.003).

Use for the experimental provenance of a widely used drift benchmark. The measurements are from metal-oxide sensors; computational success on them does not validate electrochemical hardware. Access basis: primary abstract and author-manuscript search record.

**O2. Vergara, A. (2012). _Gas Sensor Array Drift Dataset_. UCI Machine Learning Repository.** [Dataset and metadata](https://archive.ics.uci.edu/dataset/224/gas+sensor+array+drift+dataset) · [DOI](https://doi.org/10.24432/C5RP6W).

Use for chronological evaluation and feature metadata. Access basis: repository documentation. The page contains conflicting reuse statements: a current CC BY 4.0 section and legacy research-only language. Resolve terms before redistribution or commercial reuse; no dataset is bundled here.

**O3. UCI Machine Learning Repository (donated 2013). _Gas Sensor Array Drift at Different Concentrations_.** [Repository record](https://archive.ics.uci.edu/dataset/270/gas+sensor+array+drift+dataset+at+different+concentrations).

Use when concentration labels are needed. Access basis: repository documentation. Preserve batch identities and distinguish supplied features from raw traces. Its reuse text has the same inconsistency noted above.

**O4. UCI Machine Learning Repository (donated 2014). _Gas sensor array under flow modulation_.** [Repository record](https://www.archive.ics.uci.edu/dataset/308/gas+sensor+array+under+flow+modulation).

Use for optional study of dynamic sampling and time-series features. The documented apparatus uses metal-oxide sensors; transfer to other transducers requires new evidence. Access basis: repository metadata and experimental description. Review current terms at the source.

**O5. Wang, C., Chen, Z., Chan, C. L. J., et al. (2024). _Biomimetic olfactory chips based on large-scale monolithically integrated nanotube sensor arrays_. Nature Electronics 7, 157–167.** [Primary paper](https://doi.org/10.1038/s41928-023-01107-7) · [Author correction, 2024](https://doi.org/10.1038/s41928-024-01246-5).

Use for array integration as a research direction. Access basis: publisher abstract, metadata, source-data descriptions, and correction notice metadata. The correction is linked for readers; this curriculum does not infer its content from the notice alone. Array size should not be equated with independent information dimensions.

<a id="section-biological-and-computational-olfaction"></a>

## Biological and computational olfaction

**O6. Malnic, B., Hirono, J., Sato, T., and Buck, L. B. (1999). _Combinatorial receptor codes for odors_. Cell 96, 713–723.** [Primary record and abstract](https://pubmed.ncbi.nlm.nih.gov/10089886/) · [DOI](https://doi.org/10.1016/S0092-8674(00)80581-4).

A foundational experimental study of overlapping receptor responses. Use for the coding principle, not as evidence that an engineered array reproduces human perception. Access basis: abstract-level.

**O7. Mainland, J. D., Li, Y. R., Zhou, T., Liu, W. L. L., and Matsunami, H. (2015). _Human olfactory receptor responses to odorants_. Scientific Data 2, 150002.** [Primary record](https://pubmed.ncbi.nlm.nih.gov/25977809/) · [DOI](https://doi.org/10.1038/sdata.2015.2).

An optional data-reading extension about receptor assays and concentration-dependent responses. Assay outputs are not direct airborne device calibrations. Access basis: metadata, abstract, and figure descriptions.

**O8. Billesbølle, C. B., et al. (2023). _Structural basis of odorant recognition by a human odorant receptor_. Nature.** [Primary record](https://pubmed.ncbi.nlm.nih.gov/36922591/).

Use to connect molecular structure to testable recognition hypotheses. Structure alone does not establish immobilized-device sensitivity or lifetime. Access basis: indexed primary abstract; a later direct fetch was incomplete, so detailed methods are not summarized here.

**O9. de March, C. A., Ma, N., Billesbølle, C. B., et al. (2024). _Engineered odorant receptors illuminate the basis of odour discrimination_. Nature 635, 499–508.** [Primary record](https://pubmed.ncbi.nlm.nih.gov/39478229/) · [DOI](https://doi.org/10.1038/s41586-024-08126-0).

Use for recent receptor-structure research and the distinction between engineered consensus receptors and native-device behavior. Access basis: primary abstract and publisher metadata, not a complete supplementary-methods audit.

**O10. Lee, B. K., Mayhew, E. J., Sanchez-Lengeling, B., et al. (2023). _A principal odor map unifies diverse tasks in olfactory perception_. Science 381, 999–1006.** [Primary record](https://pubmed.ncbi.nlm.nih.gov/37651511/) · [DOI](https://doi.org/10.1126/science.ade4401).

Use to distinguish structure-to-perception prediction from sensor-to-chemical inference. The study's prospective evaluation has a defined task and population; it does not validate all mixtures or arbitrary sensor signals. Access basis: primary abstract and accessible article excerpts.

**O11. Vergassola, M., Villermaux, E., and Shraiman, B. I. (2007). _“Infotaxis” as a strategy for searching without gradients_. Nature 445, 406–409.** [Primary paper](https://www.nature.com/articles/nature05464).

Use for information-seeking motion under intermittent cues. Conclusions depend on the transport and detection model; a robot requires its own validation. Access basis: publisher abstract and article descriptions.

**O27. Sato, K., Pellegrino, M., Nakagawa, T., Nakagawa, T., Vosshall, L. B., and Touhara, K. (2008). _Insect olfactory receptors are heteromeric ligand-gated ion channels_. Nature 452, 1002–1006.** [Primary paper](https://www.nature.com/articles/nature06850).

Use for the distinction between insect receptor ion-channel mechanisms and mammalian GPCR signaling. Access basis: publisher abstract and metadata. Biological receptor classes should not be treated as interchangeable sensor components.

<a id="section-selected-20242026-device-research"></a>

## Selected 2024–2026 device research

**O12. Yin, X., Zhang, H., Qiao, X., et al. (2024). _Artificial olfactory memory system based on conductive metal-organic frameworks_. Nature Communications 15, 8409.** [Primary record](https://pubmed.ncbi.nlm.nih.gov/39333101/) · [DOI](https://doi.org/10.1038/s41467-024-52567-0).

Use to discuss persistence as both a computational opportunity and a potential carryover problem. Access basis: primary abstract and publisher discussion excerpts. This is a particular material demonstration, not universal odor memory.

**O13. Lee, K., Jo, Y.-M., Sohn, M. S., et al. (2025). _Photoactivated conductive MOF thin film arrays on micro-LEDs for chemiresistive gas sensing_. Nature Communications 16, 9612.** [Primary paper](https://doi.org/10.1038/s41467-025-64602-9).

Use for controlled excitation and materials/electronics integration. Access basis: publisher abstract, article excerpts, and publication metadata. The sensing family is chemiresistive; results do not establish a different electrochemical interface's performance.

**O14. Liu, T., Li, X., He, H., et al. (2026). _Bioinspired triboelectric droplet sensor for ammonia monitoring_. Nature Communications 17, 2153.** [Primary record](https://pubmed.ncbi.nlm.nih.gov/41611736/) · [DOI](https://doi.org/10.1038/s41467-026-68974-4).

Use as a recent example of liquid-interface transduction. Access basis: primary abstract and metadata. Ammonia is inorganic; broad VOC detection and field generalization are separate questions.

**O15. Wang, W., Wang, Y., Lu, Z., Liu, Y., and Li, T. (2026). _On-chip integrated NDIR CO2 gas sensor_. Microsystems & Nanoengineering 12, 272.** [Primary record](https://pubmed.ncbi.nlm.nih.gov/42493497/) · [DOI](https://doi.org/10.1038/s41378-026-01388-w).

Use for comparing optical integration, gas exchange, and device layout. Access basis: primary abstract, publisher article excerpts, and metadata. Carbon dioxide is not a VOC; this is a complementary instrumentation example.

<a id="section-signal-processing-and-machine-learning"></a>

## Signal processing and machine learning

**O16. Guo, C., Pleiss, G., Sun, Y., and Weinberger, K. Q. (2017). _On Calibration of Modern Neural Networks_. Proceedings of ICML, PMLR 70, 1321–1330.** [Primary conference paper](https://proceedings.mlr.press/v70/guo17a.html).

Use for separating predictive confidence from accuracy. The source experiments concern other domains; chemical-sensor calibration and domain shift require independent evaluation. Access basis: official proceedings abstract and paper excerpts.

**O17. scikit-learn developers. _Cross-validation: evaluating estimator performance_.** [Official documentation](https://scikit-learn.org/stable/modules/cross_validation.html).

Use for implementing group-aware and temporal evaluation. Access basis: documentation. Correct splitter selection depends on the experimental unit and deployment question.

**O18. scikit-learn developers. _Common pitfalls and recommended practices_.** [Official documentation](https://scikit-learn.org/stable/common_pitfalls.html).

Use for preprocessing and leakage controls. Access basis: documentation. A correctly implemented pipeline cannot compensate for an unrepresentative dataset.

**O19. scikit-learn developers. _Novelty and Outlier Detection_.** [Official documentation](https://scikit-learn.org/stable/modules/outlier_detection.html).

Use for distinctions between training-set outliers and new observations outside a reference distribution. Access basis: documentation. Novelty is not chemical identity.

**O20. SciPy developers. _savgol_filter_.** [Official API documentation](https://docs.scipy.org/doc/scipy/reference/generated/scipy.signal.savgol_filter.html).

Use for local polynomial filtering, derivative settings, spacing, and edge behavior. Access basis: documentation. Inspect numerical effects on representative signals before deployment.

**O21. SciPy developers. _filtfilt_.** [Official API documentation](https://docs.scipy.org/doc/scipy/reference/generated/scipy.signal.filtfilt.html).

Use to understand forward-backward filtering. Access basis: documentation. Offline zero-phase processing is not a demonstration of causal response latency.

<a id="section-system-design-reference-data-and-responsible-operation"></a>

## System design, reference data, and responsible operation

**O22. NASA. _Systems Engineering Handbook_.** [Official handbook portal](https://www.nasa.gov/reference/systems-engineering-handbook/).

Use for requirements, interfaces, verification, and validation. Access basis: official handbook portal. Adapt its process to the scale of the project; it does not certify the design.

**O23. NIST. _AI Risk Management Framework_.** [Official framework](https://www.nist.gov/itl/ai-risk-management-framework).

Use to organize risks and evidence for learned components. Access basis: official documentation. It is a voluntary risk-management resource, not a sensor-performance approval.

**O24. NIST. _Privacy Framework_.** [Official framework](https://www.nist.gov/privacy-framework).

Use for mapping data-processing risks and making retention/access decisions. Access basis: official documentation. Project-specific obligations require separate assessment.

**O25. Fagan, M., Megas, K., Scarfone, K., and Smith, M. (2020). _IoT Device Cybersecurity Capability Core Baseline_. NIST IR 8259A.** [Official publication](https://csrc.nist.gov/pubs/ir/8259/a/final).

Use for device cybersecurity capability planning. Access basis: official publication metadata and abstract. Select controls for the actual device and deployment environment.

**O26. NIST. _Standard Reference Database 1A_.** [Official database description](https://www.nist.gov/srd/nist-standard-reference-database-1a).

Use as an example of curated mass-spectral reference information. Access basis: official database documentation. Reference-library matching requires appropriate analytical context and does not independently prove every identification.

<a id="section-how-to-maintain-this-reading-map"></a>

## How to maintain this reading map

Add a source only when it supports a specific teaching statement or experiment. Record whether the evidence was an abstract, full methods, source data, or independent replication. Check corrections and retractions at the publisher before reusing quantitative results. Preserve distinctions between simulation, laboratory demonstration, external validation, and operational evidence.

For a student literature update, search by physical question rather than by superlatives: sample recovery under humidity, calibration transfer across devices, causal latency, independent mixture validation, or receptor activity after immobilization. A useful update can identify a negative result, a missing control, or a better benchmark as readily as a new material.

<!-- course-footer:start -->
---

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
