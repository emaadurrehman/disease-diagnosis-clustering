# Data Directory

## Dataset Information

This folder contains the dataset used for the disease diagnosis clustering analysis.

### Source
- **Competition**: IDM Challenge 3 (Fall 2022)
- **Platform**: Kaggle
- **Domain**: Medical Diagnostics

### Files Included

#### 1. Data.csv (Training Dataset)
- **Size**: 743 KB
- **Records**: 2,784 patient observations
- **Columns**: 133 features
  - 1 identifier column (`row ID`)
  - 132 symptom features (binary: 0 or 1)

#### 2. sample_submission.csv
- **Purpose**: Template for competition submission format
- **Structure**: Shows the expected format for cluster assignments
- **Size**: 29 KB

### Dataset Characteristics

#### Structure
- **Rows**: 2,784 patient records
- **Columns**: 133 features
  - 1 identifier column (`row ID`)
  - 132 symptom features (binary: 0 or 1)

#### Sample Feature Names
```
itching
skin_rash
nodal_skin_eruptions
continuous_sneezing
shivering
chills
joint_pain
stomach_pain
acidity
vomiting
fatigue
weight_loss
restlessness
high_fever
sweating
dehydration
... (and 116 more symptom columns)
```

#### Data Types
- All features are **binary indicators**:
  - `0` = Symptom absent
  - `1` = Symptom present

#### Data Quality
- ✅ No missing values
- ✅ No categorical encoding needed
- ✅ No outliers (binary data)
- ✅ Clean and preprocessed

### Data Privacy

This dataset contains medical symptom information. The data is anonymized:
- No personally identifiable information (PII) is included
- Data is used solely for academic and educational purposes
- Part of Kaggle IDM Challenge 3 (Fall 2022) competition

### Preprocessing Applied

The analysis notebook applies the following preprocessing:

1. **Remove identifier column**: Drop `row ID`
2. **Correlation filtering**: Remove highly correlated features (>0.95)
3. **Constant feature removal**: Drop features with zero variance
4. **Variance threshold**: Filter low-variance features (optional)

### Citation

If you use this dataset or analysis methodology, please acknowledge:
- IBA Karachi - Introduction to Data Mining (IDM) Course
- Kaggle - IDM Challenge 3 (Fall 2022)
- Original data source (if known)

---

**Need Help?**

If you have questions about the data or need access:
- Review the main README.md
- Check the PROJECT_REPORT.md in docs/
- Contact: Emaad Ur Rehman
