# Meta-Mar

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![R](https://img.shields.io/badge/R-%3E%3D4.0-blue)](https://www.r-project.org/)
[![Shiny](https://img.shields.io/badge/Shiny-1.7+-green)](https://shiny.rstudio.com/)

A free, web-based meta-analysis platform built with R Shiny, integrating comprehensive statistical methods with AI-powered methodological guidance.

**Live Application:** [https://www.meta-mar.com](https://www.meta-mar.com)

## Summary

Meta-Mar enables researchers to conduct meta-analyses without programming knowledge or software installation. The platform provides:

- Support for continuous, binary, correlation, and pre-calculated effect size data
- Fixed-effect and random-effects models with 8 heterogeneity estimators
- Publication bias assessment (funnel plots, Egger's test, trim-and-fill, fail-safe N)
- Subgroup analysis and meta-regression
- AI-powered interpretation guidance via GPT-4 integration
- Publication-quality visualizations

Since 2020, Meta-Mar has been used by over 5,800 researchers across 120+ countries and cited in 320+ peer-reviewed publications.

## Installation

### Requirements

- R >= 4.0.0
- RStudio (recommended for local development)

### Dependencies

```r
install.packages(c(
  "shiny",
  "metafor",
  "meta",
  "ggplot2",
  "dplyr",
  "DT",
  "shinythemes",
  "shinyjs",
  "httr",
  "jsonlite"
))
```

### Running Locally

```bash
git clone https://github.com/mirzafarangi/meta-mar.git
cd meta-mar
```

```r
shiny::runApp()
```

The application will open in your default browser at `http://127.0.0.1:xxxx`.

## Usage

### Data Input

Meta-Mar accepts CSV files or manual data entry for:

| Data Type | Required Columns |
|-----------|------------------|
| Continuous | `study`, `n.e`, `mean.e`, `sd.e`, `n.c`, `mean.c`, `sd.c` |
| Binary | `study`, `event.e`, `n.e`, `event.c`, `n.c` |
| Correlation | `study`, `cor`, `n` |
| Pre-calculated | `study`, `TE`, `seTE` |

### Example

```r
# Example continuous outcome data structure
data <- data.frame(
  study = c("Study A", "Study B", "Study C"),
  n.e = c(50, 75, 60),
  mean.e = c(12.5, 13.2, 11.8),
  sd.e = c(3.2, 2.9, 3.5),
  n.c = c(48, 72, 58),
  mean.c = c(10.1, 10.8, 9.9),
  sd.c = c(3.0, 3.1, 3.3)
)
```

## Statistical Methods

### Effect Size Measures

- **Continuous:** Standardized Mean Difference (SMD), Mean Difference (MD), Ratio of Means
- **Binary:** Odds Ratio (OR), Risk Ratio (RR), Risk Difference (RD)
- **Correlation:** Fisher's z transformation

### Heterogeneity Estimators

REML, DerSimonian-Laird, Paule-Mandel, Maximum Likelihood, Empirical Bayes, Sidik-Jonkman, Hedges, Hunter-Schmidt

### Confidence Interval Methods

Classic (Wald), Hartung-Knapp-Sidik-Jonkman (HKSJ), Kenward-Roger

### Publication Bias

- Funnel plot visualization
- Egger's regression test
- Begg's rank correlation test
- Trim-and-fill adjustment
- Fail-safe N (Rosenthal, Orwin, Rosenberg)

## Project Structure

```
meta-mar/
├── app.R              # Shiny UI and server logic
├── global.R           # Global functions, settings, demo data
├── user_summary.R     # Session management utilities
├── data/
│   └── statistics.json
├── paper.md           # JOSS paper
├── paper.bib          # References
├── LICENSE            # MIT License
└── README.md
```

## Core Dependencies

Meta-Mar builds on established R packages for meta-analysis:

- **metafor** (Viechtbauer, 2010): Core meta-analytic computations
- **meta** (Balduzzi et al., 2019): Additional methods and visualizations
- **shiny** (Chang et al., 2024): Web application framework

## Validation

Computational accuracy has been validated against Cochrane RevMan 5.4. See the accompanying paper for detailed comparison results.

## Privacy

- No user registration required
- Uploaded data stored in session memory only
- Automatic deletion when session ends
- No persistent storage of user data
- AI interactions not permanently stored

Full privacy policy: [https://www.meta-mar.com/privacy](https://www.meta-mar.com)

## Citation

If you use Meta-Mar in your research, please cite:

```bibtex
@software{beheshti2026metamar,
  author = {Beheshti, Ashkan and Chavanon, Mira-Lynn and Albrecht, Björn and Christiansen, Hanna},
  title = {Meta-Mar: An AI-Integrated Web Platform for Meta-Analysis},
  year = {2026},
  url = {https://github.com/mirzafarangi/meta-mar},
  version = {4.0.2}
}
```

## Contributing

Contributions welcome. Please:

1. Fork the repository
2. Create a feature branch
3. Follow R tidyverse style guide
4. Test with known datasets
5. Submit pull request

## License

MIT License. See [LICENSE](LICENSE) for details.

## Contact

- **Website:** [https://www.meta-mar.com](https://www.meta-mar.com)
- **Issues:** [GitHub Issues](https://github.com/mirzafarangi/meta-mar/issues)
- **Author:** Ashkan Beheshti, Philipps-Universität Marburg

## Acknowledgments

Development supported by Philipps-Universität Marburg, Department of Psychology.
