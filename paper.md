---
title: 'Meta-Mar: An AI-Integrated Web Platform for Meta-Analysis'
tags:
  - R
  - Shiny
  - meta-analysis
  - systematic review
  - research synthesis
  - AI assistant
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

Meta-Mar is a free, web-based meta-analysis platform built with R Shiny that enables researchers to conduct comprehensive meta-analyses without programming knowledge or software installation. The platform uniquely integrates an AI assistant powered by GPT-4 to provide context-aware methodological guidance and result interpretation. Available at https://www.meta-mar.com, Meta-Mar has been used by over 5,800 researchers across 120+ countries and cited in 320+ peer-reviewed publications since its launch in 2020 [@Beheshti2020].

# Statement of Need

Meta-analysis is essential for evidence synthesis across scientific disciplines [@Gurevitch2018], yet existing tools present significant barriers to researchers. Commercial software such as Comprehensive Meta-Analysis requires expensive licenses. Open-source alternatives like the R packages `metafor` [@Viechtbauer2010] and `meta` [@Balduzzi2019] require programming expertise. Existing web-based tools often lack comprehensive statistical options or provide limited methodological guidance for users unfamiliar with meta-analytic procedures.

Meta-Mar addresses this gap by providing:

- **Accessibility:** Browser-based interface requiring no installation, registration, or payment
- **Comprehensive statistics:** Support for continuous, binary, and correlation outcomes with multiple effect size measures
- **Multiple estimators:** Eight heterogeneity variance estimators (REML, DL, PM, ML, EB, SJ, HE, HS) and small-sample corrections (Hartung-Knapp, Kenward-Roger)
- **Publication bias tools:** Funnel plots, Egger's test [@Egger1997], Begg's test, trim-and-fill [@DuvalTweedie2000], and fail-safe N methods
- **AI-powered guidance:** Context-aware interpretation and methodological recommendations
- **Privacy-focused design:** No data retention; all uploads deleted after session ends [@Gilbert2025]

# Functionality

Meta-Mar supports the complete meta-analysis workflow through an interactive web interface:

1. **Data input:** CSV upload or manual entry for continuous outcomes, binary outcomes, correlations, or pre-calculated effect sizes (generic inverse variance)
2. **Model specification:** Fixed-effect or random-effects models with user-selected heterogeneity estimators and confidence interval methods
3. **Effect size calculation:** Automatic computation of standardized mean difference (SMD), mean difference (MD), odds ratio (OR), risk ratio (RR), risk difference (RD), or correlation coefficients with Fisher's z transformation
4. **Heterogeneity assessment:** Q-statistic, I², τ², H², and prediction intervals [@Higgins2003; @Holzmeister2024]
5. **Publication bias analysis:** Visual assessment via funnel plots, statistical tests (Egger's regression, Begg's rank correlation), adjustment methods (trim-and-fill), and sensitivity analysis (Rosenthal, Orwin, and Rosenberg fail-safe N)
6. **Moderator analysis:** Subgroup analysis for categorical moderators and meta-regression for continuous moderators
7. **Visualization:** Forest plots, funnel plots, bubble plots, Baujat plots, drapery plots, and radial plots
8. **AI interpretation:** GPT-4-powered assistant providing methodological guidance and result interpretation

The statistical engine is built on the `metafor` [@Viechtbauer2010] and `meta` [@Balduzzi2019] R packages, ensuring computational accuracy. Validation against Cochrane RevMan 5.4 confirms agreement to four decimal places for effect estimates, confidence intervals, and heterogeneity statistics.

# AI Integration

Meta-Mar integrates OpenAI's GPT-4 API as an optional AI assistant that provides:

- Interpretation of effect sizes and confidence intervals in context
- Explanation of heterogeneity statistics and their implications
- Guidance on model selection and analytical decisions
- Publication bias interpretation and recommendations

The AI assistant is designed to support, not replace, researcher judgment. All AI outputs are clearly labeled, and users retain full control over analytical decisions.

**AI Usage Disclosure:** The AI assistant is an optional feature. During development, AI tools (GitHub Copilot, Claude) assisted with code development; all outputs were reviewed and validated by the authors. Core statistical implementations rely entirely on the peer-reviewed `metafor` and `meta` R packages.

# Acknowledgements

Development of Meta-Mar was supported by Philipps-Universität Marburg, Department of Psychology. We thank the research community for feedback and feature suggestions that have shaped the platform's development.

# References
