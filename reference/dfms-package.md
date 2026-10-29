# Dynamic Factor Models

*dfms* provides efficient estimation of Dynamic Factor Models via the EM
Algorithm — following Doz, Giannone & Reichlin (2011, 2012) and Banbura
& Modugno (2014). Contents:

**Information Criteria to Determine the Number of Factors**

[`ICr()`](https://docs.ropensci.org/dfms/reference/ICr.md)  

- [`plot(<ICr>)`](https://docs.ropensci.org/dfms/reference/ICr.md)  

- [`screeplot(<ICr>)`](https://docs.ropensci.org/dfms/reference/ICr.md)  

**Fit a Dynamic Factor Model**

[`DFM()`](https://docs.ropensci.org/dfms/reference/DFM.md)  

- [`summary(<dfm>)`](https://docs.ropensci.org/dfms/reference/summary.dfm.md)  

- [`plot(<dfm>)`](https://docs.ropensci.org/dfms/reference/plot.dfm.md)  

- [`as.data.frame(<dfm>)`](https://docs.ropensci.org/dfms/reference/as.data.frame.dfm.md)  

- [`residuals(<dfm>)`](https://docs.ropensci.org/dfms/reference/residuals.dfm.md)  

- [`fitted(<dfm>)`](https://docs.ropensci.org/dfms/reference/residuals.dfm.md)

**Generate Forecasts**

[`predict(<dfm>)`](https://docs.ropensci.org/dfms/reference/predict.dfm.md)  

- [`plot(<dfm_forecast>)`](https://docs.ropensci.org/dfms/reference/predict.dfm.md)  

- [`as.data.frame(<dfm_forecast>)`](https://docs.ropensci.org/dfms/reference/predict.dfm.md)  

**News Decomposition**

[`news(<dfm>)`](https://docs.ropensci.org/dfms/reference/news.md)  

- [`as.data.frame(<dfm_news_list>)`](https://docs.ropensci.org/dfms/reference/news.md)  

**Fast Stationary Kalman Filtering and Smoothing**

[`SKF()`](https://docs.ropensci.org/dfms/reference/SKF.md) — Stationary
Kalman Filter  
[`FIS()`](https://docs.ropensci.org/dfms/reference/FIS.md) — Fixed
Interval Smoother  
[`SKFS()`](https://docs.ropensci.org/dfms/reference/SKFS.md) —
Stationary Kalman Filter + Smoother  

**Helper Functions**

[`.VAR()`](https://docs.ropensci.org/dfms/reference/dot-VAR.md) — (Fast)
Barebones Vector-Autoregression  
[`ainv()`](https://docs.ropensci.org/dfms/reference/ainv.md) —
Armadillo's Inverse Function  
[`apinv()`](https://docs.ropensci.org/dfms/reference/ainv.md) —
Armadillo's Pseudo-Inverse Function  
[`tsnarmimp()`](https://docs.ropensci.org/dfms/reference/tsnarmimp.md) —
Remove and Impute Missing Values in a Multivariate Time Series  
[`em_converged()`](https://docs.ropensci.org/dfms/reference/em_converged.md)
— Convergence Test for EM-Algorithm  

**Data**

[`BM14_M`](https://docs.ropensci.org/dfms/reference/BM14_Models.md) —
Monthly Series by Banbura and Modugno (2014)  
[`BM14_Q`](https://docs.ropensci.org/dfms/reference/BM14_Models.md) —
Quarterly Series by Banbura and Modugno (2014)  
[`BM14_Models`](https://docs.ropensci.org/dfms/reference/BM14_Models.md)
— Series Metadata + Small/Medium/Large Model Specifications  

## References

Doz, C., Giannone, D., & Reichlin, L. (2011). A two-step estimator for
large approximate dynamic factor models based on Kalman filtering.
*Journal of Econometrics, 164*(1), 188-205.
<doi:10.1016/j.jeconom.2011.02.012>

Doz, C., Giannone, D., & Reichlin, L. (2012). A quasi-maximum likelihood
approach for large, approximate dynamic factor models. *Review of
Economics and Statistics, 94*(4), 1014-1024. <doi:10.1162/REST_a_00225>

Banbura, M., & Modugno, M. (2014). Maximum likelihood estimation of
factor models on datasets with arbitrary pattern of missing data.
*Journal of Applied Econometrics, 29*(1), 133-160.
<doi:10.1002/jae.2306>
