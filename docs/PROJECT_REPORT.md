# Disease Diagnosis Clustering - Project Report

## Executive Summary

This report documents the comprehensive analysis and implementation of clustering algorithms for disease diagnosis based on patient symptoms. The project achieved an **Adjusted Rand Index (ARI) score of 0.84145**, representing strong alignment between predicted clusters and actual disease classes.

---

## 1. Business Understanding

### 1.1 Problem Statement
In medical diagnostics, identifying diseases based on symptom patterns is crucial for:
- Early disease detection and intervention
- Resource allocation in healthcare facilities
- Pattern recognition for rare disease combinations
- Supporting clinical decision-making systems

### 1.2 Project Goals
- Develop an unsupervised learning model to cluster patients by disease based on symptoms
- Maximize clustering accuracy measured by Adjusted Rand Index
- Identify optimal clustering algorithm and configuration
- Create interpretable disease groupings for medical applications

### 1.3 Success Criteria
- **Primary**: Achieve high ARI score (>0.70)
- **Secondary**: Develop reproducible and explainable clustering methodology
- **Tertiary**: Compare multiple clustering approaches systematically

---

## 2. Data Understanding

### 2.1 Dataset Overview
- **Source**: IDM Challenge 3 Kaggle Competition
- **Domain**: Medical diagnostics and disease classification
- **Records**: 2,784 patient observations
- **Features**: 133 columns (132 symptoms + 1 ID column)

### 2.2 Data Characteristics

#### Feature Types
All features are **binary indicators**:
- `0` - Symptom is absent in the patient
- `1` - Symptom is present in the patient

#### Sample Features
```
- itching
- skin_rash
- nodal_skin_eruptions
- continuous_sneezing
- shivering
- chills
- joint_pain
- stomach_pain
- acidity
- vomiting
- fatigue
- weight_loss
- restlessness
- high_fever
- sweating
- dehydration
... (and 116 more symptom features)
```

### 2.3 Data Quality Assessment

| Aspect | Finding | Action Required |
|--------|---------|-----------------|
| Missing Values | None | No imputation needed |
| Data Types | All numeric (binary) | No encoding needed |
| Duplicates | Not assessed | Assumed handled by competition |
| Outliers | Not applicable (binary data) | N/A |
| Class Imbalance | Unknown (unsupervised) | Addressed through clustering |

### 2.4 Initial Observations
- Medical symptom data with sparse representation (many 0s expected)
- High dimensionality (132 features) suggests need for feature selection
- Binary nature makes correlation analysis effective
- Domain suggests natural clustering by disease types

---

## 3. Data Preparation

### 3.1 Preprocessing Steps

#### Step 1: Data Loading
```python
import pandas as pd
import numpy as np

train = pd.read_csv('Data.csv')
train = train.drop(columns='row ID')  # Remove identifier column
```

#### Step 2: Feature Selection - Correlation Matrix
```python
# Identify and remove highly correlated features
cor_matrix = train.corr().abs()
upper_tri = cor_matrix.where(
    np.triu(np.ones(cor_matrix.shape), k=1).astype(np.bool)
)
to_drop = [column for column in upper_tri.columns 
           if any(upper_tri[column] > 0.95)]
```

**Rationale**: Highly correlated features (>0.95) provide redundant information and can skew clustering results.

#### Step 3: Remove Constant Features
```python
# Identify features with zero variance
constant_features = [col for col in train.columns 
                     if train[col].nunique() == 1]
train = train.drop(columns=constant_features)
```

**Rationale**: Features with constant values (all 0s or all 1s) provide no discriminatory power.

#### Step 4: Variance Threshold
```python
from sklearn.feature_selection import VarianceThreshold

selector = VarianceThreshold(threshold=0.01)
train_filtered = selector.fit_transform(train)
```

**Rationale**: Low-variance features contribute minimal information to clustering.

### 3.2 Data Preparation Summary

| Technique | Purpose | Impact |
|-----------|---------|--------|
| Correlation filtering | Remove multicollinearity | Improved model stability |
| Constant removal | Eliminate non-informative features | Reduced dimensionality |
| Variance threshold | Focus on discriminatory features | Enhanced clustering quality |

**Final Dataset**: Reduced feature set with higher information density

---

## 4. Modeling Approach

### 4.1 Clustering Algorithms Selected

