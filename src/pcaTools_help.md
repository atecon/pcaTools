# pcaTools

This package augments Gretl's built-in `pca` command.

The package is a collection of functions for conducting Principal Component Analysis. It ships two plotting functions for creating a so called 'scree plot' and a bi-plot.


# Public functions

```
pcaEst(const list X, bundle opts[null])
```

This function performs Principal Component Analysis (PCA) on the input data.

## Parameters

- `X`: list, Variables on which to conduct PCA.
- `opts`: bundle, Optional bundle passing parameters

`opts` can include the following parameter for setting options:

- `do_stdize`:
- `n_pcs_to_plot`:
- `use_vcv`:


## Returns

A bundle `self` containing the results of the PCA.



```
pcaPrint(const bundle self)
```

This function prints the results of a PCA analysis.


## Parameters

- `self`: bundle, Returned information from the `pcaEst()` function.

## Returns

No return value. This function prints the PCA results to the console.



```
pcaScreeplot(const bundle self, const string filename[null])
```

This function generates a scree plot from the results of a PCA analysis. A scree plot is a line plot of the eigenvalues of factors or principal components in an analysis.

## Parameters

- `self`: A bundle containing the results of a PCA, typically returned by `pcaEst`.
- `filename`: A string referring to the PATH+FILENAME for storing the plot (optional). If no string is passed, the plot appears on the screen immediately.

## Returns

No return value. This function generates a scree plot.


```
pcaBiplot(const bundle self, const string filename[null])
```

This function generates a bi-plot from the results of a PCA analysis for each combination of computed principal components as a matrix of plots. A biplot is a plot of two principal components. It shows the combination of scores and the loading factors for each principal component.

## Parameters

- `self`: A bundle containing the results of a PCA, typically returned by `pcaEst`.
- `filename`: A string referring to the PATH+FILENAME for storing the plot (optional). If no string is passed, the plot appears on the screen immediately.

## Returns

No return value. This function generates a bi-plot.



# Changelog

* **v0.1 (December 2023)**
    * Initial version
