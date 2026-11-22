---
layout: default
title: 'Glossary across chemistry, electronics, and inference'
---

<a id="page-top"></a>

<!-- course-navigation:start -->
[Home](index.md) · [Start](getting-started.md) · [Modules](modules/index.md) · [Labs](labs/index.md) · [Projects](projects/index.md) · [Library](references/index.md) · [Site map](navigation.md)

[Course home](index.md) / Glossary across chemistry, electronics, and inference

<!-- course-navigation:end -->

# Glossary across chemistry, electronics, and inference

These are teaching definitions. They describe how terms are used in this course; formal terminology should be checked against the cited technical source when writing a specification. For chemical terminology, use the [IUPAC Gold Book](https://goldbook.iupac.org/). For measurement terminology, use the [JCGM VIM](https://jcgm.bipm.org/vim/en/).

| Term | Working meaning and common confusion |
| --- | --- |
| Activity | Effective thermodynamic abundance relative to a standard state. It is dimensionless and is not always numerically equal to concentration. |
| Adsorption | Accumulation at an interface. Distinguish from absorption into a bulk phase. |
| Aerosol | Particles or droplets suspended in a gas. A dissolved molecule, vapor molecule, and aerosol-borne molecule can follow different sample paths. |
| Aliasing | High-frequency variation represented incorrectly after sampling. Digital filtering after sampling cannot undo arbitrary aliasing. |
| Analyte | The substance or constituent being investigated. A sensor's response may also include interferents. |
| Array | Multiple sensing channels considered together. Channel count is not the same as independent information count. |
| Baseline | A reference signal state used for comparison. Its definition may be a blank, a pre-exposure interval, or a fitted trend. |
| Bias | In measurement, a systematic displacement; in electronics, an imposed operating level; in statistics, a property of an estimator or sampling process. State which meaning applies. |
| Biomarker | A measured characteristic associated with a biological process or condition. An association does not guarantee a specific diagnosis. |
| Blank | A measurement intended to represent the analytical procedure without the target contribution. A zero entered into a computer is not a procedural blank. |
| Calibration | Establishing a relationship between indications and reference values under specified conditions. It is distinct from adjusting the instrument. |
| Calibration transfer | Maintaining an inference relationship across devices, batches, or conditions. Transfer requires evidence on the receiving domain. |
| Capacitance | Change in stored charge per change in potential under stated conditions. Interfacial capacitance may vary with potential, frequency, composition, and history. |
| Charge-transfer resistance | A small-signal parameter describing a local current-potential slope within an electrochemical model. It is not a unique identifier of a molecule. |
| Chemoresistor | A material whose electrical resistance changes with chemical environment. It need not be an electrochemical cell with a liquid electrolyte. |
| Common-mode error | A disturbance shared across channels. Averaging or voting does not remove it automatically. |
| Concentration | A quantity of substance relative to a quantity of mixture. Specify whether the basis is amount, mass, or volume. |
| Confounder | A variable linked to both a measured predictor and an outcome, creating an alternative explanation for association. |
| Counter electrode | Electrode carrying the balancing current in a three-electrode measurement. Distinct from the reference electrode. |
| Cross-sensitivity | Response to substances or conditions other than the intended target. It can be a liability for a single channel and useful diversity in an array. |
| Dead volume | Sample-containing volume that contributes delay, mixing, or retained material without serving the intended measurement. |
| Desiccant | A material used to remove moisture. It may also change target recovery or introduce contaminants. |
| Diffusion | Molecular transport arising from random motion and chemical-potential gradients. Simple Fickian models are approximations of this behavior. |
| Domain shift | A change in the data-generating conditions between model development and use. Time, hardware, humidity, and population can all define domains. |
| Double layer | Interfacial charge organization near an electrode. Its structure depends on the electrolyte and operating conditions. |
| Drift | Time-dependent change in the instrument or its response relationship. It can affect offsets, gains, selectivity, kinetics, or noise. |
| Electrochemical window | An operationally defined potential interval over which unwanted decomposition is acceptably small under a specified test. It is not an unconditional material constant. |
| Electrode potential | Potential assigned relative to a reference convention. “One volt” is incomplete without the relevant reference and measurement context. |
| Electrolyte | Medium providing ionic conduction. Conduction does not itself demonstrate analyte recognition. |
| Equivalent circuit | Electrical model matching aspects of a response. More than one circuit or mechanism can explain a finite dataset. |
| Faradaic current | Current associated with electron-transfer reactions across an interface. Total measured current can include capacitive and parasitic contributions. |
| Feature | A representation derived from a measurement for inference. Feature extraction must be fitted or chosen without contaminating test data. |
| Fouling | Accumulation or reaction of material that changes a sensing surface's behavior. It can alter kinetics and transport together. |
| Ground truth | Informal name for reference labels or values. In engineering, their provenance and uncertainty must still be stated. |
| Headspace | Gas region above or around a sample. Its composition depends on equilibrium, kinetics, geometry, and history. |
| Henry coefficient | A gas-liquid partition parameter with several conventions. Always state numerator, denominator, units, solvent, and temperature. |
| Hysteresis | Dependence of response on the path by which a state was reached. An increasing-concentration calibration may not describe recovery. |
| Identifiability | Whether observations can distinguish the parameters or mechanisms in a model. Excellent fitting cannot fix nonidentifiability. |
| Impedance | Complex voltage-to-current ratio for a specified perturbation and operating state. The usual linear interpretation requires small-signal and stationarity conditions. |
| Interferent | Substance or condition affecting the measurement of the intended target. Effects can be additive, competitive, or nonlinear. |
| Ionic liquid | A salt that is liquid over a relevant temperature range. The room-temperature subset is often abbreviated RTIL. |
| Limit of detection | A procedure-specific detection threshold defined with a statistical convention. It differs from a single visually noticeable response. |
| Limit of quantification | A level at which a method meets defined quantitative performance criteria. A universal fixed multiplier is inadequate without context. |
| Measurand | The quantity intended to be measured, including the conditions needed to define it. |
| Non-Faradaic response | Electrical behavior without net interfacial electron-transfer reaction in the idealized description, often involving charging or polarization. |
| Open-set recognition | Inference that allows a sample to fall outside known classes. A closed-set classifier always choosing a label does not identify every molecule. |
| Overpotential | Electrode potential departure from the equilibrium value for a specified reaction. |
| Partition coefficient | Ratio describing equilibrium distribution between phases under a defined convention. It does not by itself describe transfer rate. |
| Permeation | Passage through a material, often involving sorption and diffusion. It differs from leakage through an opening. |
| Potentiostat | Feedback instrument controlling an electrode potential relative to a reference while measuring or supporting current flow. |
| Precision | Closeness among repeated measurements under specified conditions. High precision can coexist with systematic error. |
| Reference electrode | Electrode intended to provide a stable comparison potential while carrying negligible measurement current. |
| Recovery | Fraction of a target contribution retained through an analytical process, defined relative to a specified reference. |
| Repeatability | Precision under closely held conditions. It is narrower than reproducibility across laboratories or devices. |
| Selectivity | Ability to determine a target in the presence of other contributions under defined conditions. It requires an interference context. |
| Sensitivity | In calibration, slope of response versus quantity; in classification, true-positive rate. Always identify the intended meaning. |
| Specificity | In diagnostic classification, true-negative rate. Chemical usage sometimes differs; prefer an explicit definition. |
| Standard uncertainty | Uncertainty expressed as a standard deviation. It is not the same quantity as maximum error. |
| Stationarity | Statistical or physical properties remaining sufficiently stable over a measurement interval for the chosen analysis. |
| Transimpedance amplifier | Circuit converting input current to output voltage with a gain expressed in ohms. |
| Validation | Evidence that a method meets requirements for its intended use. A correct code implementation is only one component. |
| VOC | Volatile organic compound. The boundaries can depend on scientific or regulatory context; not all gases or biomarkers are VOCs. |
| Working electrode | Electrode at which the process of primary analytical interest is investigated. |

[Return to the curriculum](curriculum.md)

<!-- course-footer:start -->
---

[Back to top](#page-top) · [Site map](navigation.md) · [Course home](index.md)
<!-- course-footer:end -->