#### 4.1.1 K-Means Clustering
**Characteristics**:
- Partitioning algorithm
- Minimizes within-cluster variance
- Requires pre-specified number of clusters
- Sensitive to initialization

**Configuration Tested**:
- Cluster range: 8-19 clusters
- Initialization: Random and k-means++
- Multiple iterations with different random states

**Advantages for this dataset**:
- Fast computation
- Scales well with 2,784 records
- Simple interpretability

**Challenges**:
- High variance in results due to random initialization
- Assumes spherical clusters (may not match medical symptom patterns)

#### 4.1.2 Agglomerative Clustering
**Characteristics**:
- Hierarchical bottom-up approach
- Deterministic results (no randomness)
- Flexible with linkage criteria and distance metrics

**Configuration Tested**:

| Parameter | Options Tested |
|-----------|---------------|
| Linkage | Single, Average, Complete |
| Distance Metric | Euclidean, Manhattan |
| Cluster Count | 8-19 clusters |

**Advantages for this dataset**:
- More stable results
- Better handles non-spherical clusters
- Dendrograms provide interpretability

### 4.2 Cluster Count Determination

Three techniques employed:

#### 4.2.1 Elbow Method
```python
from sklearn.cluster import KMeans

WSS = []
for k in range(2, 20):
    kmeans = KMeans(n_clusters=k, random_state=42)
    kmeans.fit(train)
    WSS.append(kmeans.inertia_)
```
**Purpose**: Identify point where adding clusters provides diminishing returns

#### 4.2.2 Silhouette Analysis
```python
from sklearn.metrics import silhouette_score

silhouette_scores = []
for k in range(2, 20):
    kmeans = KMeans(n_clusters=k)
    labels = kmeans.fit_predict(train)
    score = silhouette_score(train, labels)
    silhouette_scores.append(score)
```
**Purpose**: Measure cluster cohesion and separation

#### 4.2.3 Dendrogram Analysis
```python
from scipy.cluster.hierarchy import dendrogram, linkage

linked = linkage(train, 'ward')
plt.figure(figsize=(100, 5))
dendrogram(linked)
plt.axhline(y=19, color='b', linestyle='--')
```
**Purpose**: Visual hierarchy analysis for hierarchical clustering

### 4.3 Experimentation Strategy

**Systematic Approach**:
1. **Phase 1**: K-Means with varying clusters (Entries 1-17)
2. **Phase 2**: Agglomerative initial testing (Entries 18-19)
3. **Phase 3**: Feature-selected K-Means (Entries 20-30)
4. **Phase 4**: Optimized Agglomerative (Entries 31-50)

**Total Experiments**: 50 model configurations tested

---

## 5. Results & Analysis

### 5.1 Top Performing Models

| Rank | Entry | Algorithm | Config | ARI Score |
|------|-------|-----------|--------|-----------|
| 1 | 40, 41, 50 | Agglomerative | 11 clusters, avg, Manhattan, corr matrix | **0.84145** |
| 2 | 17 | K-Means | 18 clusters | 0.78356 |
| 3 | 35 | Agglomerative | 11 clusters, avg, Manhattan | 0.74522 |
| 4 | 38 | Agglomerative | 11 clusters, avg, Manhattan | 0.72321 |
| 5 | 43 | Agglomerative | 16 clusters, single linkage | 0.72239 |

### 5.2 Performance Analysis

#### Best Model Deep Dive
```
Configuration: Agglomerative Clustering
- Clusters: 11
- Linkage: Average
- Distance: Manhattan
- Feature Selection: Correlation matrix filtering
- ARI Score: 0.84145
```

**Why This Configuration Succeeded**:
1. **Average linkage** balances cluster compactness and separation better than single/complete
2. **Manhattan distance** works well with binary data (L1 norm suitable for sparse features)
3. **11 clusters** likely aligns with actual number of diseases in dataset
4. **Correlation filtering** removed redundant symptoms, improving cluster purity

#### Algorithm Comparison

**K-Means Performance**:
- Average score: ~0.50
- Best score: 0.78356
- High variance: Scores ranged from 0.33 to 0.78
- **Issue**: Random initialization caused instability

**Agglomerative Performance**:
- Average score: ~0.65
- Best score: 0.84145
- More consistent: Lower variance across experiments
- **Advantage**: Deterministic results, better stability

### 5.3 Feature Selection Impact

