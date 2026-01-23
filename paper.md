---
title: 'Meta-Mar: An AI-Integrated Web Platform for Meta-Analysis'
tags:
  - R
  - Shiny
  - meta-analysis
  - systematic review
  - evidence synthesis
  - AI assistant
  - GPT-4
authors:
  - name: Ashkan Beheshti
    orcid: 0000-0002-6377-0710
    affiliation: "1, 2"
    corresponding: true
    email: a.beheshti@posteo.de
  - name: Hassan Sazmand
    affiliation: 2
  - name: Mira-Lynn Chavanon
    affiliation: 1
  - name: Hanna Christiansen
    affiliation: 1
affiliations:
  - name: Department of Psychology, Philipps-Universität Marburg, Germany
    index: 1
  - name: Independent Researcher
    index: 2
date: 23 January 2026
bibliography: paper.bib
---

# Summary

Meta-analysis is a cornerstone methodology in evidence-based research, enabling systematic synthesis of findings across multiple studies to produce more reliable and generalizable conclusions [@Borenstein2021; @Gurevitch2018]. Yet despite its central importance, existing tools for conducting meta-analyses remain fragmented—often technically demanding, costly, or lacking transparency—creating barriers for early-career researchers, educators, and interdisciplinary teams [@Harrer2021].

Meta-Mar addresses this challenge as a free, browser-based meta-analysis platform that combines statistical rigor with accessibility. Built with R Shiny and powered by the `metafor` [@Viechtbauer2010] and `meta` [@Balduzzi2019] packages, Meta-Mar v4.0.2 performs fixed-effect and random-effects meta-analyses across continuous, binary, correlation, and generic inverse-variance data structures. The platform integrates advanced heterogeneity diagnostics, publication bias assessments, and publication-quality visualizations within a guided, stepwise interface. Uniquely, Meta-Mar incorporates a large language model (LLM) assistant via GPT-4 that provides contextual guidance for model selection, data validation, and result interpretation—bridging the gap between statistical complexity and practical usability.

Available at https://www.meta-mar.com, Meta-Mar has been used by over 5,800 researchers across 120+ countries and cited in 200+ peer-reviewed publications since its initial release in 2020 [@Beheshti2020].

# Statement of Need

The current landscape of meta-analysis software presents a fundamental tension between methodological sophistication and day-to-day usability [@Fisher2022; @Harrer2021]. Commercial platforms such as Comprehensive Meta-Analysis (CMA) and Cochrane's RevMan offer comprehensive functionality but operate under subscription-based models (approximately €65–95 annually for students), creating financial barriers particularly for researchers in resource-limited settings. Open-source alternatives like the R packages `metafor` and `meta` provide robust analytical frameworks but require programming expertise that many researchers—especially those in applied fields such as health, education, and behavioral sciences—may lack.

Existing web-based tools have attempted to bridge this gap, but typically sacrifice either statistical comprehensiveness or methodological guidance. Platforms like metaHUN [@Umaroglu2018] provide web-based access to `metafor` functionality but lack features such as customizable pooling methods, prediction intervals, and interactive tutorials. Desktop applications like JASP [@Bartos2025] require installation, which can pose barriers in institutional computing environments.

Meta-Mar addresses these limitations by providing:

