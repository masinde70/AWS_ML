
---

![correlation_temp](img/sagemaker.jpeg) ![temp](img/autogluon.png)

# Predict Bike Sharing Demand with AutoGluon

This project demonstrates how to use AWS SageMaker and AutoGluon to predict bike sharing demand, using the "Bike Sharing Demand" dataset from Kaggle.

## Environment Setup

- **Instance Type:** Use an AWS SageMaker instance of type ml.t3.medium (2 vCPU + 4 GiB RAM).
- **Kernel:** Python 3 (MXNet 1.8 Python 3.7 CPU Optimized)

## Installation

Install all required packages (uncomment if running for the first time):

```bash
# !pip install -U pip
# !pip install -U setuptools wheel
# !pip install -U "mxnet<2.0.0" bokeh==2.0.1
# !pip install autogluon --no-cache-dir
# !pip install kaggle
# !pip install python-dotenv
```
> Note: Use --no-cache-dir if you run into memory issues on small AWS instances.

## Kaggle API Setup

1. Create a Kaggle account and generate an API token.
2. Store your credentials in a `.env` file:
    ```
    KAGGLE_USERNAME=your_kaggle_username
    KAGGLE_KEY=your_kaggle_key
    ```
3. The notebook will set up the `.kaggle/kaggle.json` file automatically.

## Downloading the Data

Download and unzip the dataset using the Kaggle API:

```bash
!kaggle competitions download -c bike-sharing-demand
!unzip -o bike-sharing-demand.zip
```

## Data Exploration

- Load the datasets (`train.csv`, `test.csv`, `sampleSubmission.csv`) with pandas.
- Initial data exploration includes viewing head, info, and descriptive statistics.

## Training the Model

- **Framework:** [AutoGluon TabularPredictor](https://auto.gluon.ai/)
- **Label to Predict:** `count`
- **Ignored Columns:** `casual`, `registered` (not present in test data)
- **Evaluation Metric:** `root_mean_squared_error`
- **Training Time Limit:** 10 minutes (600 seconds)
- **Preset:** `best_quality` for maximum accuracy

```python
from autogluon.tabular import TabularPredictor

predictor = TabularPredictor(
    label="count",
    eval_metric='root_mean_squared_error',
    problem_type='regression',
    learner_kwargs={'ignored_columns': ['casual', 'registered']}
).fit(
    train_data=train,
    time_limit=600,
    presets="best_quality"
)
```

## Model Evaluation

- The notebook summarizes the model performance and lists all trained models.
- The best model is selected automatically by AutoGluon, typically a weighted ensemble.

## Output

AutoGluon saves the leaderboard of models and their validation scores. The best model can be used for predictions on the test set.

## References

- [AutoGluon Documentation](https://auto.gluon.ai/)
- [Bike Sharing Demand Kaggle Competition](https://www.kaggle.com/c/bike-sharing-demand)

---

**Note:** For more details, see the notebook [`project.ipynb`](project.ipynb).

---

