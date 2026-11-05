# FONG HIO LAM

![FONG HIO LAM avatar](https://github.com/FongHioLam-mc654953.png){ width="128" style="border-radius:50%" }

**Master's Student in Data Science & AI (in progress) · University of Macau**

Currently pursuing my **M.Sc. in Data Science & AI** at the University of Macau. Interested in **data analysis** and **machine learning** — building end-to-end pipelines from raw data to models, and turning insights into clear visualisations.

## Technical Skills

- **Languages & Tools**: Python ★★★★☆ · Jupyter Notebook ★★★★★
- **Data Manipulation**: pandas ★★★★☆ · numpy ★★★★☆
- **Visualisation**: matplotlib ★★★☆☆ · seaborn ★★★☆☆
- **Machine Learning**: scikit-learn ★★★★☆ (regression, cross-validation, Ridge, GridSearchCV) · PyTorch ★★★☆☆
- **Workflow**: data cleaning, EDA, model development, hyper-parameter tuning

## About

- **University**: University of Macau (UM) — Macao SAR, China
- **Programme**: M.Sc. in Data Science & AI (in progress)
- **Key Courses**: CISC7021 Applied NLP · CISC7201 Data Mining · CISC7204 Machine Learning · CISC7026 Deep Learning
- **Contact**: [mc65495@um.edu.mo](mailto:mc65495@um.edu.mo)
- **Course context**: CISC7204 Machine Learning · November 2026
- **Peer review**: [PEER_FEEDBACK.md](PEER_FEEDBACK.md) — the review received on 2026-11-05 and the change made in response to each item

## Research Questions

1. **Car price prediction** — Can we predict the price of a car (USD) from its technical specifications (engine size, horsepower, fuel type, body style)?
2. **Laptop price prediction** — Can we predict the price of a laptop (USD) from its hardware attributes (CPU frequency, screen size, RAM, storage, GPU)?
3. **House price prediction (King County, USD)** — Which features (sqft living area, waterfront, floors) drive house prices, and can a regression pipeline predict them?
4. **Medical insurance cost prediction (USD)** — How do BMI, smoker status, age and other factors affect individual medical charges?

## Approach

Every question runs through the same six-stage pipeline, applied to a different dataset:

- **Libraries**: pandas, numpy, matplotlib, seaborn, scikit-learn, Jupyter Notebook
- **Data cleaning**: `?` placeholders converted to missing values, drop / mean / mode imputation, unit conversion (MPG to L/100km), dummy variables (`pd.get_dummies`), binning (`pd.cut`)
- **EDA**: correlation matrices and heatmaps, scatter and box plots, pivot tables, Pearson correlation coefficients
- **Modelling**: simple, multiple and polynomial regression (degrees 1–11) inside scikit-learn `Pipeline` objects, scored with R-squared
- **Validation and tuning**: train/test split, k-fold cross-validation, `cross_val_predict`, Ridge regression, `GridSearchCV` over the alpha grid
- **Units**: every price and charge in this portfolio is reported in USD

## Key Findings

- **More polynomial degree is not more accuracy.** On the Auto data a degree-5 model reaches training R-squared 0.557 while test R-squared falls to −29.87 — a negative R-squared means the model predicts worse than simply guessing the mean, which is the clearest overfitting signal; 4-fold cross-validation returns 0.522 with a spread of ±0.291, and that spread is the instability itself.
- **Regularisation repairs an over-flexible model.** Ridge with an alpha tuned by GridSearchCV (10,000 on Auto, 10 on Laptops) brings validation R-squared back to 0.564 on Auto (train 0.859) and 0.423 on Laptops, trading a little training fit for a test score that no longer collapses.
- **Feature coverage matters more than model family.** King County house prices (USD) rise from R-squared 0.493 with sqft_living alone to 0.658 with multiple features and 0.751 through the full pipeline, while insurance charges (USD) reach 0.845 with all features against 0.622 for smoker status alone.

## Limitations

- This is a course assignment: the models are built to demonstrate the full pipeline rather than for production deployment.
- Some datasets contain `?` placeholders that are imputed or dropped, so results depend on those preprocessing choices.
- A few notebooks download their datasets from external URLs and therefore need network access to run end to end.
- No external or held-out temporal validation beyond the provided train/test splits.

## Projects

### CISC7204 Assignment 1 — Price Regression Full-Pipeline Analysis

A complete machine learning project covering the full workflow: data import → cleaning → EDA → modelling → cross-validation & tuning. Each module is showcased separately on the website.

- **Module 01 — Data Import**: load the Auto and Laptops price datasets, both in USD ([Module01_Lab01_Data_Import_Auto.ipynb](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/Module%2001/Module01_Lab01_Data_Import_Auto.ipynb) · [Module01_Lab02_Data_Import_Laptops.ipynb](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/Module%2001/Module01_Lab02_Data_Import_Laptops.ipynb)) · [auto.csv](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/Module%2001/auto.csv) · [laptops.csv](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/Module%2001/laptops.csv) · [charts](images/module01_basic_insights.png)
- **Module 02 — Data Cleaning**: merge columns & dummy variables ([Module02_Lab01_Data_Cleaning_Auto.ipynb](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/Module%2002/Module02_Lab01_Data_Cleaning_Auto.ipynb) · [Module02_Lab02_Data_Cleaning_Laptops.ipynb](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/Module%2002/Module02_Lab02_Data_Cleaning_Laptops.ipynb)) · [auto.csv](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/Module%2002/auto.csv) · [clean_df.csv](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/Module%2002/clean_df.csv) · [laptops.csv](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/Module%2002/laptops.csv) · [charts](images/module02_horsepower_histogram.png)
- **Module 03 — EDA**: correlation heatmaps & scatter plots ([Module03_Lab01_EDA_Auto.ipynb](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/Module%2003/Module03_Lab01_EDA_Auto.ipynb) · [Module03_Lab02_EDA_Laptops.ipynb](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/Module%2003/Module03_Lab02_EDA_Laptops.ipynb)) · [Module 03 files](https://github.com/FongHioLam-mc654953/data-science-project/tree/main/Module%2003) · [charts](images/module03_correlation_matrix.png)
- **Module 04 — Model Development**: simple / multiple / polynomial regression ([Module04_Lab01_Model_Development_UsedCars.ipynb](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/Module%2004/Module04_Lab01_Model_Development_UsedCars.ipynb) · [Module04_Lab02_Model_Development_Laptops.ipynb](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/Module%2004/Module04_Lab02_Model_Development_Laptops.ipynb)) · [usedcars.csv](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/Module%2004/usedcars.csv) · [laptops.csv](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/Module%2004/laptops.csv) · [charts](images/module04_compare_models.png)
- **Module 05 — Cross-Validation · Ridge · Grid Search**: k-fold CV, Ridge, GridSearchCV. Auto: CV mean R² 0.522 (±0.291 — that spread shows the model is unstable across folds); degree-5 polynomial overfits hard (train R² 0.557 vs test R² −29.87, and a negative R² means the model does worse than predicting the mean); tuned Ridge val R² 0.564; best α = 10000. Laptops: single-feature CV R² 0.127; polynomial test R² 0.053→−1.376; Ridge val R² 0.423; best α=10. ([Module05_Lab01_CrossValidation_Ridge_Auto.ipynb](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/Module%2005/Module05_Lab01_CrossValidation_Ridge_Auto.ipynb) · [Module05_Lab02_CrossValidation_Ridge_Laptops.ipynb](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/Module%2005/Module05_Lab02_CrossValidation_Ridge_Laptops.ipynb)) · [module_5_auto.csv](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/Module%2005/module_5_auto.csv) · [laptops.csv](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/Module%2005/laptops.csv) · [charts](images/module05_r2_across_polynomial_orders.png)
- **Module 06 — House Pricing & Insurance**: King County house sales and medical insurance datasets, both in USD. House: sqft_living LR R² 0.493 → multi-feature 0.658 → full pipeline 0.751; Ridge (α=0.1) 0.648; poly2+Ridge 0.700. Insurance: smoker 0.622 → all-feature 0.750 → pipeline 0.845; Ridge test 0.676; poly2 Ridge test 0.784. ([Module06_FinalProject_HousePricing.ipynb](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/Module%2006/Module06_FinalProject_HousePricing.ipynb) · [Module06_PracticeProject_InsuranceCost.ipynb](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/Module%2006/Module06_PracticeProject_InsuranceCost.ipynb)) · [kc_house_data_NaN.csv](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/Module%2006/kc_house_data_NaN.csv) · [medical_insurance_dataset.csv](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/Module%2006/medical_insurance_dataset.csv) · [charts](images/module06_price_vs_sqft_correlations.png)
- **Preliminary Project — Macau Bus Supply & Demand**: pair-project bus supply/demand analysis, built jointly with a fellow CISC7204 student ([PreliminaryProject_ProposalVerification.ipynb](https://github.com/FongHioLam-mc654953/data-science-project/blob/main/PreliminaryProject_Pair/PreliminaryProject_ProposalVerification.ipynb) · [PreliminaryProject_Pair folder](https://github.com/FongHioLam-mc654953/data-science-project/tree/main/PreliminaryProject_Pair)) · [charts](images/bus_fig1_supply_demand_match.png)

- **Repository**: [github.com/FongHioLam-mc654953/data-science-project](https://github.com/FongHioLam-mc654953/data-science-project)
- **Status**: Completed
