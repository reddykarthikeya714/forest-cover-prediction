# Forest Cover Type Prediction

A supervised machine-learning project that predicts one of **seven forest cover classes** from cartographic and environmental features.

## Project at a glance

| Item | Details |
|---|---|
| Problem type | Multiclass classification |
| Domain | Environmental / geospatial data |
| Target | Forest cover type (7 classes) |
| Main model | Tuned Random Forest |
| Reported result | 86.9% accuracy in the notebook's evaluation setup |

## Objective

Use the available terrain and cartographic measurements to classify the forest cover category. The project follows a practical machine-learning workflow, from understanding the data through model comparison and evaluation.

## Workflow

1. Load the dataset and inspect its structure.
2. Perform exploratory data analysis to understand feature distributions and target classes.
3. Prepare the data and apply feature scaling where appropriate.
4. Train and compare six classification algorithms.
5. Tune a Random Forest classifier.
6. Evaluate the selected model using the notebook's evaluation process.

## Result

The notebook reports **86.9% accuracy** for the tuned Random Forest evaluation. This figure reflects the notebook's particular split and setup; it should not be interpreted as a guarantee of performance on new geographic areas.

## Tools and technologies

- Python, Jupyter Notebook
- Pandas, NumPy
- Matplotlib, Seaborn
- Scikit-learn

## Skills demonstrated

Exploratory data analysis · Data cleaning and preparation · Feature scaling · Multiclass classification · Model comparison · Random Forest · Hyperparameter tuning · Model evaluation

## Run locally

1. Clone this repository.
2. Open the notebook using Jupyter Notebook, JupyterLab, or Google Colab.
3. Install the libraries imported in the notebook.
4. Update the dataset path to the location on your computer.
5. Run the notebook cells in order.

## Limitations and next steps

- Validate the model on a clearly separated hold-out dataset and, where possible, data from different geographic regions.
- Review class-wise precision, recall, and F1-score in addition to overall accuracy.
- Document the final feature set and tuning procedure for reproducibility.

---

*Portfolio project | Data Science · Machine Learning · Environmental Classification*
