## Why Dimensionality Reduction

Dimensionality reduction (reducing the number of features) can result in:

- Visualizations (2-3 dimensional plots)
- Lower computational complexity (time and space)
- Improve model performance (e.g. accuracy)
- Avoid over-fitting

## How can we reduce the number of features?

1. Dimensionality reduction (transform features into a lower dimension using linear algebra)
    - PCA: Principal Component Analysis
    - LDA

2. Variable selection (simply selecting or excluding certain variables)

    - Filter methods
    - Wrapper methods
-----------

## What is PCA?
PCA represents many variables with fewer variables while minimizing loss of information!

For number of dimensions (variablse/features) in our data, we also have the same number of principal components.

> :bulb: **Tip:** Remember that PC1 was a “best-fit” line in the direction of MOST variation.

PC2 will be in the direction of the **next most variation**, following a few rules:
- Must pass through the mean of each variable
- Must be perpendicular/orthogonal to all other previous principal components.

We keep the principal components that have the most variation! 

PCA is done mathematically through matrix multiplication (python: sklearn)

> :memo: **Note:** it is important to scale data prior to PCA (since it’s based on variance). (StandardScaler)

## Coding
``` python
# Create cumulative explained variance graph
# Pretend we'd like to have about 90% explained variance
from sklearn.decomposition import PCA

pca = PCA()
pca.fit(df)

cum_explained_variance = np.cumsum(pca.explained_variance_ratio_)
plt.plot(cum_explained_variance)
plt.xlabel('PC number')
plt.ylabel('% Cumulative explained variance')
```
``` python
# Find the first 100 principle components of the dataset
pca = PCA(n_components=100)
pca.fit(df)

# Transform the data to its low-dimensional representation
reduced_df = pca.transform(df)

print(reduced_df.shape)
pd.DataFrame(reduced_df).head() #as a dataframe
```
## My Questions
- Why not using PCA for clustering before modeling?
- Do we use PCA for classification before or after modeling?
- Should we scale all the features? How can we do it? ( yes we should, trough StandardScaler)
- Should we deal with outliers prior to PCA? (Yes, I think so)
- Does the information loss in PCA, mean that we disregard some rows in the modeling?
- How to identify the extreme cases where PCA is not useful and cause loosing lots of information? (I think with the variance graph)
- It seams that PCA deals with outliers in some way. Am I right?