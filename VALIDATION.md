# Validation record

Checked on **22 November 2026**. This record describes the delivered Markdown curriculum and its computational examples. It does not report physical-device validation, clinical validation, legal clearance, a GitHub Pages deployment, or website access testing.

## Content and structure

The release contains 53 newly authored Markdown files, including 49 learner-facing files under `docs/`. The complete package is approximately 77,000 whitespace-delimited words, including code, tables, bibliography, navigation, and maintainer guidance. It includes 18 modules, eight labs, an integrated executable example, a design studio, a physical build ladder, nine derivative-project proposals, assessments and solutions, a glossary, mathematics reference, and teaching/publication guidance.

All learner-facing pages have valid frontmatter, a title, and the default layout declaration. Markdown code fences and table row widths were checked. Relative file links were checked for target existence and for remaining within the learner-facing publication directory. Navigation reachability was checked from the course home. All 49 learner pages have a shared menu and return links. Modules and labs have position counts and previous/next navigation; new module and project hubs and a complete site map support browsing. Forty-seven longer pages have collapsible contents lists with explicit section anchors.

All curriculum and maintainer documents are `.md` files. Four theme support files add Jekyll configuration, a Sass stylesheet, and header/footer includes. There are no bundled datasets, copied third-party figures, generated website assets, or deployment credentials in the delivered source. The publishing workflow uses the standard GitHub Pages Markdown/Jekyll route documented in [PUBLISHING.md](PUBLISHING.md).

## Local website rendering and navigation

Two local Jekyll builds succeeded: one with a project path prefix (`/sensor-course`) and one at the domain root. Each produced 49 HTML pages. A rendered-output check passed all 1,834 internal link occurrences, including fragment targets, without missing files, duplicate IDs, unconverted Markdown destinations, or paths escaping the configured site prefix. All 47 contents lists and 49 header menus rendered as native collapsible elements.

The latest theme preview at the available narrow viewport verified the home page, keyboard-operated header menu, sidebar navigation to the lab directory, keyboard navigation to a lab, a contents toggle and section jump, and dark syntax highlighting. Text, menus, code, and the inspected tables remained readable. An earlier navigation pass also checked the module directory, next-lesson links, and the project directory. All 49 rendered stylesheet references resolved in each URL configuration. This was a representative visual check, not an exhaustive browser, mobile-device, or accessibility audit.

The isolated temporary runtime used Jekyll 3.10.0, kramdown 2.4.0, GFM parser 1.1.0, relative-links 0.6.1, and Minima 2.5.1, matching the checked GitHub Pages core versions. The local SEO plugin was 2.8.0 rather than the listed 2.9.1, and live repository metadata was disabled. This establishes local content rendering and navigation, not an identical reproduction of the hosted service. Temporary build overrides, dependencies, and generated assets remained outside the delivered source directory; the published theme settings live in `docs/_config.yml`. [GitHub Pages dependency baseline](https://github.com/github/pages-gem/blob/master/lib/github-pages/dependencies.rb)

## Computational and scientific checks

Eight complete Python blocks were executed: labs 01–07 and the integrated example. All ran successfully and passed their included assertions. The design capstone is an assignment rather than executable code. Expected outputs in the drift and timing labs matched execution.

Independent numerical review covered concentration/amount conversions, electrode-kinetics examples, diffusion scales and transients, impedance, pipe pressure drop, analog gain/noise examples, uncertainty propagation, correlated-channel behavior, diagnostic predictive values, and selected system budgets. The review corrected a transimpedance label, revised the disturbance in the ill-conditioned-array example to match its interpretation, and added an explicit transduction bridge between subsystem models.

The integrated example verifies its quantization bound and rejects injected disconnection and clipping faults. Its physical coefficients are synthetic; these checks demonstrate behavior of the educational model only.

## Literature and editorial checks

The three main annotated bibliographies contain 71 entries, with overlap across subjects. Additional official and primary references support datasets, independent projects, and publication setup. Sources include selected 2024–2026 research and foundational work. Bibliographic identity and relevance were checked through public source pages; the annotations distinguish full or partial content access, metadata, and abstract-level evidence. Known corrections are linked where identified.

The curriculum records the inconsistent reuse wording on the UCI drift dataset pages and does not redistribute those data. No exhaustive literature search, complete source-method replication, or guarantee of permanent external-link availability is claimed. Publisher access restrictions may require an institutional subscription or an alternate author-hosted version for deeper reading.

Editorial review checked for identifiers and source cues excluded by the content brief, confidential product-specific settings, unsupported selectivity assertions, and unqualified legal-clearance statements. A second editorial pass generalized prescriptive combinations in design assignments and removed implementation-specific mechanism wording. Project work now starts from independently documented educational platforms, authorized commercial modules, or synthetic models; optional subsystems must be justified by a chosen question. The independent re-review found no actionable disclosure residuals within the reviewed material. Synthetic and measured results are distinguished. Derivative projects retain unassessed clearance status. These checks cannot establish the absence of overlap with all intellectual-property rights. A subsequent attribution audit checked all 57 delivered source files, including the 53 Markdown files and four theme files, plus all 49 rendered HTML pages for excluded personal names and source identifiers, titles, and URLs. None were present, so no academic-citation exception was needed.

## Verification limits

The Markdown was structurally parsed, rendered locally, and checked for internal navigation and executable-example behavior. The actual GitHub-hosted build and private-access behavior remain untested; those require the chosen publishing repository and hosting configuration. No external publication, repository creation, commit, or upload was performed.

When publishing, build the actual site, inspect representative rendered pages at the final URL, and verify access using authorized and unauthorized sessions. Repeat the relevant local link, layout, and code checks after changes. See [EDITORIAL.md](EDITORIAL.md) for maintenance and content boundaries.
