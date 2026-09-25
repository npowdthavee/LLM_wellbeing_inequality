# LLM Well-Being Inequality

Replication code for the project **Large Language Models Substantially Compress Well-Being Inequality but Largely Preserve Its Socioeconomic Structure**.

The study examines whether large language models (LLMs) preserve the socioeconomic structure of human well-being inequality even when their predicted responses are substantially less dispersed than human responses. The main analyses use World Values Survey (WVS) Wave 7 data and compare observed life satisfaction with respondent-level predictions from six LLMs.

## Preregistration

The study was preregistered on AsPredicted:

https://aspredicted.org/sf62bj.pdf

The primary preregistered analyses focus on the relationship between household income position and well-being inequality. Analyses of distributional tails, country-level gradient fidelity, and generalisation to other socioeconomic and psychosocial characteristics are exploratory.

## Data

The study uses **World Values Survey Wave 7** data. The WVS data are not redistributed in this repository. They can be obtained from the World Values Survey:

https://www.worldvaluessurvey.org/WVSDocumentationWV7.jsp

The final common analysis sample contains **93,901 respondents from 66 countries and territories** with valid responses for life satisfaction (Q49) and household income group (Q288).

The main outcome is life satisfaction (Q49), measured from 1 (completely dissatisfied) to 10 (completely satisfied). Household income position (Q288) ranges from 1 (lowest income group) to 10 (highest income group within the respondent's country).

## LLMs

Predictions were collected between **20 and 23 September 2026** using six models:

- GPT-5.6 Luna
- Claude Sonnet 5
- Gemini 3.8 Flash
- DeepSeek V4.1 Flash
- Qwen 3.7 Plus
- Gemma 4 31B

Each model received the same respondent profile and was asked to predict the respondent's life satisfaction on the WVS 1-10 scale. The notebooks record the exact model identifiers, prompts, API endpoints, and output-audit information used for the study.

## Repository structure

### `1_WVS_prepare.ipynb`

Prepares the WVS Wave 7 data, constructs respondent profiles, defines the common analysis sample, and creates the input file used for LLM prediction. The life-satisfaction outcome itself is excluded from the respondent profiles to prevent leakage.

### `2_WVS_predict.ipynb`

Sends respondent profiles to one LLM at a time and saves respondent-level predictions. The notebook contains the exact prompt, model configuration, endpoint settings, batching logic, and technical audit information.

Required environment variables are:

- `OPENAI_API_KEY`
- `ANTHROPIC_API_KEY`
- `GEMINI_API_KEY`
- `DEEPSEEK_API_KEY`
- `DASHSCOPE_API_KEY`
- `DEEPINFRA_API_KEY`

API keys are not stored in this repository.

### `3_WVS_Human_LLM_Analysis.ipynb`

Runs the main human-LLM analyses, including raw income gradients in mean life satisfaction and well-being inequality, scale-normalised dispersion profiles, profile-comparison tests, country-fixed-effect RIF variance regressions, RIF-Oaxaca decompositions, distributional-tail analyses, and country-level gradient-fidelity analyses.

### `4_WVS_Generalization_Other_Characteristics.ipynb`

Extends the scale-normalised heterogeneity analysis to employment status, educational attainment, marital status, and perceived freedom and control.

## Reproduction order

Run the notebooks in numerical order:

1. `1_WVS_prepare.ipynb`
2. `2_WVS_predict.ipynb` separately for each model
3. `3_WVS_Human_LLM_Analysis.ipynb`
4. `4_WVS_Generalization_Other_Characteristics.ipynb`

The prediction notebook is intentionally designed to run one model at a time. Retain the output CSV from each completed model before proceeding to the main analysis.

## Main methodological distinction

The paper distinguishes between two aspects of second-moment fidelity:

- **Scale fidelity:** whether an LLM reproduces the overall amount of human heterogeneity.
- **Structural fidelity:** whether it reproduces where relatively greater and lower heterogeneity occurs across social groups.

To study structural fidelity independently of overall compression, within-group standard deviations are normalised by each source's own weighted-average standard deviation, using fixed human group shares as weights.

## Reproducibility

The notebooks contain the complete data-processing, prompting, prediction, and analysis code used for the paper. Because the WVS microdata and API credentials are subject to their respective access and licensing conditions, they are not included in the repository.

## Citation

A manuscript citation will be added when the paper is publicly available.
