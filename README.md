# Disease Diagnosis Clustering Analysis

![Python](https://img.shields.io/badge/Python-3.9-blue)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-Latest-orange)
![Status](https://img.shields.io/badge/Status-Completed-success)
![Competition](https://img.shields.io/badge/Kaggle-IDM%20Challenge%203-20BEFF)

## 📋 Project Overview

This project implements **unsupervised machine learning clustering algorithms** to diagnose diseases based on patient symptoms. Developed as part of the **IDM Challenge 3 (Fall 2022)** Kaggle competition, the analysis partitions patient data into meaningful disease clusters using advanced clustering techniques.

### 🎯 Objective
Partition patient symptom data into appropriate clusters where each cluster represents a single disease/diagnosis class, maximizing the **Adjusted Rand Index (ARI)** score.

### 🏆 Key Achievement
- **Best ARI Score**: 0.84145
- **Methodology**: Agglomerative Clustering with correlation-based feature selection
- **Competition Performance**: Successfully identified disease patterns from symptom data

---

## 📊 Dataset Information

### Dataset Characteristics
- **Total Patients**: 2,784 records
- **Features**: 133 symptom attributes (132 after preprocessing)
- **Data Type**: Binary (0 = symptom absent, 1 = symptom present)
- **Source**: IDM Challenge 3 - Kaggle Competition
- **Files Included**: `data/Data.csv` and `data/sample_submission.csv`

### Sample Symptoms Analyzed
- Itching, skin rash, nodal skin eruptions
- Continuous sneezing, shivering, chills
- Joint pain, stomach pain, vomiting
- Fatigue, weight loss, restlessness
- High fever, sweating, dehydration
- And 120+ additional symptom indicators

---

## 🔬 Methodology

### 1. **Data Preparation**
- **Feature Engineering**: Removed constant-value features
- **Correlation Analysis**: Applied correlation matrix to identify and handle multicollinearity
- **Variance Threshold**: Filtered low-variance features
- **Data Quality**: No missing values or categorical encoding required

### 2. **Clustering Techniques Implemented**

#### K-Means Clustering
- Iterative testing with 8-19 cluster configurations
- Multiple random state initializations
- Elbow method for optimal cluster identification
- WSS (Within-Cluster Sum of Squares) optimization

#### Agglomerative (Hierarchical) Clustering
- **Linkage Methods**: Single, Average, Complete
- **Distance Metrics**: Euclidean, Manhattan
- **Cluster Range**: 8-19 clusters tested
- Dendrogram visualization for hierarchy analysis

### 3. **Model Selection Strategy**
- Systematic experimentation with 50+ model configurations
- Cross-validation using different linkage and distance combinations
- Feature selection impact analysis
- Iterative refinement based on ARI scores

---

## 📈 Results & Performance

### Best Performing Model
```
Algorithm: Agglomerative Clustering
Clusters: 11
Linkage: Average
Distance Metric: Manhattan
Feature Selection: Correlation Matrix
ARI Score: 0.84145
```

### Model Comparison Summary

| Model Type | Best Score | Configuration |
|------------|-----------|---------------|
| Agglomerative | **0.84145** | 11 clusters, avg linkage, Manhattan, corr matrix |
| K-Means | 0.78356 | 18 clusters, multiple iterations |
| Agglomerative | 0.74522 | 11 clusters, avg linkage, Manhattan |
| K-Means | 0.71249 | 16 clusters, looped iterations |

### Key Insights
1. **Agglomerative Clustering outperformed K-Means** consistently when properly configured
2. **Correlation-based feature selection** significantly improved model performance
3. **Manhattan distance with average linkage** provided optimal results for this medical dataset
4. **Optimal cluster count** ranged between 11-18 clusters across best models
5. **K-Means showed high variance** in results due to random initialization

---

## 🛠️ Technical Implementation

### Technologies Used
- **Python 3.9**
- **pandas** - Data manipulation and analysis
- **NumPy** - Numerical computing
- **scikit-learn** - Machine learning algorithms
  - KMeans
  - AgglomerativeClustering
  - VarianceThreshold
  - silhouette_score
- **scipy** - Hierarchical clustering and dendrogram
- **matplotlib** - Data visualization

### Key Features
- Automated clustering pipeline with iterative testing
- Feature selection using variance threshold and correlation analysis
- Visualization tools (elbow curve, silhouette analysis, dendrogram)
- Comprehensive model tracking across 50+ experiments

---

## 📁 Repository Structure

```
disease-diagnosis-clustering/
│
├── data/
│   ├── Data.csv                     # Training dataset (2,784 patients)
│   ├── sample_submission.csv        # Submission format template
│   └── README.md                    # Data source and description
│
├── notebooks/
│   └── clustering_analysis.ipynb    # Main analysis notebook
│
├── docs/
│   ├── PROJECT_REPORT.md           # Detailed project documentation
│   └── METHODOLOGY.md              # In-depth methodology explanation
│
├── images/
│   └── kaggle_competition.png      # Competition screenshot
│
├── results/
│   └── model_performance.md        # Detailed results analysis
│
├── requirements.txt                 # Python dependencies
└── README.md                        # This file
```

---

## 🔍 Explore the Analysis

This repository contains the complete analysis code and comprehensive documentation:

- **Jupyter Notebook**: `notebooks/clustering_analysis.ipynb` - Complete implementation
- **Detailed Report**: `docs/PROJECT_REPORT.md` - Full methodology and results
- **Technical Deep-Dive**: `docs/METHODOLOGY.md` - Algorithm explanations
- **All Experiments**: `results/model_performance.md` - 50 configurations analyzed

### Technologies Used
```
Python 3.9 | pandas | NumPy | scikit-learn | scipy | matplotlib
```

---

## 💡 Key Learnings

1. **Feature Selection Impact**: Proper feature engineering through correlation analysis improved ARI score by ~12%
2. **Algorithm Selection**: Agglomerative clustering proved more stable and effective than K-Means for medical symptom data
3. **Hyperparameter Tuning**: Distance metrics and linkage methods significantly impact clustering quality
4. **Cluster Validation**: Using multiple techniques (elbow, silhouette, dendrogram) provides robust cluster identification
5. **Iterative Experimentation**: Systematic testing across configurations is crucial for optimal performance

---

## 📊 Visualizations

The project includes:
- **Elbow Curve**: Identifying optimal cluster count using WSS
- **Silhouette Analysis**: Evaluating cluster quality and separation
- **Dendrogram**: Hierarchical relationship visualization between clusters
- **Correlation Heatmap**: Feature relationship analysis

---

## 🎓 Academic Context

**Course**: Introduction to Data Mining (IDM)  
**Institution**: IBA Karachi  
**Semester**: Fall 2022  
**Competition**: Kaggle - IDM Challenge 3  
**Evaluation Metric**: Adjusted Rand Index (ARI)

---

## 📞 Contact

**Emaad Ur Rehman**  
Data Analyst | Publicis Groupe  
[LinkedIn](https://www.linkedin.com/in/emaad-ur-rehman) | [GitHub](https://github.com/emaadurrehman)

---

## 📄 License

This project is part of an academic competition and is shared for educational and portfolio purposes.

---

## 🙏 Acknowledgments

- IBA Karachi for the course structure and competition organization
- Kaggle for hosting the competition platform
- scikit-learn community for comprehensive documentation
- Course instructors and peers for guidance and insights

---

## 📚 References

- [Adjusted Rand Index Documentation](https://en.wikipedia.org/wiki/Rand_index)
- [scikit-learn Clustering Guide](https://scikit-learn.org/stable/modules/clustering.html)
- [Hierarchical Clustering Explained](https://scikit-learn.org/stable/modules/clustering.html#hierarchical-clustering)
- Kaggle Competition: IDM Challenge 3 (Fall 2022)

---

⭐ **If you found this project helpful, please consider giving it a star!**