| Approach | Best Score | Improvement |
|----------|-----------|-------------|
| No feature selection | 0.72321 | Baseline |
| With correlation matrix | 0.84145 | +16.4% |

**Key Finding**: Correlation-based feature selection was critical for achieving top performance.

### 5.4 Cluster Count Analysis

Optimal range identified: **11-18 clusters**

| Clusters | Best ARI | Algorithm |
|----------|----------|-----------|
| 11 | 0.84145 | Agglomerative |
| 16 | 0.72239 | Agglomerative |
| 17 | 0.60619 | Agglomerative |
| 18 | 0.78356 | K-Means |
| 19 | 0.53057 | Agglomerative |

**Insight**: Performance peaked at 11 clusters, suggesting dataset contains approximately 11 distinct disease patterns.

---

## 6. Model Evaluation

### 6.1 Adjusted Rand Index (ARI) Explained

**Formula**: ARI measures similarity between predicted and true clusters, adjusted for chance.

**Interpretation**:
- ARI = 1.0: Perfect clustering match
- ARI = 0.0: Random clustering
- ARI < 0: Worse than random

**Score of 0.84145**:
- Indicates **84% agreement** with true disease classes
- Significantly better than random assignment
- Shows strong pattern recognition capability

### 6.2 Model Strengths
1. ✅ High accuracy in disease grouping (84% ARI)
2. ✅ Reproducible results (deterministic algorithm)
3. ✅ Interpretable through dendrogram visualization
4. ✅ Robust to feature engineering choices
5. ✅ Computationally efficient for dataset size

### 6.3 Model Limitations
1. ⚠️ Requires domain knowledge for optimal cluster count selection
2. ⚠️ Performance sensitive to distance metric choice
3. ⚠️ No direct probability estimates for cluster assignment
4. ⚠️ Assumes diseases have distinct symptom patterns

---

## 7. Conclusions

### 7.1 Key Findings

1. **Agglomerative clustering significantly outperformed K-Means** for medical symptom data
2. **Feature selection through correlation analysis** was crucial for optimal performance
3. **Manhattan distance with average linkage** proved most effective for binary symptom data
4. **11 clusters** optimally represented the disease structure in the dataset
5. **Systematic experimentation** across 50 configurations identified best approach

### 7.2 Business Value

For healthcare applications:
- **Automated disease grouping** can support clinical decision systems
- **Pattern identification** helps recognize rare symptom combinations
- **Resource planning** based on disease cluster prevalence
- **Quality assurance** for diagnostic consistency

### 7.3 Technical Learnings

1. **Algorithm Selection**: Hierarchical methods excel with structured medical data
2. **Distance Metrics**: Manhattan distance suits binary/sparse features better than Euclidean
3. **Feature Engineering**: Removing correlated features improves cluster quality
4. **Validation**: Multiple cluster determination techniques provide robust selection
5. **Iteration**: Systematic experimentation reveals non-obvious optimal configurations

---

## 8. Future Enhancements

### 8.1 Potential Improvements
- **Ensemble clustering**: Combine multiple algorithms for robust results
- **Feature importance**: Identify which symptoms most define each cluster
- **Cluster profiling**: Detailed symptom analysis for each disease group
- **Validation**: Compare against known disease taxonomies
- **Dimensionality reduction**: Apply PCA/t-SNE for visualization

### 8.2 Production Considerations
- **Real-time scoring**: Deploy model for new patient classification
- **Model monitoring**: Track performance drift over time
- **Integration**: API for clinical systems integration
- **Explainability**: SHAP values for cluster assignment reasoning
- **Continuous learning**: Update clusters as new diseases emerge

---

## 9. References

### Academic Papers
- Rousseeuw, P. J. (1987). "Silhouettes: A graphical aid to the interpretation and validation of cluster analysis"
- Rand, W. M. (1971). "Objective Criteria for the Evaluation of Clustering Methods"
- Ward, J. H. (1963). "Hierarchical Grouping to Optimize an Objective Function"

### Technical Documentation
- scikit-learn Clustering Documentation
- scipy Hierarchical Clustering Guide
- pandas Data Manipulation Reference

### Competition
- Kaggle: IDM Challenge 3 (Fall 2022)
- IBA Karachi - Introduction to Data Mining Course

---

**Report Prepared By**: Emaad Ur Rehman  
**Date**: Fall 2022  
**Institution**: IBA Karachi  
**Competition**: Kaggle IDM Challenge 3
