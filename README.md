# pcaTools

This package augments Gretl's built-in `pca` command.

The package is a collection of functions for conducting Principal Component Analysis. It ships two plotting functions for creating a so called 'scree plot' (https://en.wikipedia.org/wiki/Scree_plot) and a bi-plot (https://en.wikipedia.org/wiki/Biplot).

Furthermore, it supports the computation of sparse PCs meaning that some loading coefficients may be zero. The estimation of the loadings is done by the forward-stagewise boosting algorithm (Tibshirani, for details see the `fsboost` Gretl package) which is similar to Lasso. Currently, however, only the loadings and scores are based on the sparse PC estimates but not the estimated variances.

Please report bugs or comments on the gretl mailing list, report an issue on github (https://github.com/atecon/pcaTools/issues) or write to atecon@posteo.de.


# Install from local file

Download the gfn-file which you find here https://github.com/atecon/pcaTools/blob/main/src/pcaTools.gfn

To install the package, run the following Gretl command:

```
pkg install /path/to/pcaTools.gfn --local
```


# Public functions

```
pcaEst(const list X, bundle opts[null])
```

This function performs Principal Component Analysis (PCA) on the input data.

## Parameters

- `X`: list, Variables on which to conduct PCA.
- `opts`: bundle, Optional bundle passing parameters

`opts` can include the following parameter for setting options:

- `do_stdize`: bool, Centre variables and divide by their respective standard deviattion (default: `TRUE`)
- `use_vcv`: bool, Compute principal components based on variance-covariance matrix if `TRUE`, otherwise if `FALSE` use the correlation matrix (default: `TRUE`)
- `verbose`: bool, Make output more verbose if `TRUE` (default: `FALSE`)


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

One can tweak the plot by passing specific parameters to the bundle `self` before calling `pcaScreeplot()`. The following parameters are supported:

- `fontsize`: Size of font (default: 10)
- `linedwidth`: Width of the line (default: 1.5)

## Returns

No return value. This function creates a scree plot.


```
pcaBiplot(const bundle self, const string filename[null])
```

This function generates a bi-plot from the results of a PCA analysis for each combination of computed principal components as a matrix of plots. A biplot is a plot of two principal components. It shows the combination of scores and the loading factors for each principal component.

## Parameters

- `self`: A bundle containing the results of a PCA, typically returned by `pcaEst`.
- `filename`: A string referring to the PATH+FILENAME for storing the plot (optional). If no string is passed, the plot appears on the screen immediately.


## Returns

No return value. This function generates a bi-plot.


## Options passed to the PairPlot() function by means of the 'opts' bundle

One can tweak the plot by passing specific parameters to the bundle `self` before calling `pcaBiplot`. The following parameters are supported:

- `centre_biplot`: bool, Centre the axes if `TRUE`, otherwise not (default: `TRUE`).
- `cols_biplot`: int, Number of columns of gridplot (default: `NA` -> automatically set)
- `color_arrow`: string, Color of the arrows depicting the eigenvector (default: "web-blue")
- `color_pattern`: string, Color pattern for (factorized) data points of biplot. Either "dark2" or "default" (default: `dark2`).
- `factor`: series, Distinct values for factorized bi-plot (default: none)
- `fontsize`: int, Size of font (default: 12)
- `fontsize_arrow`: int, Size of font of the arrow labels (default: 12)
- `height_biplot`: int, Height of biplot (default: 600)
- `linedwidth`: scalar, Width of the line (default: 1.5)
- `linedwidth_arrow`: scalar, Width of the lines for the bi-plot arrows (default: 1.0)
- `n_pcs_to_plot`: int, Number of first principal components to plot (default: all)
- `offset_label_x`: scalar, Offset of labels for arrows along x-axis (default: 0)
- `offset_label_y`: scalar, Offset of labels for arrows along y-axis (default: 0)
- `pointtype`: int, Point type (default: 4)
- `pointsize`: scalar, Size of point (default: 1.0)
- `rows_biplot`: int, Number of rows of gridplot (default: `NA` -> automatically set)
- `sparse_pca`: bool, If true, compute sparse PCA, otherwise non-sparse version (default: `FALSE`)
- `transparency`: int, The rgbalpha plotting style assumes that each pixel of input data contains an alpha value in the range [0:255] (no transparency:full transparency). Currently, only applied to the 1st factor.
- `width_biplot`: int, Width of biplot (default: 600)

# Changelog

* **v0.2 (February 2024)**
    * Introduce sparse regression-based PCA using the forward-stagewise boosting algorithm for feature selection
    * Improve plotting the loadings: put on the secondary axis
    * New package dependence: 'fsboost' package

* **v0.1 (January 2024)**
    * Initial version
