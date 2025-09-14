# 📊 Marketing Mix Model with Causal Mediation

This project analyzes **two years of weekly sales data** to understand the drivers of revenue for a business.  
The primary goal is to build a machine learning model that quantifies the impact of various marketing channels  
(paid media, email, SMS), pricing, and brand presence on revenue.

A key feature of this analysis is the explicit modeling of a **causal mediation assumption**:

> **Social Media Spend (Facebook, TikTok, etc.) → Google Searches (Google Spend) → Revenue**

This relationship is modeled using a **two-stage regression approach** to separate the direct and mediated effects of social media.

---

## 📂 Project Structure
.
├── data/
│ └── Assessment 2 - MMM Weekly.csv
├── MMM_Causal_Analysis.ipynb
└── README.md

## ⚙️ Setup and Installation

This project uses **Python 3.10**.  
It is recommended to use a virtual environment to manage dependencies.

### 1️. Create a Virtual Environment

```bash
# Create the environment
python -m venv .venv

# Activate the environment
# On Windows:
.\.venv\Scripts\activate
# On MacOS/Linux:
source .venv/bin/activate
```
### 2. Install Required Libraries

```bash
pip install -r requirements.txt
```

## Methodology & Findings – Marketing Mix Model with Causal Mediation

All analysis is implemented in **MMM_Causal_Analysis.ipynb** following these steps:

---

### 1️. Data Preparation & EDA

- Load weekly data and index by date.
- Perform exploratory data analysis (EDA) to identify trends, seasonality, and correlations.

---

### 2️. Feature Engineering

- **Adstock:** Apply geometric decay to model carryover effects of ad spend.
- **Saturation:** Model diminishing returns with a power function.
- **Time Features:** Add trend index and month-based dummy variables.

---

### 3️. Two-Stage Causal Modeling

To address the **Social → Google → Revenue** mediation hypothesis:

- **Stage 1:** Predict **Google Spend** using Social Media Spend and control variables (**Ridge Regression**).
- **Stage 2:** Predict **Revenue** using:
  - Direct Social Spend effects
  - Predicted + residual components of Google Spend  
  *(This avoids double-counting the marketing effects).*

---

### 4️. Model Refinement

- Combine highly correlated social channels into a single **`total_social_spend`** feature.
- Standardize features using **StandardScaler** for numerical stability.
- Regularize with **Ridge regression** to reduce multicollinearity.

---

###  Key Findings & Recommendations

- **Social Media is the Primary Driver:** A holistic social strategy is the largest revenue driver.
- **SMS Outperforms Email:** SMS is a highly effective direct-response lever.
- **High Price Sensitivity:** Revenue drops significantly with price increases.
- **Brand Building Pays Off:** Growth in `social_followers` strongly correlates with revenue uplift.
- **Promotions Are Reactive:** Promotions seem defensive (used to recover slow periods) rather than proactive growth drivers.

---

##  How to Run

1. Ensure your virtual environment is active and dependencies are installed.
2. Launch **Jupyter Notebook** or **VS Code**.
3. Open `MMM_Causal_Analysis.ipynb`.
4. Run the cells sequentially from top to bottom to reproduce the analysis.

---

##  Notes

- The **two-stage modeling approach** helps prevent **double-counting effects** of marketing channels.
- You can experiment with:
  - Different **adstock rates**
  - Alternative **saturation parameters**
  - Varying **regularization strengths**

to further optimize performance.