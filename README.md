# california-housing-regression

Predicting house values in California with Linear Regression, Ridge and Lasso, and checking whether regularization improves the result.

## Questions

1. Does regularization (Ridge, Lasso) give better predictions than plain Linear Regression on this dataset?
2. Which features matter most for house prices?

## Data

The California Housing dataset from scikit-learn (`fetch_california_housing`), based on the 1990 U.S. census. It has 20,640 districts and 8 numeric features, for example median income, house age, average number of rooms and the location (latitude, longitude). The target is the median house value in 100,000 dollars.

The data is downloaded by scikit-learn when the notebook runs, so it is not stored in this repository.

## Method

- Train/test split (80/20) **before** any scaling or model selection. The test set is used only once, for the final comparison.
- `StandardScaler` and the model in one `Pipeline`, so the scaling is learned from the training data only.
- `alpha` for Ridge and Lasso chosen with 5-fold cross-validation on the training data (11 values from 0.001 to 100).
- Evaluation with RMSE (in the unit of the target), MSE and R².

## Results

- All three models perform almost the same: test RMSE of about 0.75 (predictions are off by about 75,000 dollars on average) and R² of about 0.58. The exact table is in the notebook.
- Regularization does not improve the result here. Training and test errors are very close, so Linear Regression does not overfit: with 8 features and more than 16,000 training rows it is already stable.
- Income (`MedInc`) and location (`Latitude`, `Longitude`) are the most important features.
- With a larger `alpha` (for example 0.1), Lasso keeps only a few features, but the error is clearly higher.

## Limitations

- House values in the data are capped at 500,000 dollars, so very expensive districts cannot be predicted correctly.
- The effect of location on price is not linear. Non-linear models (random forest, gradient boosting) or new features such as the distance to the coast would probably reduce the error.

## Files

```
california-housing-regression/
├── california_housing_regression.ipynb   # analysis notebook
├── README.md
└── requirements.txt
```

## How to run

```
git clone https://github.com/mina-motaghinasab/california-housing-regression.git
cd california-housing-regression
pip install -r requirements.txt
jupyter notebook california_housing_regression.ipynb
```

## Use of AI tools

This started as my own practice project: I wrote the first version of the code, which trained Linear Regression, Ridge and Lasso and compared different values of `alpha`. I used Claude (an AI assistant) to review it. Following its review, the scaling was moved into a pipeline after the train/test split, `alpha` is now chosen with cross-validation instead of the test error, and the results table is built from the code. Claude also helped write the explanations in the notebook and this README. I can explain every step of the code.

## Author

Mina Motaghinasab, M.Sc. Data Science student at TU Dortmund
