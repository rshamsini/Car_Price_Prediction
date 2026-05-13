# Car Price Prediction

Machine learning major project completed for **Verzeo**. The project predicts the resale price of used cars using historical car listing data and a Random Forest regression model.

## Project Objective

The goal of this project is to estimate the price of a used car from its technical and listing details. The notebook performs exploratory analysis, data cleaning, feature preparation, model training, hyperparameter tuning, and final prediction.

## Repository Contents

| File | Description |
| --- | --- |
| `Verzeo_ML_MajorProject.ipynb` | Main Jupyter/Colab notebook containing data analysis, preprocessing, training, and prediction steps. |
| `README.md` | Project documentation and setup guide. |
| `LICENSE` | MIT license. |

## Dataset

The notebook expects the Verzeo car price dataset files:

- `Data_Train (1).xlsx`
- `Data_Test (1).xlsx`

In the original notebook, these files are read from Google Drive:

```python
data = pd.read_excel("/content/drive/My Drive/Data_Train (1).xlsx")
datatest = pd.read_excel("/content/drive/My Drive/Data_Test (1).xlsx")
```

The training dataset contains `6019` records with columns such as:

- `Name`
- `Location`
- `Year`
- `Kilometers_Driven`
- `Fuel_Type`
- `Transmission`
- `Owner_Type`
- `Mileage`
- `Engine`
- `Power`
- `Seats`
- `New_Price`
- `Price`

`Price` is the target variable.

## Methodology

1. Loaded the training and test datasets from Excel files.
2. Removed the `New_Price` column because it contains many missing values.
3. Cleaned numeric columns that originally included text units:
   - `Mileage`: removed `kmpl` and `km/kg`
   - `Engine`: removed `CC`
   - `Power`: removed `bhp`
4. Filled missing values and converted cleaned columns to numeric format.
5. Removed rare categories from selected categorical columns, including:
   - `Owner_Type = Fourth & Above`
   - `Fuel_Type = LPG`
   - `Fuel_Type = Electric`
6. Selected numerical features for model training:
   - `Year`
   - `Kilometers_Driven`
   - `Mileage`
   - `Engine`
   - `Power`
   - `Seats`
7. Split the data into training and validation sets using a 67:33 split.
8. Trained a `RandomForestRegressor`.
9. Tuned model parameters using `GridSearchCV`.
10. Used the trained model to predict used car prices.

## Model

The final model uses Scikit-learn's `RandomForestRegressor`.

Best parameters recorded in the notebook:

```text
criterion: mse
max_depth: 10
min_samples_leaf: 3
min_samples_split: 3
n_estimators: 1000
```

## Results

The model achieved the following results in the notebook:

| Metric | Value |
| --- | --- |
| GridSearchCV best score | `0.8275` |
| Validation R2 score | `0.90` |

This means the trained Random Forest model was able to explain about 90% of the variance in car resale prices on the validation split.

## Setup Instructions

### 1. Clone the Repository

```bash
git clone <repository-url>
cd Car_Price_Prediction
```

### 2. Create a Virtual Environment

```bash
python -m venv .venv
```

Activate it:

```bash
# Windows
.venv\Scripts\activate

# macOS/Linux
source .venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install pandas numpy matplotlib seaborn scikit-learn openpyxl jupyter
```

### 4. Add the Dataset

Place the dataset files in the project folder:

```text
Data_Train (1).xlsx
Data_Test (1).xlsx
```

If you are running the notebook locally instead of Google Colab, update the dataset loading cells to:

```python
data = pd.read_excel("Data_Train (1).xlsx")
datatest = pd.read_excel("Data_Test (1).xlsx")
```

If you are running in Google Colab, upload the files to Google Drive and keep the original Drive paths, or adjust the paths to match your Drive folder.

### 5. Run the Notebook

Start Jupyter Notebook:

```bash
jupyter notebook
```

Open:

```text
Verzeo_ML_MajorProject.ipynb
```

Then run the cells from top to bottom.

## Conclusion

The project successfully trains a regression model to predict used car prices from cleaned vehicle attributes. The Random Forest Regressor performs well on the validation data, achieving a validation R2 score of approximately `0.90`.

## License

This project is licensed under the MIT License.
