---
layout: default
title: 'References · Systems and validation'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](../index.md) · [Start](../getting-started.md) · [Modules](../modules/index.md) · [Labs](../labs/index.md) · [Projects](../projects/index.md) · [**Library**](index.md) · [Site map](../navigation.md)

[Course home](../index.md) / [Library](index.md) / References · Systems and validation

<!-- course-navigation:end -->

# References · Systems and validation

<!-- course-toc:start -->
<details markdown="1">
<summary>On this page</summary>

- [Sampling and fluid mechanics](#section-sampling-and-fluid-mechanics)
- [Water and sample conditioning](#section-water-and-sample-conditioning)
- [Storage and materials](#section-storage-and-materials)
- [Electronics and instrumentation](#section-electronics-and-instrumentation)
- [Calibration and metrology](#section-calibration-and-metrology)
- [Physiology, clinical evaluation, and ethics](#section-physiology-clinical-evaluation-and-ethics)
- [A reading sequence](#section-a-reading-sequence)

</details>
<!-- course-toc:end -->

These sources support [modules 07–12](../modules/07-sampling-and-fluidics.md). They combine original studies, official technical documentation, measurement guidance, and foundational educational material. Source pages and bibliographic metadata were checked on **22 November 2026**. The notes distinguish what was accessible from what would require deeper examination. Links to a paper do not imply that its complete method has been independently reproduced.

The worked numerical examples in the lessons are original teaching examples with explicitly hypothetical parameters. They are not measurements from these publications. Do not transfer a reported recovery, accuracy, or electronic specification to a different material, instrument, or population without relevant evidence.

<a id="section-sampling-and-fluid-mechanics"></a>

## Sampling and fluid mechanics

**S01 · NASA Glenn Research Center. “Reynolds Number.”** Official educational resource; undated page. [Read the explanation](https://www.grc.nasa.gov/www/k-12/airplane/reynolds.html). **Use:** dimensionless comparison of inertial and viscous effects. **Limit:** general scaling does not determine transition or mixing in every geometry. **Access basis:** official page content. **Course connection:** module 07; derive the relevant characteristic length before calculating a number.

**S02 · Ling, S. J., Sanny, J., and Moebs, W. *University Physics, Volume 1*, section 14.7, “Viscosity and Turbulence.” OpenStax (2016).** [Read the chapter](https://openstax.org/books/university-physics-volume-1/pages/14-7-viscosity-and-turbulence). **Use:** an accessible derivation-oriented introduction to viscous pipe flow. **Limit:** the simplified equations require appropriate geometry and flow assumptions. **Access basis:** publisher's educational page. **Course connection:** module 07; identify where a proposed inlet violates the ideal tube model.

**S03 · Horváth, I., Barnes, P. J., Loukides, S., et al. “A European Respiratory Society technical standard: exhaled biomarkers in lung disease.” *European Respiratory Journal* 49, 1600965 (2017).** DOI: [10.1183/13993003.00965-2016](https://doi.org/10.1183/13993003.00965-2016); [PubMed record](https://pubmed.ncbi.nlm.nih.gov/28446552/). **Use:** professional guidance on collection, analysis, and reporting. **Limit:** technical standardization is distinct from evidence for an individual diagnostic application. **Access basis:** abstract, society-indexed document, and bibliographic record. **Course connection:** modules 07, 08, and 12.

**S04 · United States Environmental Protection Agency. *Method TO-15A: Determination of Volatile Organic Compounds (VOCs) in Air Collected in Specially Prepared Canisters and Analyzed by Gas Chromatography–Mass Spectrometry (GC–MS)* (September 2019).** [Official method collection](https://www.epa.gov/amtic/compendium-methods-determination-toxic-organic-compounds-ambient-air); [official text record](https://nepis.epa.gov/Exe/ZyPURL.cgi?Dockey=P100YDPO.txt). **Use:** a mature example of linking sampling, container quality, calibration, and analytical control. **Limit:** it is a specified canister/GC–MS method, not a certification route for an unrelated electrochemical system. **Access basis:** official method listing and indexed method text. **Course connection:** modules 07–09.

<a id="section-water-and-sample-conditioning"></a>

## Water and sample conditioning

**S05 · National Institute of Standards and Technology. *NIST Chemistry WebBook*, water phase-change data and Antoine correlations.** [Read the water entry](https://webbook.nist.gov/cgi/cbook.cgi?ID=C7732185&Mask=4&Type=ANTOINE&Plot=on). **Use:** vapor-pressure data with explicit correlation ranges. **Limit:** select compatible units and a valid temperature interval; a saturation relation alone does not predict dynamic condensation. **Access basis:** official database entry. **Course connection:** module 08.

**S06 · Lee, S.-W., Dinh, T.-V., Park, S.-Y., et al. “Development of a Moisture Pretreatment Device for the Accurate Quantitation of Water-Soluble Volatile Organic Compounds in Air.” *Chemosensors* 11(3), 188 (2023).** DOI: [10.3390/chemosensors11030188](https://doi.org/10.3390/chemosensors11030188). **Use:** original comparison showing why moisture treatment must be evaluated alongside compound recovery. **Limit:** results are conditional on the tested devices, compounds, flows, and analytical methods. **Access basis:** publisher metadata and abstract; no unverified details from inaccessible sections are asserted in the lessons. **Course connection:** module 08; design a follow-up experiment rather than treating one ranking as universal.

<a id="section-storage-and-materials"></a>

## Storage and materials

**S07 · Beauchamp, J., Herbig, J., Gutmann, R., and Hansel, A. “On the use of Tedlar® bags for breath-gas sampling and analysis.” *Journal of Breath Research* 2(4), 046001 (2008).** DOI: [10.1088/1752-7155/2/4/046001](https://doi.org/10.1088/1752-7155/2/4/046001); [PubMed record](https://pubmed.ncbi.nlm.nih.gov/21386188/). **Use:** original storage observations relevant to VOC and humidity changes. **Limit:** its conditions do not establish a universal holding time. **Access basis:** publication metadata and abstract. **Course connection:** modules 07–09.

**S08 · Mochalski, P., King, J., Unterkofler, K., and Amann, A. “Stability of selected volatile breath constituents in Tedlar, Kynar and Flexfilm sampling bags.” *Analyst* 138, 1405–1418 (2013).** DOI: [10.1039/C2AN36193K](https://doi.org/10.1039/C2AN36193K). **Use:** original comparison of storage behavior across materials and compounds. **Limit:** tested conditions and fill fractions must accompany any performance comparison. **Access basis:** indexed author-manuscript metadata and abstract. **Course connection:** module 09; distinguish leakage, chemical loss, and background.

<a id="section-electronics-and-instrumentation"></a>

## Electronics and instrumentation

**S09 · Texas Instruments. *LMP91000 Sensor AFE System: Configurable AFE Potentiostat for Low-Power Chemical-Sensing Applications*. Datasheet SNAS506I, revision I (December 2014).** [Read the datasheet](https://www.ti.com/lit/ds/symlink/lmp91000.pdf). **Use:** manufacturer specifications and an example integrated AFE architecture. **Limit:** datasheet performance depends on stated conditions and does not establish chemical specificity. **Access basis:** official datasheet and product description. **Course connection:** module 10. Check the revision before designing hardware.

**S10 · Analog Devices. *AD5940/AD5941: High Precision, Impedance, and Electrochemical Front End*.** [Product page and current datasheet](https://www.analog.com/en/products/ad5940.html). The documentation page listed revision G dated 9 February 2026 when checked. **Use:** integrated excitation and measurement architecture. **Limit:** performance must be checked for the selected load, frequency, and configuration. **Access basis:** official product and documentation listing. **Course connection:** module 10; read conditions attached to every numerical specification.

**S11 · Analog Devices. “AN-1563: Optimizing the AD5940 for Electrochemical Measurements” (2019).** [Read the application note](https://www.analog.com/en/resources/app-notes/an-1563.html). **Use:** device-specific implementation of electrochemical measurements and electrical calibration. **Limit:** electrical-path calibration does not validate a chemical mechanism. **Access basis:** official application note. **Course connection:** module 10.

**S12 · Analog Devices. “Transimpedance Amplifier Noise Considerations” (18 February 2015).** [Read the technical article](https://www.analog.com/en/resources/technical-articles/transimpedance-amplifier-noise-considerations.html). **Use:** relationships among amplifier noise, feedback resistance, capacitance, and bandwidth. **Limit:** examples address particular amplifiers; the course's numerical budget uses independently chosen teaching values. **Access basis:** official article text. **Course connection:** module 10.

<a id="section-calibration-and-metrology"></a>

## Calibration and metrology

**S13 · NIST/SEMATECH. *e-Handbook of Statistical Methods*, section 2.3.6.5, “Data analysis and model validation.”** [Read the calibration guidance](https://www.itl.nist.gov/div898/handbook/mpc/section3/mpc365.htm). **Use:** model and residual assessment for calibration. **Limit:** an example statistical fit does not cover every sampling or chemical error. **Access basis:** official handbook page. **Course connection:** module 11.

**S14 · NIST/SEMATECH. *e-Handbook of Statistical Methods*, section 2.3.6.7.3, “Comparison of check standard analysis and propagation of error.”** [Read the discussion](https://www.itl.nist.gov/div898/handbook/mpc/section3/mpc3673.htm). **Use:** relate empirical check-standard behavior to propagated uncertainty. **Limit:** independence and model assumptions require review in each application. **Access basis:** official handbook page. **Course connection:** module 11.

**S15 · Eurachem. *The Fitness for Purpose of Analytical Methods: A Laboratory Guide to Method Validation and Related Topics*, third edition (2025).** [Read the guide](https://www.eurachem.org/images/stories/Guides/pdf/MV_guide_3rd_ed_V1_EN.pdf); [publication announcement](https://www.eurachem.org/index.php/news/newsarts/542-nws-ffp2025). **Use:** professional validation and verification framework. **Limit:** intended use determines appropriate performance requirements; citing the guide does not validate an instrument. **Access basis:** official guide and edition announcement. **Course connection:** module 11.

**S16 · Joint Committee for Guides in Metrology. *Evaluation of measurement data—Guide to the expression of uncertainty in measurement*, JCGM 100:2008, with the 2026 amendment listed in the current GUM suite.** [Official publications and current documents](https://www.bipm.org/en/committees/jc/jcgm/publications); [base-document DOI](https://doi.org/10.59161/JCGM100-2008E). **Use:** uncertainty concepts and propagation framework. **Limit:** nonlinear models and unusual distributions can need methods beyond the first-order examples. **Access basis:** official publication listing and base-document record. **Course connection:** modules 09 and 11. Consult the current suite rather than describing the unamended 2008 text as the latest complete guidance.

**S17 · International Union of Pure and Applied Chemistry. “Limit of detection.” *Compendium of Chemical Terminology*, fifth edition (2025), entry L03540.** [Read the term](https://goldbook.iupac.org/terms/view/L03540). **Use:** detection-limit terminology. **Limit:** a numerical limit requires a stated measurement model and statistical criterion. **Access basis:** official terminology entry. **Course connection:** module 11.

<a id="section-physiology-clinical-evaluation-and-ethics"></a>

## Physiology, clinical evaluation, and ethics

**S18 · Unterkofler, K., King, J., Mochalski, P., et al. “Modeling-based determination of physiological parameters of systemic VOCs by breath gas analysis: a pilot study.” *Journal of Breath Research* 9(3), 036002 (2015).** DOI: [10.1088/1752-7155/9/3/036002](https://doi.org/10.1088/1752-7155/9/3/036002); [open manuscript](https://pmc.ncbi.nlm.nih.gov/articles/PMC4909147/). **Use:** a mechanistic example incorporating inhaled VOC concentration. **Limit:** the physiological and chemical assumptions limit generalization. **Access basis:** manuscript abstract and model-assumption sections. **Course connection:** module 12.

**S19 · Bossuyt, P. M., Reitsma, J. B., Bruns, D. E., et al. “STARD 2015: an updated list of essential items for reporting diagnostic accuracy studies.” *BMJ* 351, h5527 (2015).** DOI: [10.1136/bmj.h5527](https://doi.org/10.1136/bmj.h5527); [open article](https://pmc.ncbi.nlm.nih.gov/articles/PMC4623764/). **Use:** transparent reporting of diagnostic-accuracy studies. **Limit:** reporting completeness is distinct from study validity. **Access basis:** open article. **Course connection:** module 12.

**S20 · Collins, G. S., Moons, K. G. M., Dhiman, P., et al. “TRIPOD+AI statement: updated guidance for reporting clinical prediction models that use regression or machine learning methods.” *BMJ* 385, e078378 (2024).** DOI: [10.1136/bmj-2023-078378](https://doi.org/10.1136/bmj-2023-078378); [open article](https://pmc.ncbi.nlm.nih.gov/articles/PMC11019967/). **Use:** prediction-model reporting across regression and machine learning. **Limit:** a reporting guideline is not a performance guarantee. **Access basis:** primary publication metadata and accessible article record. **Course connection:** module 12.

**S21 · Lee, M.-R., Kao, M.-H., Hsieh, Y.-C., et al. “Cross-site validation of lung cancer diagnosis by electronic nose with deep learning: a multicenter prospective study.” *Respiratory Research* 25, 203 (2024).** DOI: [10.1186/s12931-024-02840-z](https://doi.org/10.1186/s12931-024-02840-z); [PubMed record](https://pubmed.ncbi.nlm.nih.gov/38730430/). **Use:** original evidence of the difficulty of transferring an electronic-nose model across sites. **Limit:** distinguish augmentation, adaptation, and independent evaluation; results are not transferable specifications for another sensor. **Access basis:** publication abstract and bibliographic record. **Course connection:** module 12.

**S22 · Buma, A. I. G., Muntinghe-Wagenaar, M. B., van der Noort, V., et al. “Lung cancer detection by electronic nose analysis of exhaled breath: a multicentre prospective external validation study.” *Annals of Oncology* 36(7), 786–795 (2025).** DOI: [10.1016/j.annonc.2025.03.013](https://doi.org/10.1016/j.annonc.2025.03.013); [PubMed record](https://pubmed.ncbi.nlm.nih.gov/40174676/). **Use:** prospective external evaluation in a defined outpatient setting. **Limit:** referral-population results do not establish population-screening utility. **Access basis:** abstract and bibliographic record, with an author-hosted manuscript located for further reading. **Course connection:** module 12.

**S23 · World Medical Association. *Declaration of Helsinki—Ethical Principles for Medical Research Involving Human Participants*, revised October 2024.** [Read the official declaration](https://www.wma.net/policies-post/wma-declaration-of-helsinki/). **Use:** a primary research-ethics framework. **Limit:** local institutional and jurisdictional requirements still need appropriate review; the declaration is not permission to conduct a study. **Access basis:** official current declaration. **Course connection:** module 12.

<a id="section-a-reading-sequence"></a>

## A reading sequence

Start with S01–S02 for flow reasoning, S05 for humidity calculations, and S07–S08 for the practical consequences of storage. Then read an AFE datasheet beside the module 10 error budget. Use S13–S17 to revise that budget into a complete measurement model. Finally, compare S21 and S22 using the questions in module 12 and the reporting frameworks S19–S20. This sequence connects physical design choices to the evidence needed to interpret the finished system.

<!-- course-footer:start -->
---

[Back to top](#page-top) · [Site map](../navigation.md) · [Course home](../index.md)
<!-- course-footer:end -->
