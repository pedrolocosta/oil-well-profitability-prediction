# Oil Well Profitability Prediction — Machine Learning & Risk Analysis

**Data Science portfolio project | TripleTen MBA in Artificial Intelligence & Data Science**

Predicting oil reserves is only one part of an investment decision. This project combines **Python, exploratory data analysis, linear regression, model evaluation, financial modeling, and bootstrap simulation** to choose an oil-development region while controlling downside risk.

## Business problem

A simulated oil company must choose **one of three regions** for developing new wells. The decision process evaluates 500 candidate sites and selects the 200 wells with the highest predicted reserves. The investment must satisfy a **maximum 2.5% probability of loss**.

The project uses three geological datasets, each initially containing 100,000 records. These are educational scenario data, not real investment recommendations.

## Key results

| Measure | Result |
| --- | --- |
| Recommended region | **Region 01** |
| Estimated mean profit (bootstrap) | **$4.61 million** |
| Estimated probability of loss | **0.7%** |
| 95% bootstrap profit interval | **$0.78M–$8.63M** |
| Simulations | **1,000 bootstrap samples** of 500 candidate wells |

**Why not Region 00?** Selecting the 200 highest-ranked wells from the full validation set produced a higher *single-scenario* potential profit of about **$33.2M** for Region 00. But that calculation is not directly comparable to the bootstrap scenario, which selects 200 wells from only 500 sampled candidates. Under the latter, Region 00's estimated loss probability was **6.9%**, above the 2.5% limit; Region 02's was **6.5%**. Region 01 was the only region meeting the risk criterion.

These figures are estimates from the notebook's simulated assumptions and validation predictions; they are not guaranteed returns.

## Methodology

1. **Data preparation and EDA:** inspect three geological datasets, check missing values and duplicates, rename the reserve target to clarify units, and remove 10 duplicate well IDs in Region 00.
2. **Predictive modeling:** train a separate **Linear Regression** model for each region using a **75/25 train/validation split**. Fit **StandardScaler** on training features only.
3. **Model evaluation:** compare predicted and actual reserve volumes using **RMSE** and **R²**. Region 01's validation RMSE was approximately **0.89 thousand barrels**, whereas Regions 00 and 02 showed much larger errors.
4. **Profit modeling:** rank wells by predicted reserves, then calculate realized profit using the corresponding actual reserves and the project's financial assumptions.
5. **Risk assessment:** run **1,000 bootstrap resamples** of **500 wells**, select the top **200** in each resample, and estimate mean profit, a percentile-based **95% interval**, and the fraction of simulations with negative profit.
6. **Business recommendation:** choose a region only if the estimated loss probability is below **2.5%**.

### Financial assumptions

- Total development budget: **$100 million**
- Wells selected for development: **200**
- Revenue: **$4,500 per thousand barrels**
- Break-even volume per well: approximately **111.11 thousand barrels**

## Tools and skills

**Python · Pandas · NumPy · scikit-learn · Exploratory Data Analysis (EDA) · Linear Regression · Predictive Modeling · RMSE · R² · Bootstrapping · Statistical Simulation · Risk Analysis · Business Analytics · Data-Driven Decision-Making**

## Repository contents

- [`notebook.ipynb`](notebook.ipynb) — complete analysis, code, outputs, and conclusions
- [`datasets/`](datasets/) — project datasets
- [`requirements.txt`](requirements.txt) — pinned Python dependencies

## Reproduce the analysis

Requires **Python 3.12**. From the repository root:

```bash
python -m venv .venv
# Windows PowerShell:
.venv\Scripts\Activate.ps1
# macOS/Linux:
# source .venv/bin/activate
pip install -r requirements.txt
```

Open `notebook.ipynb` in VS Code or Jupyter and run the cells in order. Check the dataset paths in the notebook against your local `datasets/` folder before execution.

## Interpretation and limitations

- **Predictive accuracy and business value are different questions.** Region 00 had the highest one-off potential profit, but did not satisfy the risk constraint in the simulated selection process.
- The bootstrap interval describes the **simulated distribution of profits under the notebook's assumptions**; it should not be interpreted as a guarantee about future investments.
- The project uses **linear regression** and a fixed training/validation split, not a production deployment or a causal study.
- Region 01's exceptionally strong predictive fit reflects this particular dataset and should not be assumed to generalize to real oil exploration.

## About

Created as part of my **MBA in Artificial Intelligence & Data Science at TripleTen**. My portfolio focuses on applying **Data Science, statistical reasoning, and Machine Learning** to practical decisions, drawing on my background in Mechanical Engineering.

- [GitHub profile](https://github.com/pedrolocosta)
- [LinkedIn](https://www.linkedin.com/in/pedrolocosta/)
- [Portfolio](https://ocaiengineering.com/)
