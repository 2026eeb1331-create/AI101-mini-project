# AI101-mini-project
# Fish Weight Prediction

An IIT Ropar AI101 mini-project that predicts a fish's weight in grams from its species and physical measurements using linear regression.

## Team

Team number: **[Add team number]**

| Member | GitHub username | Lead role | Contribution |
| --- | --- | --- | --- |
| [Name] | [Username] | Documentation | [Describe completed work] |
| [Name] | [Username] | Setup and execution | [Describe completed work] |
| [Name] | [Username] | Presentation | [Describe completed work] |
| [Name] | [Username] | Video | [Describe completed work] |

## Project files

| File | Purpose |
| --- | --- |
| [AI101mini.ipynb](AI101mini.ipynb) | Data checks, model training, plots, and test results |
| [Fish.csv](Fish.csv) | Fish Market dataset included in the repo |
| [requirements.txt](requirements.txt) | Pinned Python packages for the notebook |
| [results/actual_vs_predicted.png](results/actual_vs_predicted.png) | Plot produced by running the notebook |

## Dataset

The notebook reads 159 fish records across seven species. It checks for missing values and flags potential outliers with the interquartile range rule. The original split retains all rows, including one recorded weight of 0 g. The data comes from the [Fish Market dataset on Kaggle](https://www.kaggle.com/datasets/vipullrathod/fish-market).

| Column | Role |
| --- | --- |
| `Species` | Categorical input |
| `Length1`, `Length2`, `Length3` | Three fish length measurements in centimetres |
| `Height`, `Width` | Body measurements in centimetres |
| `Weight` | Prediction target in grams |

## Setup and run

The steps below use PowerShell on Windows. The notebook was verified with Python 3.12.14 and the pinned packages in `requirements.txt`. The original team notebook used Python 3.14.6.

```powershell
git clone https://github.com/2026eeb1331-create/AI101-mini-project.git
cd AI101-mini-project
python --version
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

1. Open the `AI101-mini-project` folder in VS Code. Install the **Python** and **Jupyter** extensions if needed.
2. Open `AI101mini.ipynb`. Choose **Select Kernel → Python Environments** and select the interpreter from `.venv`.
3. Choose **Run All**. Keep `Fish.csv` beside the notebook so its relative path resolves.
4. Scroll to the final code cell to see the three-model comparison.

On macOS or Linux, use `.venv/bin/python -m pip install -r requirements.txt` after creating the virtual environment.

## Method

1. Split the data into **127 training fish** and **32 test fish** using an 80/20 split and `random_state=42`.
2. Encode species with `OneHotEncoder` inside each pipeline. Fit the preprocessing and the regression on the training rows.
3. Compare two linear regressions. The baseline uses the original measurements, and the scaled model applies `StandardScaler` to the five numerical inputs.
4. Fit a third model on the same training fish. It uses the original inputs and adds `VolumeProxy = Length3 * Height * Width` as an approximate body-size feature.
5. Measure performance on the same 32 test fish. The split and target stay fixed across the comparison.

## Expected output

| Model | Test MAE (g) | Test RMSE (g) | Test R² | Negative predictions |
| --- | ---: | ---: | ---: | ---: |
| Unscaled baseline | 65.30 | 83.71 | 0.9507 | 5 |
| Scaled linear regression | 65.30 | 83.71 | 0.9507 | 5 |
| Linear regression with volume proxy | 43.73 | 58.23 | 0.9762 | 2 |

MAE is the average absolute error in grams. RMSE gives larger errors more influence. The unscaled and scaled regressions agree to rounding precision. Ordinary least squares can adjust its coefficients and intercept when the inputs are standardized. On this split, adding the body-size feature reduces test MAE by about 21.57 g.

![Actual versus predicted weight for the original scaled regression on the held-out fish](results/actual_vs_predicted.png)

The plot comes from running the notebook. Add a screenshot of your own **Run All** output showing the final comparison table before submitting.

## Limitations

The evaluation covers one split of a small dataset. The volume experiment is a comparison on that split. Fish shape varies by species, and the volume proxy approximates size. The volume model still produces two negative test predictions. Predictions for unfamiliar species and sizes need further evaluation.

## Presentation and demo

- **Five-slide presentation** [Add slide link]
- **Demo video, at most five minutes** [Add video link]

## AI-use disclosure

ChatGPT reviewed the notebook, suggested the volume feature, corrected the RMSE table label, and helped draft this README. The updated notebook was rerun against the repo's `Fish.csv` to check the results above. Add any other AI assistance your team used and record the checks each member actually performed.