- **Zero-barrier accessibility:** Browser-based interface requiring no installation, registration, or payment
- **Comprehensive statistical coverage:** Support for continuous, binary, and correlation outcomes with multiple effect size measures (SMD, MD, OR, RR, RD, Fisher's z)
- **Methodological flexibility:** Eight heterogeneity variance estimators (REML, DL, PM, ML, EB, SJ, HE, HS) with small-sample corrections (Hartung-Knapp, Kenward-Roger)
- **Publication bias diagnostics:** Funnel plots, Egger's regression [@Egger1997], Begg's rank correlation, trim-and-fill adjustment [@DuvalTweedie2000], and fail-safe N calculations (Rosenthal, Orwin, Rosenberg)
- **AI-powered guidance:** Context-aware interpretation and methodological recommendations that serve as a dynamic tutor for users unfamiliar with meta-analytic conventions
- **Privacy-by-design:** GDPR-aligned data handling with no persistent storage; all uploads deleted after session ends

# Statistical Architecture

Meta-Mar implements the complete meta-analysis workflow through a modular architecture:

**Data Input and Effect Size Calculation.** The platform accepts CSV uploads or manual entry for four data structures: continuous outcomes (computing SMD, MD, or ratio of means), binary outcomes (OR, RR, RD with zero-event handling), correlations (Fisher's z transformation), and pre-calculated effect sizes (generic inverse variance). Input validation ensures data integrity before analysis.

**Model Specification.** Users select between fixed-effect models using inverse-variance weighting and random-effects models with user-specified τ² estimators. Confidence interval methods include classic Wald intervals, Hartung-Knapp-Sidik-Jonkman (HKSJ), and Kenward-Roger corrections for improved small-sample performance.

**Heterogeneity Assessment.** The platform computes Cochran's Q statistic, I², τ², H², and prediction intervals [@Higgins2003], enabling researchers to distinguish between true between-study heterogeneity and sampling variation.

**Publication Bias Analysis.** Visual assessment via funnel plots (including contour-enhanced variants) is complemented by Egger's regression test for small-study effects, Begg's rank correlation, trim-and-fill adjustment for estimating missing studies, and three fail-safe N methods for quantifying robustness.

**Moderator Analysis.** Subgroup analysis supports categorical moderators with between-group heterogeneity testing, while meta-regression accommodates continuous and categorical covariates with bubble plot visualization.

**Visualization.** Publication-quality outputs include forest plots (with subgroup comparisons), funnel plots, Galbraith (radial) plots, L'Abbé plots for binary outcomes, Baujat plots for identifying influential studies, and drapery plots for p-value functions.

**Validation.** Computational accuracy was validated against Cochrane RevMan 5.4, demonstrating agreement to four decimal places for effect size estimates, standard errors, confidence intervals, and study weights across standardized mean difference models.

# Design Rationale

The architectural decisions underlying Meta-Mar reflect deliberate trade-offs between statistical power, accessibility, and maintainability:

**Build vs. extend decision.** Rather than implementing meta-analytic algorithms from scratch, Meta-Mar wraps the established `metafor` and `meta` R packages. This choice prioritizes computational reliability over novelty—these packages have been peer-reviewed, widely cited, and validated across thousands of published meta-analyses. Our contribution lies in the accessibility layer and AI integration, not in reinventing statistical methods.

**Web-based vs. desktop architecture.** We chose R Shiny over desktop deployment (like JASP) to eliminate installation barriers. This enables immediate use in institutional environments with restricted software policies and supports the platform's educational mission in classroom settings where setup time is limited.

**AI as guidance, not automation.** The GPT-4 integration was designed as an interpretive assistant rather than an automated analyst. Statistical computations remain deterministic and reproducible through the underlying R packages; the AI layer provides explanatory support without modifying analytical outputs. This separation ensures that research conclusions depend on validated statistical methods, not on LLM outputs.

**Privacy-first data handling.** Session-based data storage with automatic deletion was chosen over persistent user accounts to minimize data governance complexity and align with GDPR principles. This trade-off sacrifices cross-session continuity for stronger privacy guarantees.

# AI Integration

Meta-Mar integrates OpenAI's GPT-4 API through LangChain to provide an optional AI assistant that enhances interpretability without modifying statistical computations. The assistant supports users with:

- Contextual interpretation of effect sizes, confidence intervals, and heterogeneity statistics
- Guidance on model selection based on data characteristics and research questions
- Explanation of publication bias diagnostics and their implications
- Interactive methodological tutoring for users new to meta-analysis

The integration employs conversation memory to maintain context across multi-turn interactions, custom prompt templates tailored to meta-analytic workflows, and error handling for invalid inputs or API timeouts. Critically, the AI assistant is designed to support—not replace—researcher judgment. All AI outputs are clearly labeled, statistical computations remain deterministic and reproducible, and users retain full control over analytical decisions.

**AI Usage Disclosure:** The AI assistant is an optional feature that users may enable or disable. During platform development, AI coding assistants were used as follows:

- **Tools used:** GitHub Copilot, Claude 3.5 Sonnet (Anthropic)
- **Scope of assistance:** Code refactoring, UI component scaffolding, documentation drafting, and test case generation
- **Where applied:** Shiny UI modules, API integration code, README and documentation text
- **Human oversight:** All AI-generated outputs were reviewed, edited, and validated by the authors. Core design decisions, statistical implementations, and architectural choices were made entirely by human authors.

Core statistical computations rely entirely on the peer-reviewed `metafor` and `meta` R packages without AI modification. The AI assistant feature within Meta-Mar uses the OpenAI GPT-4 API; this integration was designed and implemented by the authors with AI coding assistance for boilerplate code only.

# Privacy and Governance

Meta-Mar implements privacy-by-design principles aligned with GDPR requirements:

- No user registration required
- Uploaded data stored in session memory only
- Automatic deletion when session ends
- Automated anonymization of free-text inputs before AI processing
- TLS 1.3 encryption for all data transmission
- No persistent storage of user data or AI interactions

These safeguards ensure responsible deployment in academic and educational environments where data sensitivity is paramount.

# Development Practices and Community

Meta-Mar has been developed openly on GitHub since 2020, with a public commit history spanning six years of iterative refinement. The repository includes:

- **Documentation:** Comprehensive README, online user guide at meta-mar.com/documentation, and in-app tooltips
- **Issue tracking:** Public issue tracker for bug reports and feature requests
- **Contribution pathway:** Guidelines for community contributions via pull requests
- **Versioned releases:** Tagged releases with semantic versioning (current: v4.0.2)
- **Validation testing:** Computational outputs verified against Cochrane RevMan 5.4 benchmark data

The platform can be tested locally by cloning the repository and running `shiny::runApp()` in R with the required dependencies installed.

# Target Audience

Meta-Mar serves two complementary user groups: (1) researchers without programming expertise who require accessible tools for conducting methodologically sound meta-analyses, and (2) technically trained users who may lack formal training in meta-analytic methodology and benefit from AI-driven guidance on model selection and interpretation. The platform has been adopted in graduate-level meta-analysis courses, including PhD programs at Semmelweis University, demonstrating its utility as both a research and pedagogical tool.

# Acknowledgements

Development of Meta-Mar was supported by Philipps-Universität Marburg, Department of Psychology. We thank the research community for feedback and feature suggestions that have shaped the platform's evolution since 2020.

# References

