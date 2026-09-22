# What drives the price of a used car?

A CRISP-DM analysis of 426,880 used-car listings for dealership inventory decisions.

## Summary of findings

- The strongest predictors in the selected model were **model year, mileage, model, fuel, manufacturer**.
- Training listings below 50,000 miles had a **$25,990 median asking price**, compared with **$8,995** at 100,000–150,000 miles. These unadjusted comparisons also reflect vehicle mix.
- Cleaning retained **205,928 listings**. The training-CV-selected model was **Log-price polynomial Lasso**, with **$3,829 test MAE**, **$6,729 RMSE**, and **0.736 R²** on **41,258 test listings**, reducing baseline MAE by **59.2%**.
- Polynomial features + Lasso uses degree **3**, alpha **0.001**, and retains **409 of 465 encoded terms**. The notebook explains its powers, interactions, scaling, and feature selection.
- MAE above $40,000 is **$15,487**. Use individual appraisal and current local comparables. Asking prices do not establish consumer willingness to pay, profits, or sales speed.

**Recommended actions:** compare model year, mileage, and specifications; verify condition and title; measure sale prices, days to sell, and costs before changing inventory mix.

## Models and validation

Compare a median baseline, ridge regression, and polynomial features + Lasso. Three-fold grouped cross-validation searches ridge regularization and Lasso degree/regularization; model selection uses dollar MAE. Polynomial terms apply only to standardized year and mileage; categorical attributes remain separately one-hot encoded.

The test partition is excluded from model fitting and hyperparameter tuning. Confirm performance on external or later-period data before operational use.

## Notebook

[Open the executed CRISP-DM notebook](prompt_II.ipynb) for data preparation, charts, model comparisons, coefficient interpretation, the dealer report, and actionable recommendations.

## Run the analysis

Use Python 3.13. Download and extract `vehicles.csv` from the [assignment dataset archive](https://mo-pcco.s3.us-east-1.amazonaws.com/BH-PCMLAI-R2/module11/practical_application_II_starter.zip). Place it in a local `data/` folder beside the notebook, or set the `VEHICLES_CSV` environment variable to its full path. The dataset is excluded from Git.

From the repository folder:

```sh
python -m pip install -r requirements.txt
python -m pip install notebook
python -m notebook prompt_II.ipynb
```

Select the Python environment containing the dependencies and run all cells in order. Model tuning can take time depending on hardware. The random seed is 42. Charts, evaluation tables, and the dealer report are displayed inside the notebook; no separate report or results files are generated.

The notebook also recognizes the original dataset location in the supplied certification workspace. The README summarizes the saved run; review its numerical summary if you rerun the analysis with different data or settings.
