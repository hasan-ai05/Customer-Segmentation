# Customer Segmentation — Unsupervised Learning

A clustering project that discovers natural customer groups from purchasing behavior
without any predefined labels. Three algorithms are compared, and each resulting segment
is translated into a business persona with a specific marketing recommendation.

---

## The Problem

A mall has 200 customers and no labels. No one has decided in advance which customers
are valuable, which are at risk, or which need a different approach. The question this
project answers: **do natural groups exist in the data, and if so, what defines them?**

This is fundamentally different from the supervised projects in this portfolio.
There is no target column. The algorithm finds structure that was not put there.

---

## Dataset

**Source:** Mall Customer Segmentation Dataset — Kaggle  
**Records:** 200 customers, 5 features  
**No target variable** — pure unsupervised learning

| Feature | Description |
|---|---|
| Age | Customer age in years |
| Annual Income | Income in thousands of dollars (k$), range 15–137 |
| Spending Score | Mall-assigned score 1–100 based on purchase frequency |
| Gender | Male (44%) / Female (56%) |

**Key observation before modeling:** Income and Spending Score have a correlation of 0.010 — essentially zero. High earners do not necessarily spend more. This is what makes 5 distinct segments possible: the two axes are independent.

---

## Finding the Right K

Two methods were used in combination to select K:

**Elbow Method:** Inertia drops sharply from K=2 to K=5, then flattens.

**Silhouette Scores:**

| K | Silhouette |
|---|---|
| 2 | 0.3213 |
| 3 | 0.4666 |
| 4 | 0.4939 |
| **5** | **0.5547** |
| 6 | 0.5399 |
| 7 | 0.5281 |

K=5 maximizes the Silhouette Score — clusters are well-separated and internally compact.

![Elbow and Silhouette](images/elbow_silhouette.png)

---

## Model Comparison

| Model | Clusters | Silhouette | DB Score |
|---|---|---|---|
| KMeans | 5 | **0.5547** | **0.5722** |
| DBSCAN | 2 | 0.3876 | N/A |
| Hierarchical | 5 | 0.5538 | 0.5779 |

KMeans wins by a small margin over Hierarchical. DBSCAN found only 2 clusters and
labeled 8 customers (4%) as noise — it is designed for arbitrary shapes, not the
clean spherical clusters that income/spending data produces.

**Stability check:** KMeans run 10 times with different seeds.
Silhouette = 0.5547 ± 0.0000 — identical result every run. The 5 clusters are stable.

---

## The 5 Customer Personas

| Cluster | Size | Avg Age | Avg Income | Avg Spending | Persona |
|---|---|---|---|---|---|
| 0 | 81 (40.5%) | 42.7 | 55.3k | 49.5 | Regular Customers |
| 1 | 39 (19.5%) | 32.7 | 86.5k | 82.1 | VIP Spenders |
| 2 | 22 (11.0%) | 25.3 | 25.7k | 79.4 | Impulsive Shoppers |
| 3 | 35 (17.5%) | 41.1 | 88.2k | 17.3 | Careful High-earners |
| 4 | 23 (11.5%) | 45.2 | 26.2k | 20.1 | Budget Conscious |

**The most strategically important finding:** Cluster 3 — high earners with low spending scores.
These customers have the purchasing power but are not using it. Re-engagement campaigns
directed at this segment have the highest potential return.

**Cluster 2 is the risk segment:** young, low income, high spending. Loyalty programs
and subscription models capture this group before they reduce spend.

![2D Cluster Plot](images/cluster_2d.png)
![3D Cluster Plot](images/cluster_3d.png)

---

## Cluster Profiles

![Persona Cards](images/persona_cards.png)

---

## Executive Dashboard

![Dashboard](images/executive_dashboard.png)

---

## How to Run

```bash
pip install kagglehub pandas numpy scikit-learn plotly matplotlib seaborn scipy
jupyter notebook Project3_Customer_Segmentation.ipynb
```

Dataset downloads automatically via `kagglehub`.

---

## Where to Place Screenshots

```
customer-segmentation/
    images/
        eda_dashboard.png         Section 5 — EDA subplots
        elbow_silhouette.png      Section 7 — finding K
        cluster_2d.png            Section 12 — 2D scatter
        cluster_3d.png            Section 12 — 3D scatter
        dendrogram.png            Section 10 — hierarchical tree
        executive_dashboard.png   Section 15 — full dashboard
    README.md
    Project3_Customer_Segmentation.ipynb
```

---

## Project Structure

```
Project3_Customer_Segmentation.ipynb    main notebook (15 sections)
README.md                               this file
images/                                 screenshots from notebook output
```

---

*Part of an 8-project AI Engineering portfolio — Hasan Akhras*
