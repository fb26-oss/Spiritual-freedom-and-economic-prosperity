 Spiritual Freedom and Economic Prosperity
An empirical approach based on Pope Francis' definition of spiritual freedom


 1. Objective of the project

This project asks a simple question: can "spiritual freedom" help explain why some countries are more economically prosperous than others?

Rather than relying on a religious or philosophical definition, the project borrows an operational one from Pope Francis, who describes spiritual freedom as resting on three pillars: **education**, **religious freedom**, and **civil rights such as gender equity**. Using cross-sectional data for 74 countries in 2023, the project tests whether these three pillars are statistically associated with GDP per capita, both globally and within each continent (Africa, America, Asia, Europe).

The empirical model estimated throughout the project is:

```
LOGC = b0 + b1(ED) - b2(RE) + b3(GE) + e
```

| Symbol | Variable | What it measures | Expected sign |
|---|---|---|---|
| `LOGC` | Log of GDP per capita | Economic prosperity (dependent variable) | — |
| `ED` | Adult Literacy Rate | Education | `+` |
| `RE` | Government Restrictions Index | Government restrictions on religion (higher = less religious freedom) | `-` |
| `GE` | Health and Survival Index | Gender equity | `+` |

2. Repository contents

| File | Description |
|---|---|
| [`SAVE.xlsx`](SAVE.xlsx) | The dataset used for the analysis. The relevant worksheet is `clean`, containing `Country`, `ED`, `GE`, `RE`, and `LOGC` for 74 countries. The workbook also keeps the intermediate/raw worksheets used while building the final data set, for full transparency. |
| [`code.txt`](code.txt) | The full SAS script used to import, clean, and analyze the data (rename to `code.sas` if your editor requires a `.sas` extension to enable syntax highlighting). The script is heavily commented so it can be run step by step by anyone, even without prior SAS experience. |
| [`econometrics paper 1211.docx`](econometrics%20paper%201211.docx) | The final paper: literature review, hypotheses, methodology, results, discussion, and conclusion. |

 3. Data sources

The three components of spiritual freedom and the dependent variable come from the following sources:

- Adult Literacy Rate (`ED`) : UNESCO database, via the Fordham Pope Francis Global Poverty Report 2024.
- Government Restrictions Index (`RE`): Pew Research Center, a 10-point scale built from 20 measures of government restriction on religion (e.g. banning faiths, prohibiting conversions, limiting preaching, or granting preferential treatment to specific religious groups).
- Health and Survival Index (`GE`): World Bank database; combines the sex ratio at birth and the gender gap in healthy life expectancy.
- GDP per capita (`LOGC`, log-transformed): World Bank database (current US dollars).

 4. Process followed

1. Data collection: variables were gathered from the World Bank, UNESCO, and the Pew Research Center, then assembled into a single spreadsheet for 74 countries observed in 2023 (listed with their continent in the appendix of the paper).
2. Data cleaning: some numeric fields were imported as text; these were converted back to numbers, and rows with missing values were identified before running any regression.
3. Continent classification: each country was tagged with its continent (Africa, America, Asia, Europe) to allow both a global and a regional analysis.
4. Descriptive statistics & correlation : means, standard deviations, and a correlation matrix were produced to check the data before modeling.
5. Regression analysis: an OLS regression of `LOGC` on `ED`, `RE`, and `GE` was estimated for:
   - the full sample of 74 countries, and
   - each of the four continents separately.
   Diagnostic checks (variance inflation factors for multicollinearity, a specification test for heteroscedasticity, and heteroscedasticity-robust standard errors) were run alongside each model.
6. Interpretation : coefficients, p-values, and R² were compared across the global model and the four regional models to see whether the relationship between spiritual freedom and prosperity holds everywhere, or varies by region.

 5. Summary of findings

| Sample | Equation | R² | Statistically significant variables (10%) |
|---|---|---|---|
| Global (74 countries) | LOGC = 3.12 + 1.36·ED − 0.21·RE − 0.11·GE | 0.57 | ED |
| Africa (32) | LOGC = 3.63 + 0.92·ED − 0.52·RE − 0.21·GE | 0.42 | ED, RE |
| America (16) | LOGC = 1.66 + 1.96·ED − 0.44·RE + 1.29·GE | 0.55 | ED, GE |
| Asia (17) | LOGC = 3.39 + 1.06·ED + 0.09·RE − 0.43·GE | 0.46 | ED |
| Europe (9) | LOGC = 7.63 − 3.02·ED − 0.42·RE − 0.018·GE | 0.51 | none |

Main takeaway: education (`ED`) is the most consistent driver of GDP per capita across the global sample and most regions. Government restrictions on religion (`RE`) tend to depress prosperity, as expected, in the global and African samples. The gender-equity index (`GE`) behaves counter-intuitively in the global sample (negative sign) but positively in America, suggesting the relationship between spiritual freedom and prosperity is not uniform across regions — it appears strongest in the American sample. A full discussion of these results, including limitations and directions for future research, is in the paper.

 6. How to reproduce the analysis

1. Download `SAVE.xlsx` and `code.txt` from this repository.
2. Open `code.txt` in SAS (SAS Studio, SAS OnDemand for Academics, or a local SAS installation). You can rename it to `code.sas` for convenience.
3. In Step 1 of the script, update the file path in the `LIBNAME` statement to point to wherever you saved `SAVE.xlsx` on your own computer.
4. Run the script from top to bottom — each step is commented to explain what it does and what to check in the output before moving to the next one.

 7. Notes and limitations

- The analysis is cross-sectional (single year, 2023); it cannot establish causality or capture how these relationships evolve over time.
- Sample sizes for the regional regressions are small (as few as 9 countries for Europe), so regional coefficients should be interpreted with caution.
- The counter-intuitive sign on the gender-equity index (`GE`) in the global model warrants further investigation, as noted in the paper's conclusion.

 8. Citation

If you use this repository, please cite:

> Bomba, F. (2026). Spiritual Freedom and Economic Prosperity: approach from Pope Francis.
