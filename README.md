# DimensionalityReduction_Workshop

Project: Soil Health Prediction for Sustainable Agriculture

Short description
-----------------
This repository contains a professor-style workshop pipeline that performs dimensionality reduction and feature selection to predict the most suitable crop (label) from agronomic features (N, P, K, pH, temperature, humidity, rainfall) and additional fields from a second dataset. The analysis is packaged as a Jupyter notebook that demonstrates data harmonization, filtering, transforms, PCA, random-forest based importance scoring, and wrapper-based feature selection followed by model evaluation.

Repository structure
--------------------
- `Dimensionality_reduction.ipynb` — (alternate notebook)
- `DimensionalityReduction_Workshop.ipynb` — main notebook implementing the pipeline
- `Data/` — contains source CSV files used by the notebook:
	- `Crop_recommendation 2.csv`
	- `Crop_recommendationV2 1.csv`
	- `Soil Nutrients.csv` (additional data)

Quick start (Windows PowerShell)
-------------------------------
1. Create and activate the virtual environment (optional but recommended):

```powershell
# from repository root
python -m venv .venv; .\.venv\Scripts\Activate.ps1
```

2. Install the minimal Python dependencies:

```powershell
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install numpy pandas matplotlib scikit-learn jupyter
```

3. Launch Jupyter and open the main notebook:

```powershell
.\.venv\Scripts\python.exe -m jupyter notebook
```

Open `DimensionalityReduction_Workshop.ipynb` and run the cells in order.

Notes about filenames
---------------------
- The notebook expects the CSV files under the `Data/` directory and uses these constants (present in the notebook):
	- `PATH_A = "./Data/Crop_recommendation 2.csv"`
	- `PATH_B = "./Data/Crop_recommendationV2 1.csv"`

If your filenames differ, update those constants at the top of the notebook.

What the notebook does (pipeline summary)
-----------------------------------------
1. Load and harmonize two CSV sources (union of columns).  
2. Numeric feature extraction and target separation.  
3. Missing-values-ratio filter and median imputation.  
4. Low-variance filter (VarianceThreshold).  
5. High-correlation filter (drop one of each highly correlated pair).  
6. Optional Box–Cox / Tukey transforms to reduce skew.  
7. PCA for descriptive compression and scree analysis.  
8. Random Forest (bootstrapped) for feature importances.  
9. Forward (SequentialFeatureSelector) and backward-style RFE wrapper selection.  
10. Model evaluation: Logistic Regression and Random Forest; metrics: Accuracy and macro-F1.

Troubleshooting
---------------
- If you see FileNotFoundError for `Crop_recommendation2.csv` or similar, check `PATH_B` at the top of the notebook and update it to the actual file name in `Data/`.  
- If Pylance in VS Code reports unresolved imports, ensure the notebook kernel matches the environment where packages were installed (see Quick start).  
- If you get selection errors like `n_features_to_select must be < n_features`, the notebook contains guards to choose sensible n_features based on the dataset size; run cells sequentially after loading the data.

Reproducibility and environment
--------------------------------
- The notebook sets `RANDOM_STATE = 42` for reproducible splits and RF runs.  
- Recommended minimal packages: `numpy`, `pandas`, `matplotlib`, `scikit-learn`, `jupyter`.

Results & report
----------------
The notebook contains plotted PCA scree, RF importance lists, selected feature sets, and evaluation tables that you can use in your group report and presentation. See the analysis section at the end of the notebook for interpretation and hypothesis testing notes.

Contributing
------------
If you want to extend the project:
- Add a `requirements.txt` or `environment.yml` for reproducible installs.
- Add unit tests for the transformer utilities.
- Add a small script to export the selected model as a pickle and a simple CLI to predict on new data.

License & contact
-----------------
Add your preferred license and contact information here (or keep as coursework material).

---
Generated/updated: README.md — provides quick start and pipeline overview for the project.