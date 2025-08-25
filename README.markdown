## Demand Forecasting in Retail Stores

Demand forecasting plays a crucial role in supply chain management and retail operations. Accurate forecasts ensure that the right product quantities are available at the correct time and location, preventing stockouts or overstocking.

## Introduction

This project leverages advanced neural networks and time-series forecasting techniques to address challenges in retail sales prediction. By integrating machine learning and deep learning methods, the project aims to demonstrate how businesses can optimize inventory management and maximize profitability.

## Project Goal
The objective is to build forecasting models capable of predicting 30 days of sales across 10 stores and 5 items, using both classical ML and modern deep learning architectures.

Models were trained with slightly different splitting strategies(tree models on random split,sequence models on time splits).For each RMSE was reported on held-out validation/test set.

## Dataset Access

The dataset used in this project comes from the Kaggle competition: 
[Store Item Demand Forecasting Challenge](https://www.kaggle.com/c/demand-forecasting-kernels-only/data).

Due to licensing restrictions, the dataset is **not included in this repository**.  
Please download it directly from Kaggle and place it in your working directory before running the notebooks.

⚠️ Note on Dataset Usage  

The original Kaggle dataset contains sales records for **10 stores × 50 items** over 5 years.  
However, training deep learning models (e.g., LSTM, N-BEATS, TFT) on the full dataset can take **hours** even with GPU acceleration.  

To make experiments feasible within Google Colab’s limited GPU resources,  
this project uses a **reduced version of the dataset (10 stores × 5 items)** for modeling and demonstration purposes.  

The full dataset can still be downloaded from Kaggle if you wish to reproduce results at scale.


## Dataset Description
Attributes:
Date: Sales record date
Store ID: Identifier for each store
Item ID: Identifier for each item
Sales: Number of units sold

Time Span:
January 1, 2013 → December 31, 2017

Preprocessing Steps:
✅ Removed duplicates (none found)
✅ Standardized date format
✅ Verified no missing values

## Exploratory Data Analysis (EDA)

EDA was performed in `main.ipynb` to explore the dataset before modeling.  
Key steps included:

- **Date Formatting & Sorting**: Converted `date` column to datetime format and sorted the dataset by `store`, `item`, and `date`.
- **Missing Date Check**: Verified continuity of the time series by checking for gaps in dates for sample store–item pairs.
- **Trend & Seasonality Decomposition**: Applied seasonal decomposition to visualize overall trends, seasonal patterns, and residuals in sales.
- **Stationarity & Correlation Checks**: Used ACF plots to analyze autocorrelations in sales.
- **Data Quality Checks**: Confirmed no missing values or null entries in the dataset.

These steps ensured the dataset was consistent, continuous, and ready for model training.

## Modeling Approach
Statistical Model
- SARIMAX: Tried as a baseline for time series forecasting. Performed reasonably well on single series but limited scalability across multiple store–item combinations.

Machine Learning Models
LightGBM
XGBoost
CatBoost

🤖 Deep Learning Models
LSTM: Demonstrated on 1 store × 1 item (since LSTMs are effective for single time series).
Results: Limited improvement → shifted focus to global models.
Global Deep Learning Models (Darts Library):
N-BEATS
Temporal Fusion Transformer (TFT)

Both are designed for multi-series forecasting, making them suitable for retail datasets with multiple stores and items.


## Evaluation

Horizon: 30 days
Metrics: RMSE

## Final Results

Among all the models tested, **N-BEATS achieved the lowest RMSE** and consistently outperformed classical ML models (LightGBM, XGBoost, CatBoost) as well as other deep learning approaches (LSTM, TFT).  

For the final submission, we retrained N-BEATS on the **entire dataset** (2013–2017) and generated forecasts for the **next 30 days** across all stores and items.

## References

Kaggle – Store Item Demand Forecasting Challenge


## Technologies Used

Python
Google Colab (for GPU acceleration)
Libraries: pandas, numpy, matplotlib, seaborn, scikit-learn, lightgbm, xgboost, catboost, darts, pytorch-lightning

## How to Run the Project
Run Locally (Jupyter Notebook)

Clone the Repository
git clone https://github.com/Surajit-maity1110/Retail-Demand-Forecasting

Install Dependencies
pip install -r requirements.txt

Run the Notebook
jupyter notebook main.ipynb

Dataset Access
Download the dataset directly from Kaggle: Store Item Demand Forecasting Challenge


## Contributing

Want to contribute to this project? Here’s how you can do it step by step:

**Fork the Repository**
Click the Fork button on the top-right of this GitHub repo to create a copy under your own GitHub account.

**Clone the Fork**
Download your forked project to your local machine.

**Create a New Branch**
Make a new branch where you'll write your changes. This keeps the main project stable.

**Make Your Changes**
Add or improve code, fix bugs, enhance documentation, or try new features.

**Commit and Push**
Save your changes and push them to your branch on GitHub.

**Create a Pull Request**
Go to your GitHub fork and click “Compare & pull request”. Add a clear title and description, then submit.

---

### License

This project is licensed under the MIT License - see the Licence file for details.