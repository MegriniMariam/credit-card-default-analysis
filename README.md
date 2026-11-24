# Who defaults on a credit card? Evidence from 30,000 Taiwanese clients

**RM402E – Statistics & Data Analysis · Group project (November 2026)**

**Group members:** Malak ACHOUAQ · Andrée Camille Manuella BROU · Marie Christelle Anaïs KOUAME · Mariam MEGRINI · Israel MENDEZ AYAVIRI · Evgeniia NAKARIAKOVA (RM402E_GR04)

## Research question
> Which client characteristics and payment behaviours are associated with defaulting on a credit-card payment next month, and how well can we predict default from them?

## Dataset
**Default of Credit Card Clients** – 30,000 clients of a bank in Taiwan, April–September 2005, 25 columns.

- Kaggle: https://www.kaggle.com/datasets/uciml/default-of-credit-card-clients-dataset
- Original source: UCI Machine Learning Repository – Yeh, I. C. (2009), https://doi.org/10.24432/C55H7Z (licence CC BY 4.0)
- Target: `default.payment.next.month` (1 = default in October 2005, 0 = no default)
- Main variables: credit limit (`LIMIT_BAL`), sex, education, marital status, age, repayment status for 6 months (`PAY_0`, `PAY_2`–`PAY_6`), bill amounts (`BILL_AMT1–6`) and payments (`PAY_AMT1–6`).

## Repository content
| File | Description |
|---|---|
| `Credit_Card_Default_Analysis.ipynb` | The Google Colab notebook = the full report (code, outputs, comments, conclusions) |
| `UCI_Credit_Card.csv` | The raw dataset (30,000 rows × 25 columns) |
| `UCI_Credit_Card_clean.csv` | The clean dataset created by the notebook (30,000 rows × 28 columns: `ID` removed, unknown codes grouped, new columns `sex_name`, `education_name`, `age_group`, `months_late`) |
| `README.md` | This file |

## Methodology
1. **Data cleaning** – missing values, duplicates, removal of `ID`, unknown codes of `EDUCATION` and `MARRIAGE` grouped into "others", new variable `months_late`.
2. **Descriptive statistics and charts** – mean, median, skewness, default rate by group.
3. **Probability** – Shapiro-Wilk test, probabilities and conditional probabilities from the data, Central Limit Theorem with `norm.cdf`, `norm.sf`, `norm.ppf`.
4. **Confidence intervals** – default rate and mean credit limit.
5. **Hypothesis tests** – Shapiro-Wilk, Mann-Whitney U, chi-square, Kruskal-Wallis, Wilcoxon.
6. **Correlation and linear regression** – Spearman correlation, simple and multiple OLS on the credit limit.
7. **Prediction** – logistic regression (with balanced classes) and random forest.

## Main results
- **22.12%** of the clients default (95% CI: 21.65%–22.59%).
- Clients late in September default in **50%** of the cases against **14%** for clients on time; clients with 2 months of delay in September default in **69%** of the cases.
- Defaulters have a lower credit limit (median 90,000 vs 150,000 NT$, Mann-Whitney p ≈ 0).
- Sex, education and age group are linked to default (chi-square p < 0.05) but the differences are small (19%–27%).
- The credit limit depends mostly on education and on past delays (multiple regression, R² = 0.175).
- Random forest: best accuracy (81.5%). Balanced logistic regression: finds the most defaulters (recall 0.57, F1 0.52). The naive model is 77.9% accurate but finds no defaulter.

**Conclusion:** default is mainly linked to the recent payment behaviour of the client, not to who the client is.

## How to run
1. Open `Credit_Card_Default_Analysis.ipynb` in Google Colab (menu "File", then "Upload notebook", or open it from GitHub).
2. Run the cells; when the upload window appears, choose `UCI_Credit_Card.csv`.
3. Click "Runtime", then "Run all". The results are reproducible (`random_state=0`).

Libraries: pandas, NumPy, Matplotlib, Seaborn, SciPy, statsmodels, scikit-learn (all already in Colab).

## Limitations and ethics
Data from one Taiwanese bank in 2005, only six months of history and no income data. With 30,000 observations almost every test is significant, so we also look at the size of the differences. Results are associations, not causal effects. Sex, age and marital status are protected characteristics: this is an academic exercise, not a credit-scoring tool.

## Reference
Yeh, I. C., & Lien, C. H. (2009). The comparisons of data mining techniques for the predictive accuracy of probability of default of credit card clients. *Expert Systems with Applications*, 36(2), 2473–2480.
