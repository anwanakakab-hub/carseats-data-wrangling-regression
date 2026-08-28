[README_Carseats_Data_Wrangling_Regression (1).md](https://github.com/user-attachments/files/31540833/README_Carseats_Data_Wrangling_Regression.1.md)
# Carseats Data Management, Wrangling, and Regression in Python

## About the Project

This project rewrites an introductory **R data-management and regression lab in Python** using the ISLR / ISLR2 `Carseats` dataset.

The workflow demonstrates how to move from raw data inspection to a business-readable regression analysis.

The project covers:

- dataset inspection,
- missing-value checks,
- duplicate checks,
- categorical-data review,
- sales sorting and filtering,
- feature engineering,
- multiple linear regression,
- statistical interpretation,
- and business-focused visualization.

The central analytical question is:

> **How are Price, store location, US status, and shelf placement related to car-seat sales?**

---

## Dataset

The Carseats dataset contains:

- **400 store observations**
- **11 original variables**

### Variables

| Variable | Description |
|---|---|
| Sales | Unit sales in thousands |
| CompPrice | Competitor price |
| Income | Community income level |
| Advertising | Local advertising budget |
| Population | Population size |
| Price | Company car-seat price |
| ShelveLoc | Shelf quality: Bad, Medium, Good |
| Age | Average local population age |
| Education | Education level |
| Urban | Urban store indicator |
| US | US store indicator |

The Python notebook creates two additional fields:

- `HighSales`
- `HighSales_Flag`

---

## Executive Findings

### 1. The Dataset Is Clean

The original analysis found:

- **400 rows**
- **11 variables**
- **0 missing values**

This means no missing-value imputation was required before the main analysis.

---

### 2. Maximum Sales = 16.27

The highest recorded Sales value is:

**16.27 thousand units**

This occurs at one store in the dataset.

---

### 3. Only 27 Stores Exceed the High-Sales Threshold

The analysis defines:

```text
High Sales = Sales > 12
```

Only **27 of 400 stores** meet this condition.

That means approximately **6.75%** of stores fall into the high-sales group.

This is useful context because the threshold identifies a relatively small top-performing segment rather than splitting the dataset evenly.

---

## Feature Engineering

The R analysis creates a `HighSales` field based on the threshold:

```python
Carseats["HighSales"] = np.where(
    Carseats["Sales"] > 12,
    "Yes",
    "No"
)
```

The Python version also creates:

```python
Carseats["HighSales_Flag"]
```

where:

- 1 = High Sales
- 0 = Not High Sales

This makes the dataset easier to reuse later for classification models.

---

# Regression Analysis

## Model

The project fits:

```text
Sales ~ Price + Urban + US + ShelveLoc
```

The model explains approximately:

- **R² = 0.5734**
- **Adjusted R² = 0.5680**

This means the selected variables explain roughly **57% of the variation in store sales**.

---

## Regression Results

| Variable | Estimate | Business Meaning |
|---|---:|---|
| Intercept | 11.320 | Baseline prediction |
| Price | **-0.058** | Higher price is associated with lower sales |
| Urban = Yes | 0.245 | Small positive relationship |
| US = Yes | **1.002** | US stores have higher predicted sales |
| ShelveLoc = Good | **4.853** | Strong positive shelf-placement effect |
| ShelveLoc = Medium | **1.913** | Better than Bad shelf placement |

---

## Insight 1 — Shelf Placement Has the Largest Estimated Effect

The strongest coefficients in the model are associated with `ShelveLoc`.

Compared with a **Bad** shelf location:

- **Good** shelf placement is associated with approximately **4.85 thousand additional units of sales**
- **Medium** shelf placement is associated with approximately **1.91 thousand additional units**

The shelf-location effects are also highly statistically significant in the original regression.

### Business Interpretation

Shelf placement appears to be a major commercial driver.

A retailer deciding between improving shelf visibility and simply targeting more urban locations would find much stronger evidence in favor of shelf-quality improvements.

---

## Insight 2 — Higher Prices Are Associated with Lower Sales

The Price coefficient is approximately:

**-0.058**

Holding Urban status, US status, and shelf location constant:

> A $1 increase in Price is associated with approximately **0.058 thousand fewer units sold**.

The Price coefficient is highly statistically significant.

### Business Interpretation

Pricing decisions can materially affect volume.

This does not automatically mean that the company should lower price, because the model analyzes sales volume rather than profit.

A stronger commercial analysis would combine the price effect with unit margin.

---

## Insight 3 — US Stores Perform Better

The `US = Yes` coefficient is approximately:

**+1.002**

Holding the other model variables constant, US stores are predicted to sell about **1 thousand more units** than non-US stores.

The original model reports a very small p-value for this effect, indicating strong statistical evidence.

---

## Insight 4 — Urban Status Is Not a Strong Predictor

The Urban coefficient is approximately:

**+0.245**

However, its original p-value is approximately:

**0.231**

This is above the common 0.05 significance threshold.

### Interpretation

After controlling for Price, US status, and shelf location, the model does not provide strong evidence that Urban location independently predicts Sales.

This is a useful management finding because a variable can appear intuitively important without adding meaningful explanatory power in the regression.

---

## Model Performance

The original regression reports:

| Metric | Result |
|---|---:|
| R² | **0.5734** |
| Adjusted R² | **0.5680** |
| Residual Standard Error | **1.856** |
| F-statistic | **105.9** |
| Overall model p-value | **< 0.001** |

The model is statistically significant overall.

However, about 43% of Sales variation remains unexplained.

Additional predictors such as competitor price, advertising, income, population, and age could be explored in future models.

---

## Why This Project Is Useful

This project demonstrates several foundational analytics skills in one workflow:

### Data Management

- Inspecting dimensions
- Reviewing data types
- Missing-value checks
- Duplicate checks
- Categorical-value validation

### Data Wrangling

- Sorting
- Filtering
- Creating derived variables
- Converting categories into model-ready form

### Statistical Modeling

- Multiple linear regression
- Dummy-variable interpretation
- Significance testing
- R² interpretation

### Business Analytics

- Converting model coefficients into plain-English business insights
- Distinguishing statistical significance from practical importance
- Identifying actionable variables

---

## My Role

For this project, I completed the Python version of the end-to-end workflow, including:

- loading the Carseats dataset,
- validating dataset structure,
- checking missing values,
- reviewing duplicates,
- cleaning categorical formats,
- identifying maximum sales,
- filtering high-sales stores,
- engineering the HighSales field,
- profiling shelf-location performance,
- fitting the regression model,
- interpreting regression coefficients,
- and creating business-focused visualizations.

---

## Key Skills & Tools

### Python

- Pandas
- NumPy
- Matplotlib
- Statsmodels
- Jupyter Notebook

### Data Management

- Missing-Value Analysis
- Duplicate Detection
- Data-Type Review
- Categorical Cleaning
- Filtering
- Sorting
- Feature Engineering

### Statistics

- Multiple Linear Regression
- Categorical Predictors
- Regression Coefficients
- P-values
- R-squared
- Adjusted R-squared
- F-test

### Business Analytics

- Pricing Analysis
- Store Performance
- Shelf Placement Analysis
- Sales Segmentation
- Data-Driven Recommendations

---

## Repository Structure

```text
carseats-data-wrangling-regression/
│
├── Carseats_Data_Wrangling_Regression_Python.ipynb
│   └── Main step-by-step Python notebook
│
├── carseats_data_wrangling_regression.py
│   └── Standalone Python script
│
├── data/
│   └── Carseats.csv
│
├── outputs/
│   ├── carseats_cleaned_with_highsales.csv
│   ├── high_sales_stores.csv
│   ├── regression_coefficients.csv
│   └── regression_model_performance.csv
│
└── README.md
```

---

## How to Run

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/carseats-data-wrangling-regression.git
cd carseats-data-wrangling-regression
```

### 2. Install Packages

```bash
pip install pandas numpy matplotlib statsmodels jupyter
```

### 3. Add the Dataset

Place:

```text
Carseats.csv
```

in the repository root or `data/` folder.

If no local dataset is available, the notebook can attempt to retrieve `Carseats` from the R datasets repository using Statsmodels.

### 4. Start Jupyter

```bash
jupyter notebook
```

### 5. Open

```text
Carseats_Data_Wrangling_Regression_Python.ipynb
```

Run the cells from top to bottom.

---

## Limitations

- The model explains sales relationships, not causation.
- The HighSales threshold of 12 is analyst-defined.
- The regression does not include all available Carseats variables.
- The model predicts unit sales, not profit.
- Interaction effects are not included.
- Linear regression assumes a linear relationship between the numeric predictors and Sales.
- The analysis is intended as an introductory data-management and regression exercise.

---

## Future Improvements

Potential extensions include:

- add CompPrice, Income, Advertising, Population, Age, and Education,
- compare full and reduced regression models,
- examine residual assumptions,
- test Price × ShelveLoc interactions,
- build a HighSales classification model,
- compare Logistic Regression, Decision Tree, and SVM,
- analyze profit implications of pricing,
- and create an interactive sales dashboard.

---

## Conclusion

The project shows how a relatively simple dataset can support useful business insights when data management and statistical modeling are combined.

The strongest result is the size of the shelf-location effect.

Good shelf placement is associated with substantially higher sales, while higher prices reduce sales and Urban status adds little explanatory value after the other variables are controlled.

The main takeaway is:

> **Shelf placement and pricing appear to matter much more to store-level car-seat sales than urban location alone.**
