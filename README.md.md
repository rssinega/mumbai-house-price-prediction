# 🏠 Mumbai House Price Prediction

A machine learning project that predicts residential property prices in Mumbai and its surrounding areas (Thane, Kalyan, Dombivali, Nala Sopara, Mulund, Kurla, Sion, Ville Parle, etc.) using regression models.

## 📌 Overview

This project walks through a complete beginner-friendly ML workflow in a Jupyter Notebook:

1. Load and explore the dataset
2. Clean the data (remove duplicates, handle missing values)
3. Encode categorical features
4. Train and evaluate regression models
5. Compare model performance

## 📂 Project Structure

```
├── house_price.ipynb                    # Main notebook (EDA, cleaning, modeling)
├── mumbai-house-price-data-cleaned.csv  # Dataset
└── README.md
```

## 📊 Dataset

- **File:** `mumbai-house-price-data-cleaned.csv`
- **Size:** 8,917 rows × 15 columns (7,773 rows after removing 1,144 duplicates)

| Column | Description |
|---|---|
| `title` | Name of the project / property |
| `price` | Property price (target variable) |
| `area` | Area in sq. ft. |
| `price_per_sqft` | Price per square foot |
| `locality` | Neighbourhood (e.g. Kalyan, Thane, Sion) |
| `city` | City (Mumbai) |
| `property_type` | Type of property (e.g. Apartment) |
| `bedroom_num` | Number of bedrooms |
| `bathroom_num` | Number of bathrooms |
| `balcony_num` | Number of balconies |
| `furnished` | Furnished / Semi-Furnished / Unfurnished |
| `age` | Age of the property |
| `total_floors` | Total floors |
| `latitude` / `longitude` | Geographic coordinates |

## 🧹 Data Preprocessing

- **Duplicates:** Found and dropped 1,144 duplicate rows.
- **Missing values:** Filled the single missing value in `bedroom_num`, `bathroom_num`, `balcony_num`, `age`, `total_floors`, `latitude` and `longitude` with the column **median**.
- **Encoding:** One-hot encoded the `furnished` column using `pd.get_dummies`.
- **Feature selection:** Dropped `title`, `locality`, `city`, `property_type`, `total_floors`, the original `furnished` column, and the target `price`.
- **Train/test split:** 80% training / 20% testing (`random_state=42`).

### Final features

`area`, `price_per_sqft`, `bedroom_num`, `bathroom_num`, `balcony_num`, `age`, `latitude`, `longitude`, `Furnished`, `Semi-Furnished`, `Unfurnished`

**Target:** `price`

## 🤖 Models & Results

| Model | Train R² | Test R² |
|---|---|---|
| Linear Regression | 0.859 | 0.819 |
| Decision Tree Regressor | 1.000 | 0.937 |

## 🛠️ Tech Stack

- Python 3.13
- pandas
- scikit-learn
- Jupyter Notebook

## 🚀 Getting Started

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd <your-repo-folder>
   ```

2. **Install dependencies**
   ```bash
   pip install pandas scikit-learn jupyter
   ```

3. **Run the notebook**
   ```bash
   jupyter notebook house_price.ipynb
   ```

   Make sure the CSV file is in the same folder as the notebook.

## ⚠️ Limitations & Notes

- **Possible data leakage:** `price_per_sqft` is derived from `price` (price ÷ area), so using it as a feature gives the model information about the target. This likely inflates the R² scores. Removing it would give a more realistic estimate of model performance.
- **Overfitting:** The Decision Tree scores a perfect 1.0 on training data versus 0.937 on test data, a sign that it is memorizing the training set.
- Location is only represented by latitude/longitude; the `locality` column is not used.

## 🔮 Future Improvements

- Remove `price_per_sqft` and re-evaluate the models
- Tune Decision Tree hyperparameters (`max_depth`, `min_samples_leaf`) or use Random Forest / Gradient Boosting
- Use `locality` via one-hot or target encoding
- Add cross-validation and more metrics (MAE, RMSE)
- Add visualizations (price distribution, price by locality, correlation heatmap)
- Handle outliers in `price` and `area`
- Build a simple web app (Streamlit / Flask) for live predictions

## 📄 License

This project is for educational purposes. Add a license of your choice (e.g. MIT).
