# Forest Cover Type Prediction

Predicting the forest cover type of a patch of land in the Roosevelt National Forest, Colorado, from cartographic features such as elevation, slope, hillshade and distance to water.

The task is a 7-class classification problem: each sample belongs to exactly one of seven cover types, and the goal is to predict which one.

## Dataset

`train.csv` — 15,120 rows and 56 columns:

| Column group | Count | Notes |
| --- | --- | --- |
| `Id` | 1 | Row identifier |
| Continuous features | 10 | Elevation, Aspect, Slope, distances to hydrology/roads/fire points, three hillshade indices |
| `Wilderness_Area1`–`4` | 4 | One-hot encoded wilderness areas |
| `Soil_Type1`–`40` | 40 | One-hot encoded soil types |
| `Cover_Type` | 1 | Target, values 1–7 |

The data is perfectly balanced (2,160 samples per class) and has no missing values or duplicate rows.

The dataset is the [Covertype dataset](https://archive.ics.uci.edu/dataset/31/covertype) from the UCI Machine Learning Repository.

## Approach

1. **Data understanding** — shape, dtypes, summary statistics, missing values, duplicates, class balance.
2. **Exploratory data analysis** — target distribution, histograms and boxplots of the continuous features, correlation heatmap, wilderness area counts.
3. **Preprocessing** — 80/20 stratified train/test split (`random_state=42`); `StandardScaler` fitted on the training set for the distance- and margin-based models.
4. **Modelling** — six classifiers compared on the same split.
5. **Hyperparameter tuning** — `GridSearchCV` (3-fold) over the random forest.
6. **Evaluation** — classification reports, weighted precision/recall/F1, confusion matrices, feature importances.

## Results

Untuned models, 80/20 hold-out split:

| Model | Accuracy | Precision | Recall | F1 (weighted) |
| --- | --- | --- | --- | --- |
| Logistic Regression | 0.6918 | 0.6892 | 0.6918 | 0.6891 |
| Decision Tree | 0.7930 | 0.7915 | 0.7930 | 0.7921 |
| KNN (k=5) | 0.7675 | 0.7617 | 0.7675 | 0.7628 |
| SVM (RBF) | 0.7262 | 0.7240 | 0.7262 | 0.7234 |
| Gradient Boosting | 0.8075 | 0.8044 | 0.8075 | 0.8034 |
| **Random Forest** | **0.8598** | **0.8570** | **0.8598** | **0.8571** |

Tuned random forest (`GridSearchCV`, best of 24 candidates × 3 folds):

- Best parameters: `n_estimators=200`, `max_depth=30`, `min_samples_split=2`, `min_samples_leaf=1`
- Best cross-validation accuracy: 0.8569
- **Test accuracy: 0.8687**, weighted precision 0.8663, weighted recall 0.8687, weighted F1 0.8663

Elevation is by far the strongest single predictor, followed by horizontal distance to roadways and fire points.

## Repository contents

```
PRCA - 1005  Forest type cover Prediction.ipynb   # full analysis, outputs stripped
requirements.txt                                   # Python dependencies
```

## Running it

```bash
pip install -r requirements.txt
```

Place `train.csv` in the same directory as the notebook (it is not committed to this repository), then open the notebook and run all cells.

## Known issues and next steps

- `Id` is currently used as a model feature. It is a row identifier with no predictive meaning, yet it ranks third in the random forest feature importances — dropping it is the first thing to try.
- The soil-type section looks for columns prefixed `Soil_type`, but the actual columns are `Soil_Type1`–`Soil_Type40`, so it finds zero columns and the soil analysis is empty. Fixing the prefix will let the notebook describe soil coverage.
- Only the random forest is tuned. Gradient boosting (0.8075 untuned) is a reasonable candidate for the same treatment.
- Results are from a single hold-out split. Cross-validated scores would make the comparison more robust.
- No trained model is persisted; adding a `joblib` dump of the final pipeline would make the work reusable.
