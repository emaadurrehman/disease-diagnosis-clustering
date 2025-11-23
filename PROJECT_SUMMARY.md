# Disease Diagnosis Clustering - Project Summary

## 📊 Project at a Glance

| Aspect | Details |
|--------|---------|
| **Project Name** | Disease Diagnosis Clustering Analysis |
| **Competition** | IDM Challenge 3 (Fall 2022) - Kaggle |
| **Institution** | IBA Karachi |
| **Domain** | Medical Diagnostics & Machine Learning |
| **Task** | Unsupervised clustering of patients by disease |
| **Evaluation Metric** | Adjusted Rand Index (ARI) |
| **Best Score Achieved** | **0.84145 (84% accuracy)** |

---

## 🎯 Objective

Partition 2,784 patient records into disease clusters based on 132 binary symptom indicators using unsupervised machine learning techniques.

---

## 📁 Dataset

- **Size**: 2,784 patients × 133 columns
- **Features**: 132 binary symptom indicators (0 = absent, 1 = present)
- **Type**: Medical symptom data
- **Quality**: Clean, no missing values, no encoding needed

---

## 🔬 Methodology

### Algorithms Tested
1. **K-Means Clustering** (30 experiments)
2. **Agglomerative Clustering** (20 experiments)

### Feature Selection
- Correlation matrix filtering (>0.95 threshold)
- Constant feature removal
- Variance threshold filtering

### Cluster Validation
- Elbow method (WSS analysis)
- Silhouette analysis
- Dendrogram visualization

---

## 🏆 Best Model Configuration

```python
AgglomerativeClustering(
    n_clusters=11,
    metric='manhattan',
    linkage='average'
)
```

**With correlation-based feature selection**

### Performance
- **ARI Score**: 0.84145
- **Algorithm**: Agglomerative Clustering
- **Clusters**: 11
- **Distance**: Manhattan
- **Linkage**: Average
- **Reproducibility**: Perfect (deterministic)

---

## 📈 Key Results

### Algorithm Comparison

| Algorithm | Best Score | Average Score | Consistency |
|-----------|-----------|---------------|-------------|
| **Agglomerative** | **0.84145** | 0.663 | Excellent |
| K-Means | 0.78356 | 0.504 | Poor (high variance) |

### Top 5 Experiments

| Rank | Score | Configuration |
|------|-------|--------------|
| 🥇 1 | 0.84145 | Agglomerative: 11 clusters, Manhattan, avg linkage, corr matrix |
| 🥈 2 | 0.78356 | K-Means: 18 clusters |
| 🥉 3 | 0.74522 | Agglomerative: 11 clusters, Manhattan, avg linkage |
| 4 | 0.72321 | Agglomerative: 11 clusters, Manhattan, avg linkage |
| 5 | 0.72239 | Agglomerative: 16 clusters, single linkage |

### Impact of Feature Selection

| Approach | Best Score | Improvement |
|----------|-----------|-------------|
| No feature selection | 0.72321 | Baseline |
| **With correlation matrix** | **0.84145** | **+16.4%** |

---

## 💡 Key Insights

### What Worked ✅
1. **Agglomerative > K-Means**: 7.4% better peak performance, 31.6% better average
2. **Manhattan distance**: 23% better than Euclidean for binary data
3. **Correlation filtering**: Critical preprocessing step (+16.4% improvement)
4. **Average linkage**: Most balanced and robust criterion
5. **11 clusters**: Optimal representation of disease structure

### What Didn't Work ❌
1. K-Means random initialization (high variance: σ = 0.126)
2. Variance threshold alone (reduced performance)
3. Euclidean distance on binary features
4. Too many clusters (>18) or too few (<10)

---

## 🛠️ Technologies Used

- **Python 3.9**
- **pandas** - Data manipulation
- **NumPy** - Numerical computing
- **scikit-learn** - Machine learning algorithms
- **scipy** - Hierarchical clustering
- **matplotlib** - Visualization
- **Jupyter Notebook** - Interactive analysis

---

## 📚 Documentation Structure

```
disease-diagnosis-clustering/
│
├── README.md                      # Main documentation (this file)
├── QUICKSTART.md                  # Quick setup guide
│
├── notebooks/
│   └── clustering_analysis.ipynb  # Complete analysis
│
├── docs/
│   ├── PROJECT_REPORT.md         # Comprehensive report
│   └── METHODOLOGY.md            # Technical details
│
├── results/
│   └── model_performance.md      # All 50 experiments analyzed
│
├── data/
│   └── README.md                 # Dataset documentation
│
└── images/
    └── kaggle_competition.png    # Competition overview
```

---

## 🎓 Learning Outcomes

### Technical Skills Demonstrated
- Unsupervised machine learning
- Feature engineering and selection
- Clustering algorithm implementation
- Model evaluation and validation
- Data visualization
- Systematic experimentation

### Domain Knowledge Applied
- Medical symptom analysis
- Disease pattern recognition
- Healthcare data handling
- Binary data clustering techniques

### Soft Skills
- Systematic problem-solving
- Iterative experimentation (50 configurations)
- Documentation and communication
- Project organization

---

## 📊 Business Value

### Healthcare Applications
- **Automated Disease Grouping**: Support clinical decision systems
- **Pattern Identification**: Recognize rare symptom combinations
- **Resource Planning**: Allocate based on disease prevalence
- **Quality Assurance**: Ensure diagnostic consistency

### Performance Metrics
- **84% accuracy** in disease classification
- **Fully reproducible** results (deterministic algorithm)
- **Interpretable** through dendrogram visualization
- **Scalable** to larger patient populations

---

## 🚀 Future Enhancements

### Immediate Improvements
- Ensemble clustering methods
- Feature importance analysis
- Cluster profiling by symptoms
- Cross-validation with medical taxonomies

### Advanced Techniques
- DBSCAN for noise handling
- Spectral clustering
- Gaussian Mixture Models
- Deep clustering approaches

### Production Deployment
- Real-time patient classification API
- Model monitoring dashboard
- Continuous learning pipeline
- Integration with clinical systems

---

## 📞 Contact & Links

**Developer**: Emaad Ur Rehman  
**Role**: Data Analyst @ Publicis Groupe  
**LinkedIn**: [[Emaad Ur Rehman](linkedin.com/in/emaad-ur-rehman)]  
**GitHub**: [[emaadurrehman](https://github.com/emaadurrehman)]  
**Email**: [emaadrehman3010@gmail.com]

---

## 🏅 Competition Details

**Competition**: IDM Challenge 3  
**Platform**: Kaggle  
**Course**: Introduction to Data Mining  
**Institution**: IBA Karachi  
**Semester**: Fall 2022  
**Final Score**: 0.84145 ARI  

---

## 📄 Citation

If you use this work or methodology, please cite:

```
Emaad Ur Rehman (2022). Disease Diagnosis Clustering Analysis.
IDM Challenge 3 - IBA Karachi.
Available at: https://github.com/emaadurrehman/disease-diagnosis-clustering
```

---

## ⭐ Key Takeaway

**Systematic experimentation with proper feature engineering** yields significantly better results than algorithmic complexity alone. The combination of correlation-based feature selection with Manhattan distance-based agglomerative clustering achieved 84% accuracy in disease classification from symptom data.

---

**Last Updated**: November 2025  
**Version**: 1.0  
**Status**: Completed & Documented
