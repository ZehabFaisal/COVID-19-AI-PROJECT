# COVID-19 AI/ML Project

## Overview

This project performs data analysis and machine learning on the WHO COVID-19 global daily dataset. The Jupyter notebook (`AiLabProject.ipynb`) explores global trends, cleans the data, and trains multiple regression models to predict `New_cases` using cumulative case/death counts as features.

## Dataset

- **File:** `WHO-COVID-19-global-daily-data.csv` 
- **Source:** World Health Organization (WHO)
- **Size:** ~472,560 rows × 8 columns (~21 MB)
- **Coverage:** 240 countries across 7 WHO regions (EUR, AMR, AFR, WPR, EMR, SEAR, OTHER)
- **Date Range:** 01/01/2021 - 09/09/2024

### Columns
| Column | Description |
| --- | --- |
| `Date_reported` | Date of report (MM/DD/YYYY) |
| `Country_code` | ISO country code |
| `Country` | Country name |
| `WHO_region` | WHO region |
| `New_cases` | New confirmed cases reported that day |
| `Cumulative_cases` | Total confirmed cases to date |
| `New_deaths` | New confirmed deaths reported that day (dropped in preprocessing) |
| `Cumulative_deaths` | Total confirmed deaths to date | 

## Project Structure

```
COVID-19/
├── AiLabProject.ipynb                # Main analysis & ML notebook
├── WHO-COVID-19-global-daily-data.csv # Dataset
└── README.md                         # Project documentation
```

## Workflow (as implemented in the notebook)

1. **Setup** - Imports (`pandas`, `numpy`, `seaborn`, `matplotlib`, `sklearn`)
2. **Data Loading** - Reads `WHO-COVID-19-global-daily-data.csv` from the same directory
3. **Inspection** - `shape`, `head()`, `tail()`, `info()`, `dtypes`, `describe()`, null checks
4. **Missing Value Analysis** - Visualized with heatmaps
5. **Cleaning** - `New_deaths` column dropped; `New_cases` forward-filled (`ffill`); rows with remaining nulls dropped for modeling
6. **EDA** - Line plots (global trends), bar plots (top countries), boxplots (outliers), pie charts, correlation heatmap
7. **Feature Selection** - Features: `Cumulative_cases`, `Cumulative_deaths` | Target: `New_cases`
8. **Train/Test Split** - 80% training, 20% testing (`random_state=42`)
9. **Model Training** - Linear Regression, KNN Regressor, Decision Tree, Random Forest, Gradient Boosting
10. **Evaluation** - R², MSE, MAE with model comparison table
11. **Best Model Visualization** - Actual vs Predicted scatter plot with ideal line

## Dependencies

You'll need the following Python packages:

- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`
- `scikit-learn`
- `jupyter` (or `jupyterlab`)

## How to Run in VS Code Terminal

### 1) Open the project in VS Code
Open `G:\AI-PROJECTS\COVID-19` as your workspace folder.

### 2) Create and activate a virtual environment (recommended)

**Windows (PowerShell):**
```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**Windows (Command Prompt):**
```cmd
python -m venv .venv
.\.venv\Scripts\activate.bat
```

### 3) Install required packages
```bash
pip install --upgrade pip
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

### 4) Run the notebook

**Option A: VS Code Jupyter (easiest)**
1. Install the "Jupyter" extension in VS Code
2. Open `AiLabProject.ipynb`
3. Select your `.venv` Python kernel
4. Run cells with `Shift+Enter` (or Run All)

**Option B: Jupyter Notebook in terminal**
```bash
jupyter notebook
```
This will open a browser window. Navigate to `AiLabProject.ipynb` and run it.

**Option C: JupyterLab**
```bash
jupyter lab
```

### 5) (Optional) Convert notebook to a Python script and run it
If you want to run everything from the terminal without the notebook UI:

```bash
jupyter nbconvert --to script AiLabProject.ipynb
python AiLabProject.py
```

> Note: Plotting cells (`plt.show()`) will open windows when running as a script. If you're on a headless environment, you can replace them with `plt.savefig()`.

## Notes & Tips

- The notebook has an old commented path (`C:\Users\...`). The active code already uses `pd.read_csv("WHO-COVID-19-global-daily-data.csv")` which works since the CSV is in the same folder.
- The dataset is large. Some visualizations (like heatmaps on full data) can be memory-intensive - the notebook mitigates this by plotting on subsets where appropriate.
- Model evaluation compares all five regressors and selects the best by R² for the "Actual vs Predicted" plot.
- If you see SSL/certificate issues when installing packages, try `pip install --trusted-host pypi.org --trusted-host files.pythonhosted.org ...`

## Results

After running the notebook, you'll see:
- Data cleaning summaries and null visualizations
- EDA visualizations (trends, top countries, distributions, correlations)
- A performance comparison table for all models (sorted by R²)
- An Actual vs Predicted plot for the best-performing model
