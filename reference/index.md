# Package index

- [`dfms-package`](https://docs.ropensci.org/dfms/reference/dfms-package.md)
  [`dfms`](https://docs.ropensci.org/dfms/reference/dfms-package.md) :
  Dynamic Factor Models

## Information Criteria

Choose the number of factors and the lag-order of the factor VAR.

- [`ICr()`](https://docs.ropensci.org/dfms/reference/ICr.md)
  [`print(`*`<ICr>`*`)`](https://docs.ropensci.org/dfms/reference/ICr.md)
  [`plot(`*`<ICr>`*`)`](https://docs.ropensci.org/dfms/reference/ICr.md)
  [`screeplot(`*`<ICr>`*`)`](https://docs.ropensci.org/dfms/reference/ICr.md)
  : Information Criteria to Determine the Number of Factors (r)

## Fit a Dynamic Factor Model

DFM estimation via the EM algorithm and PCA, and various methods inspect
the model and extract results.

- [`DFM()`](https://docs.ropensci.org/dfms/reference/DFM.md) : Estimate
  a Dynamic Factor Model
- [`print(`*`<dfm>`*`)`](https://docs.ropensci.org/dfms/reference/summary.dfm.md)
  [`coef(`*`<dfm>`*`)`](https://docs.ropensci.org/dfms/reference/summary.dfm.md)
  [`logLik(`*`<dfm>`*`)`](https://docs.ropensci.org/dfms/reference/summary.dfm.md)
  [`summary(`*`<dfm>`*`)`](https://docs.ropensci.org/dfms/reference/summary.dfm.md)
  [`print(`*`<dfm_summary>`*`)`](https://docs.ropensci.org/dfms/reference/summary.dfm.md)
  : DFM Summary Methods
- [`plot(`*`<dfm>`*`)`](https://docs.ropensci.org/dfms/reference/plot.dfm.md)
  [`screeplot(`*`<dfm>`*`)`](https://docs.ropensci.org/dfms/reference/plot.dfm.md)
  : Plot DFM
- [`as.data.frame(`*`<dfm>`*`)`](https://docs.ropensci.org/dfms/reference/as.data.frame.dfm.md)
  : Extract Factor Estimates in a Data Frame
- [`residuals(`*`<dfm>`*`)`](https://docs.ropensci.org/dfms/reference/residuals.dfm.md)
  [`fitted(`*`<dfm>`*`)`](https://docs.ropensci.org/dfms/reference/residuals.dfm.md)
  : DFM Residuals and Fitted Values

## Forecasting

Forecast both the factors and the data, and methods to visualize
forecasts and extract results.

- [`predict(`*`<dfm>`*`)`](https://docs.ropensci.org/dfms/reference/predict.dfm.md)
  [`print(`*`<dfm_forecast>`*`)`](https://docs.ropensci.org/dfms/reference/predict.dfm.md)
  [`plot(`*`<dfm_forecast>`*`)`](https://docs.ropensci.org/dfms/reference/predict.dfm.md)
  [`as.data.frame(`*`<dfm_forecast>`*`)`](https://docs.ropensci.org/dfms/reference/predict.dfm.md)
  : DFM Forecasts

## News Decomposition

Decompose forecast revisions into news contributions follwing Banbura
and Modugno (2014).

- [`news()`](https://docs.ropensci.org/dfms/reference/news.md)
  [`print(`*`<dfm_news>`*`)`](https://docs.ropensci.org/dfms/reference/news.md)
  [`print(`*`<dfm_news_list>`*`)`](https://docs.ropensci.org/dfms/reference/news.md)
  [`` `$`( ``*`<dfm_news_list>`*`)`](https://docs.ropensci.org/dfms/reference/news.md)
  [`` `[[`( ``*`<dfm_news_list>`*`)`](https://docs.ropensci.org/dfms/reference/news.md)
  [`` `[`( ``*`<dfm_news_list>`*`)`](https://docs.ropensci.org/dfms/reference/news.md)
  [`as.data.frame(`*`<dfm_news_list>`*`)`](https://docs.ropensci.org/dfms/reference/news.md)
  : News Decomposition

## Fast Stationary Kalman Filtering and Smoothing

Optimized Armadillo C++ implementations of the stationary Kalman Filter
and Smoother.

- [`SKF()`](https://docs.ropensci.org/dfms/reference/SKF.md) : (Fast)
  Stationary Kalman Filter
- [`FIS()`](https://docs.ropensci.org/dfms/reference/FIS.md) : (Fast)
  Fixed-Interval Smoother (Kalman Smoother)
- [`SKFS()`](https://docs.ropensci.org/dfms/reference/SKFS.md) : (Fast)
  Stationary Kalman Filter and Smoother

## Helper Functions

Convert ‘dfm’ object to other popular state space representations. Fast
VAR, matrix inverses, imputation/removal of missing values in
multivariate time series, and convergence check for EM algorithm.

- [`convert()`](https://docs.ropensci.org/dfms/reference/convert.md) :
  Convert DFM to Other State Space Model Formats
- [`.VAR()`](https://docs.ropensci.org/dfms/reference/dot-VAR.md) :
  (Fast) Barebones Vector-Autoregression
- [`tsnarmimp()`](https://docs.ropensci.org/dfms/reference/tsnarmimp.md)
  : Remove and Impute Missing Values in a Multivariate Time Series
- [`ainv()`](https://docs.ropensci.org/dfms/reference/ainv.md)
  [`apinv()`](https://docs.ropensci.org/dfms/reference/ainv.md) :
  Armadillo's Inverse Functions
- [`em_converged()`](https://docs.ropensci.org/dfms/reference/em_converged.md)
  : Convergence Test for EM-Algorithm

## Data

Euro area macroeconomic data from Banbura and Modugno (2014), and 3 DFM
specifications considered in their paper.

- [`BM14_Models`](https://docs.ropensci.org/dfms/reference/BM14_Models.md)
  [`BM14_M`](https://docs.ropensci.org/dfms/reference/BM14_Models.md)
  [`BM14_Q`](https://docs.ropensci.org/dfms/reference/BM14_Models.md) :
  Euro Area Macroeconomic Data from Banbura and Modugno 2014
