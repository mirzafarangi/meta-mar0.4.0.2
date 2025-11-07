# Meta-Mar

Free online meta-analysis platform for research and education.

**Website:** [https://www.meta-mar.com](https://www.meta-mar.com)

---

## Overview

Meta-Mar is a web-based meta-analysis platform that integrates statistical analysis with AI assistance. The platform supports comprehensive meta-analytic procedures from basic effect size calculations to advanced heterogeneity assessment and publication bias evaluation. No installation or registration required.

The platform serves both research and educational purposes, providing an interactive environment where users can explore meta-analytic concepts while conducting analyses. The integrated AI assistant offers context-specific methodological guidance and helps interpret analytical choices.

---

## Core Capabilities

### Methodological Flexibility
Support for various outcome types including continuous data, binary outcomes, correlations, and effect sizes. Implements both fixed-effect and random-effects models with multiple estimators (REML, DL, PM, ML, HS, SJ, HE, EB). Provides different calculation methods for confidence intervals including classic, Hartung-Knapp, and Kenward-Roger adjustments.

### Statistical Analysis
- Effect size calculation and pooling
- Heterogeneity assessment (I², τ², Cochran's Q)
- Subgroup analysis
- Meta-regression with continuous and categorical moderators
- Sensitivity analysis

### Publication Bias Assessment
Multiple methods for evaluating publication bias including Egger's test, Begg's test, trim-and-fill analysis, and fail-safe N calculations (Rosenthal, Orwin, Rosenberg methods).

### Visualization
Publication-quality plots including forest plots, funnel plots, Galbraith plots, L'Abbe plots, Baujat plots, and bubble plots for meta-regression. All visualizations support customization for statistical presentation.

### AI Integration
Interactive AI chatbot providing methodological guidance, interpretation support, and learning assistance through natural language interaction. Includes AI-powered report generation for comprehensive summaries of meta-analysis results.

---

## Technical Architecture

### Frontend
- **Landing Page:** Python/Flask serving static HTML with minimal JavaScript
- **Analysis Interface:** R Shiny application providing interactive statistical analysis
- **Styling:** Custom CSS following academic design principles with consistent typography and color scheme

### Backend
- **Statistical Engine:** R with `meta`, `metafor`, and `pimeta` packages
- **AI Integration:** OpenAI API for chatbot and report generation
- **Data Handling:** Session-based temporary storage with automatic deletion after analysis completion

### Deployment
- **Web Server:** PythonAnywhere for Flask frontend
- **Application Server:** shinyapps.io for R Shiny backend
- **Domain:** Custom domain with SSL/TLS encryption

---

## Project Structure

```
metamar_web/
├── python_side/
│   ├── app.py                          # Flask application
│   ├── templates/
│   │   ├── metamar.html                # Landing page
│   │   ├── documentation_frame.html    # Documentation viewer
│   │   ├── support_content.html        # Support and survey
│   │   └── survey_results.html         # Survey statistics
│   ├── survey_responses.csv            # Survey data storage
│   └── .env                            # Environment variables
│
├── R_Side/
│   └── metamar0.4.0.2/
│       ├── app.R                       # Shiny UI and server
│       ├── global.R                    # Global functions and settings
│       ├── user_summary.R              # Session management
│       └── documentation_MetaMar.R     # Documentation content
│
└── README.md
```

---

## Installation and Deployment

### Local Development

**Prerequisites:**
- Python 3.8+
- R 4.0+
- Required R packages: `shiny`, `meta`, `metafor`, `pimeta`, `ggplot2`, `dplyr`, `DT`, `httr`, `jsonlite`

**Flask Frontend:**
```bash
cd python_side
pip install -r requirements.txt
python app.py
```

**R Shiny Backend:**
```r
# In R console
setwd("R_Side/metamar0.4.0.2")
shiny::runApp()
```

### Production Deployment

**PythonAnywhere (Flask):**
1. Clone repository to PythonAnywhere
2. Configure web app to point to `python_side/app.py`
3. Set environment variables in `.env` file
4. Reload web app

**shinyapps.io (R Shiny):**
```r
library(rsconnect)
setwd("R_Side/metamar0.4.0.2")
deployApp()
```

---

## Configuration

### Environment Variables

Create `.env` file in `python_side/`:
```
STRIPE_SECRET_KEY=your_stripe_key_here
ADMIN_PASSWORD=your_admin_password_here
```

### R Configuration

API keys and settings configured in `global.R`:
- OpenAI API key for AI features
- Session timeout settings
- Statistical defaults

---

## Data Privacy

Meta-Mar implements strict data privacy measures:

- **User Data:** All uploaded data stored temporarily in session memory only
- **Automatic Deletion:** Data automatically deleted when browser session ends
- **No Persistent Storage:** No user data retained on servers
- **AI Interactions:** Chat conversations not stored permanently
- **Analytics:** Google Analytics tracks usage patterns only, not user data

See Privacy Policy at [https://www.meta-mar.com](https://www.meta-mar.com) for complete details.

---

## Development Priorities Survey

The platform includes a public survey system for gathering user feedback on development priorities:

- **Survey Submission:** Available in Support tab
- **Data Storage:** CSV file (`survey_responses.csv`) with append-only writes
- **Public Results:** Accessible at `/survey-results` with real-time statistics
- **Persistence:** Survey data survives deployments and server restarts

---

## Citation

If you use Meta-Mar in your research, please cite:

```
Beheshti, A., Chavanon, M. L., & Christiansen, H. (2020). 
Emotion dysregulation in adults with attention deficit hyperactivity disorder: 
a meta-analysis. BMC psychiatry, 20, 1-11.
https://www.meta-mar.com
```

---

## Contributing

Contributions are welcome. Please ensure all changes maintain the platform's academic style and minimal design principles.

### Code Style
- Python: PEP 8 compliance
- R: Tidyverse style guide
- HTML/CSS: Consistent with existing templates
- No emoji or decorative elements in user-facing text

### Testing
- Test all statistical functions with known datasets
- Verify AI integration functionality
- Check cross-browser compatibility
- Validate responsive design

---

## License

Meta-Mar is provided free for research and educational purposes.

---

## Support

For technical issues or questions:
- Visit the Support tab at [https://www.meta-mar.com](https://www.meta-mar.com)
- Review documentation in the Documentation tab
- Check example datasets in Resources section

---

## Version History

**2025 Update:**
- Enhanced AI integration with improved chatbot functionality
- AI-powered report generation
- Expanded statistical methods and estimators
- Improved visualization customization
- Survey system for development priorities
- Updated privacy policy and cookie consent

**Previous versions:**
- Initial release (2020)
- Multiple iterative improvements based on user feedback

---

## Technical Notes

### Statistical Methods
All statistical procedures implemented using established R packages (`meta`, `metafor`) following current methodological standards. Effect size calculations, heterogeneity statistics, and publication bias tests conform to published guidelines.

### AI Implementation
AI features use OpenAI's API with custom prompts designed for meta-analysis contexts. The system provides methodological guidance based on statistical best practices and helps users understand analytical outputs.

### Performance
Session-based architecture ensures fast response times. Statistical calculations performed server-side with results cached during session. Visualizations generated on-demand with customization options.

---

**Last Updated:** January 2025
