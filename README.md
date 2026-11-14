# AI101-mini-project.
# Fish Weight Prediction.

An IIT Ropar AI101 mini-project that predicts a fish's weight in grams from its species and physical measurements using linear regression.

## Team

Team number: **54**

| Member | GitHub username | Lead role | Contribution |
| --- | --- | --- | --- |
| Aryan Yadav | AryanIITrpr1704 | Documentation | Added the idea of volume feature and created this ReadMe file and requirements |
| Ayush Kumar | 2026eeb1331-create | Execution | Created the repository, ran code multiple times and coded the data preprocessing, training plots, and requirements |
| Harshit Verma | hv-iitrpr | Presentation | Creating the visual structure and mechanism of the project via slide decks |
| Lokesh Chabdal | Lokesh2208 | Video | Constructed the video to briefly explain the working of project |

## Project files

| File | Purpose |
| --- | --- |
| [AI101mini.ipynb](AI101mini.ipynb) | Data checks, model training, plots, and test results |
| [Fish.csv](Fish.csv) | Fish Market dataset included in the repo |
| [requirements.txt](requirements.txt) | Pinned Python packages for the notebook |


## Dataset

The notebook reads 159 fish records across seven species. It checks for missing values and flags potential outliers with the interquartile range rule. The original split retains all rows, including one recorded weight of 0 g. The data comes from the [Fish Market dataset on Kaggle](https://www.kaggle.com/datasets/vipullrathod/fish-market).

| Column | Role |
| --- | --- |
| `Species` | Categorical input |
| `Length1`, `Length2`, `Length3` | Three fish length measurements in centimetres |
| `Height`, `Width` | Body measurements in centimetres |
| `Weight` | Prediction target in grams |

## Setup and run(2 methods)

*Method 1* :

Setup video for method 2(paste the link in the browser):
```
https://github.com/user-attachments/assets/f146950e-31f7-441c-8858-34baeaa2bbc5
```

1. Create a folder with any name you want
2. Open that folder in the VS code
3. IMPORTANT: now you need to trust your folder ,by clicking on 'manage' and then clicking on trust
4. Now in the VS code terminal(to open it press Ctrl+` ) paste the below given code
```
git clone https://github.com/2026eeb1331-create/AI101-mini-project
cd AI101-mini-project
pip install -r requirements.txt
code AI101mini.ipynb

```
5. Now select kernel from the top right of the interface
6. Now click on run all

   
*Method 2*:
Setup and Run Video(paste the link in the browser):
```
https://github.com/user-attachments/assets/b3100227-0ea1-4e50-ad6f-4e5c974872d5

```
The notebook was verified with Python 3.12.14 and the pinned packages in `requirements.txt`. The original team notebook used Python 3.14.6.
1. Open our AI101-mini-project github repository
2. Click on code (green button) and go on local, and then download zip.
3. Extract the folder
4. Open VS code and open our project folder in it and view the code
5. Install the required versions as mentioned in requirements.txt
6. Click on kernel and then click on python environments and select the python environment.
7. For this , the team has used python 3.14.6, so we would encourage the same
8. IMPORTANT: keep 'Fish.csv' beside the ipynb file so that the relative path resolves

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

The addition of volume proxy helped the model understand more about the dataset and got more idea of the overall fish size, this helped in the reduction of MAE, RMSE, negative weight prediction and we see a rise in the model's r2 score.

The plot comes from running the notebook. Add a screenshot of your own **Run All** output showing the final comparison table before submitting.

## Limitations

The evaluation covers one split of a small dataset. The volume experiment is a comparison on that split. Fish shape varies by species, and the volume proxy approximates size. The volume model still produces two negative test predictions. Predictions for unfamiliar species and sizes need further evaluation.

## Presentation and demo

- **Five-slide presentation** in this GithHub Repository  
- **Demo video, at most five minutes** Link 1 attach video link here

## AI-use disclosure

ChatGPT reviewed the notebook, suggested the volume feature, corrected the RMSE table label, and helped draft this README. The updated notebook was rerun against the repo's `Fish.csv` to check the results above.
