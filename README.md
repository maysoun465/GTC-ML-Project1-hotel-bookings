# GTC ML Project 1 - Hotel Bookings (Data Cleaning & Preprocessing)

## 📌 Project Overview
This project is part of the **GTC ML Project 1 - Data Cleaning & Preprocessing Challenge**.  
The goal is to explore, clean, and preprocess the **Hotel Bookings** dataset to prepare it for further machine learning tasks.

---

## 📂 Repository Structure
- **`hotel_bookings.csv`** → The raw dataset provided for the project  
- **`hotel_bookings_cleaned.csv`** → The cleaned dataset after preprocessing  
- **`hotel_bookings.ipynb`** → Jupyter/Colab Notebook containing all steps:
  - Exploratory Data Analysis (EDA)  
  - Data Quality Report  
  - Handling Missing Values  
  - Removing Duplicates  
  - Outlier Detection & Treatment  
  - Fixing Data Types  
  - Feature Engineering  
  - Categorical Encoding  
  - Train/Test Split  
- **`README.md`** → Project description and instructions  

---

## ⚙️ Prerequisites
- Python 3.x  
- Google Colab or Jupyter Notebook  
- Libraries:  
  - `pandas`  
  - `numpy`  
  - `matplotlib`  
  - `seaborn`  
  - `missingno`  
  - `scikit-learn`  

---

## 🔑 Key Steps
1. **Exploratory Data Analysis (EDA)**  
   - Summary statistics  
   - Missing values analysis  
   - Outlier detection (boxplots, IQR)  

2. **Data Cleaning**  
   - Imputed missing values (`children`, `country`, `agent`, `company`)  
   - Removed duplicates  
   - Removed negative ADR values  
   - Capped extreme outliers (`ADR` at 500, `Lead Time` at 365)  
   - Converted date columns to datetime  

3. **Feature Engineering**  
   - `total_guests` (adults + children + babies)  
   - `total_nights` (weekend + week nights)  
   - `is_family` flag  

4. **Encoding**  
   - One-Hot Encoding for low-cardinality categorical features  
   - Frequency Encoding for high-cardinality `country` feature  

5. **Train-Test Split**  
   - 80% training, 20% testing (random_state=42 for reproducibility)  

---

## 📊 Data Quality Summary
| Column                 | Missing Values | Missing %  | Outliers Detected | Notes                              |
|-------------------------|----------------|------------|-------------------|------------------------------------|
| children               | 4              | 0.003%     | -                 | Few missing → imputed with mode    |
| country                | 488            | 0.41%      | -                 | High cardinality → frequency enc.  |
| agent                  | 16,340         | 13.69%     | -                 | Missing → replaced with 0          |
| company                | 112,593        | 94.31%     | -                 | Missing → replaced with 0          |
| adr                    | 0              | 0%         | 3.18%             | Extreme outliers, capped at 500    |
| lead_time              | 0              | 0%         | 2.52%             | Extreme outliers, capped at 365    |
| reservation_status_date| 0              | 0%         | -                 | Dropped (data leakage)             |
| reservation_status     | 0              | 0%         | -                 | Dropped (data leakage)             |

---

## 📈 Key Insights
- **ADR (Average Daily Rate)** contained extreme outliers (maximum value reached 5400).  
  These were capped at **500** to reduce skewness.  

- **Lead Time** values exceeded 500 days, which is unrealistic in most cases.  
  These were capped at **365 days**.  

- The majority of booking cancellations occur when **no deposit** is paid.  

- **Families** (bookings including children or babies) demonstrate **different booking behaviors** compared to solo travelers.  

- Guests with **special requests** are less likely to cancel, indicating a correlation between engagement and booking reliability.

