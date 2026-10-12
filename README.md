# Heart Disease Prediction using Machine Learning

An educational machine learning project that combines exploratory data analysis, comparison of five classification algorithms, and an interactive Streamlit application.

The app takes 11 inputs, processes them using saved model artifacts, and displays a binary classification labelled **High Risk of Heart Disease** or **Low Risk of Heart Disease**.

> This project is an educational demonstration, not a medical diagnostic tool. Its output labels are model predictions, not clinically validated risk estimates or medical advice.

## Project highlights

- Explore a dataset containing 918 records and 11 input features.
- Inspect distributions, categorical relationships, and numerical correlations.
- Prepare data through value replacement, categorical encoding, and scaling.
- Compare Logistic Regression, K-Nearest Neighbors, Gaussian Naive Bayes, Decision Tree, and Support Vector Machine classifiers.
- Save the selected Logistic Regression model, scaler, and feature order with Joblib.
- Connect the saved artifacts to a Streamlit interface for individual predictions.

## Dataset

The project uses `heart.csv`, containing **918 rows and 12 columns**, including the binary target `HeartDisease`. There are 508 records labelled 1 and 410 labelled 0.

| Feature | Description |
|---|---|
| Age | Age in years |
| Sex | M or F |
| ChestPainType | Chest pain category: ATA, NAP, TA, or ASY |
| RestingBP | Resting blood pressure, in mm Hg |
| Cholesterol | Cholesterol, in mg/dL |
| FastingBS | Indicator for fasting blood sugar above 120 mg/dL |
| RestingECG | Resting ECG category: Normal, ST, or LVH |
| MaxHR | Maximum heart rate |
| ExerciseAngina | Exercise-induced angina: Y or N |
| Oldpeak | ST depression value |
| ST_Slope | ST slope category: Up, Flat, or Down |
| HeartDisease | Binary target label |

The local file has the same schema and record count as the [Heart Failure Prediction Dataset on Kaggle](https://www.kaggle.com/datasets/fedesoriano/heart-failure-prediction). The original download source is not recorded in the project; confirm the source and applicable dataset terms before redistribution. The target used in this project is `HeartDisease`.

## Model comparison

The notebook uses an 80/20 train/test split with `random_state=42`.

The following are the project's **reported experimental results**, supplied by the author. They are not independently validated clinical performance estimates.

| Model | Accuracy | F1 score |
|---|---:|---:|
| Logistic Regression | **86.96%** | **0.8857** |
| K-Nearest Neighbors | 86.41% | 0.8815 |
| Gaussian Naive Bayes | 85.33% | 0.8683 |
| Decision Tree | 79.35% | 0.8155 |
| Support Vector Machine | 84.78% | 0.8679 |

Logistic Regression has the highest reported accuracy and F1 score in this comparison and is the model used by the Streamlit app. Accuracy measures the fraction of correctly classified records. The reported F1 score balances precision and recall for target class 1. Results describe this experiment and should not be interpreted as expected performance on new patient populations.

## Application workflow

```text
Enter 11 feature values
         |
         v
Encode categories and align the 15 model features
         |
         v
Apply the saved scaler
         |
         v
Run the saved Logistic Regression classifier
         |
         v
Display the predicted class
```

The interface includes sliders, numeric inputs, dropdown menus, and a Predict button. It displays a class label rather than a probability. The current app does not save submitted inputs to a database or file.

## Repository structure

Keep these files together in the repository root:

```text
heart-disease-prediction/
|-- app.py
|-- Heart.ipynb
|-- heart.csv
|-- Logistic_Regression_heart.pkl
|-- Scaler.pkl
|-- columns.pkl
|-- heartimage-removebg-preview.png
|-- README.md
`-- requirements.txt
```

| File | Purpose |
|---|---|
| `app.py` | Streamlit interface and prediction workflow |
| `Heart.ipynb` | Data exploration, preprocessing, model comparison, evaluation, and artifact export |
| `heart.csv` | Dataset used in the notebook |
| `Logistic_Regression_heart.pkl` | Saved Logistic Regression classifier |
| `Scaler.pkl` | Saved feature scaler |
| `columns.pkl` | Ordered list of model input columns |
| `heartimage-removebg-preview.png` | Image displayed in the app |
| `requirements.txt` | Dependencies for the app and notebook |

## Run locally

Use Python 3.12 or 3.13 and open a terminal in the project folder.

### 1. Create an environment

```bash
python -m venv .venv
```

Activate it on Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

On macOS or Linux:

```bash
source .venv/bin/activate
```

### 2. Install dependencies

```bash
python -m pip install -r requirements.txt
```

The dependency file pins the inspected local versions of the analysis packages and scikit-learn 1.7.2, matching the supplied model artifacts. Streamlit 1.52 or later within major version 1 is required for the app's `text_alignment` arguments, as documented in the [Streamlit release notes](https://docs.streamlit.io/develop/quick-reference/release-notes/2025#version-1520). This is a dependency specification, not a fully locked environment; a fresh installation has not been verified.

### 3. Launch the application

```bash
python -m streamlit run app.py
```

Open the local address printed in the terminal, enter example values, and select **Predict**.

**Run the command from the project folder.** The app loads its model files and image using relative paths. Moving these files into subfolders requires corresponding changes to the paths in `app.py`.

### 4. Explore the notebook

```bash
python -m notebook Heart.ipynb
```

The notebook includes the analysis, model-comparison loop, and export commands. Running the export cell overwrites the three saved artifacts in the working directory. Keep the classifier, scaler, and feature list from the same training run together. Load only trusted Joblib/pickle files.

## Technology stack

Python, pandas, NumPy, scikit-learn, Joblib, Streamlit, Matplotlib, Seaborn, and Jupyter Notebook.

## Demonstration

A short screen recording can demonstrate entering fictional example values, selecting Predict, and viewing the result. Narration is optional. Screenshots or a video link can be added to this README once those media are available.

## Author

**Sharf Ur Rehman**  
[GitHub profile](https://github.com/sharfurrehman)
