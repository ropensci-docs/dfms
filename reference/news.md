# News Decomposition

Compute the Banbura and Modugno (2014) news decomposition of forecast
updates. Given an old vintage and an updated vintage, the function
decomposes the forecast revision at `t.fcst` into contributions from new
releases.

## Usage

``` r
news(object, ...)

# S3 method for class 'dfm'
news(
  object,
  comparison,
  t.fcst = nrow(object$X_imp),
  target.vars = NULL,
  series = NULL,
  standardized = FALSE,
  ...
)

# S3 method for class 'dfm_news'
print(x, digits = 4L, ...)

# S3 method for class 'dfm_news_list'
print(x, digits = 4L, ...)

# S3 method for class 'dfm_news_list'
x$name

# S3 method for class 'dfm_news_list'
x[[i]]

# S3 method for class 'dfm_news_list'
x[i]

# S3 method for class 'dfm_news_list'
as.data.frame(x, ...)
```

## Arguments

- object:

  a `dfm` object for the old vintage.

- ...:

  not used.

- comparison:

  a `dfm` object or a new dataset for the updated vintage.

- t.fcst:

  integer. Forecast target time index.

- target.vars:

  Integer or character identifying target variables. Defaults to all
  variables.

- series:

  optional character vector for naming variables.

- standardized:

  logical. Return results on standardized scale?

- x:

  an object of class 'dfm_news' or 'dfm_news_list'.

- digits:

  integer. Number of digits to print.

- name:

  character. Element name.

- i:

  index. Element position or name.

## Value

For a single target, a `dfm_news` object with elements:

- `y_old`: old forecast for the target variable at `t.fcst`.

- `y_new`: new forecast for the target variable at `t.fcst`.

- `news_df`: data frame with one row per series and columns:

  - `series`: series name.

  - `actual`: actual release (if any).

  - `forecast`: old-vintage forecast of the release.

  - `news`: total innovation for the series on the output scale. If
    there is a single release, `news` equals `actual - forecast`. With
    multiple releases, `news` aggregates those innovations for the
    series.

  - `gain`: effective weight on `news` such that `impact = news * gain`
    (on the output scale).

  - `gain_std`: effective weight on the standardized innovations.

  - `impact`: contribution of the series to the target revision.

If `target.vars` selects multiple targets, a `dfm_news_list` object is
returned, where each element is a `dfm_news` object and list names
correspond to targets.

## Details

Let \\y_t^{old}\\ and \\y_t^{new}\\ be the old and new forecasts of a
target series at \\t = t\_{fcst}\\. For each new release \\i\\ (a
previously missing observation that becomes observed), the innovation is
\$\$\nu_i = x_i^{new} - \hat{x}\_i^{old},\$\$ where \\\hat{x}\_i^{old}\\
is the smoothed estimate from the old vintage. The revision is
decomposed as \$\$y_t^{new} - y_t^{old} = \sum_i g_i \nu_i,\$\$ with
gain weights computed from Kalman smoother covariances: \$\$g = \sigma_y
C_y P_1 P_2^{-1}.\$\$ Here \\\sigma_y\\ is the target series standard
deviation, \\C_y\\ is the loading row for the target series, \\P_1\\
collects cross-covariances between the target and each news item, and
\\P_2\\ is the covariance matrix of the news items (including
measurement error where appropriate). See Section 2.3 and Appendix D in
Banbura and Modugno (2014).

The function uses the system matrices and scaling from the new vintage.
The old data are re-standardized to the new-vintage scale before
smoothing so that innovations and gains are computed on a consistent
scale. Set `standardized = FALSE` to report results on the original data
scale.

## Note

This implementation is translated from the original MATLAB codes and is
consistent with the BM2014 news decomposition formulas. If the model was
estimated with `max.missing < 1` and `na.rm.method = "LE"` in
[`tsnarmimp`](https://docs.ropensci.org/dfms/reference/tsnarmimp.md)
(called by [`DFM()`](https://docs.ropensci.org/dfms/reference/DFM.md)),
leading or trailing rows with many missing values may be removed by
[`DFM()`](https://docs.ropensci.org/dfms/reference/DFM.md). If old and
new vintages are both dfm objects, and they drop different rows, then
`t.fcst` can become out of bounds. When `comparison` is provided as raw
data, `news()` drops `object$rm.rows` from the new dataset (if present)
and forces `max.missing = 1` for the re-estimation call to keep row
alignment. To avoid issues, estimate both vintages with
`max.missing = 1`. For mixed-frequency or idiosyncratic AR(1) models,
`news()` relies on the full state-space matrices stored in
`dfm$ss_full`.

## References

Banbura, M., & Modugno, M. (2014). Maximum likelihood estimation of
factor models on datasets with arbitrary pattern of missing data.
*Journal of Applied Econometrics, 29*(1), 133-160.

## See also

[dfms-package](https://docs.ropensci.org/dfms/reference/dfms-package.md)

## Examples

``` r
# \donttest{
# (1) Monthly DFM example
X <- collapse::qM(BM14_M)[, BM14_Models$medium[BM14_Models$freq == "M"]]
X_old <- X
# Creating earlier vintage
X_old[nrow(X) - 1, sample(which(is.finite(X[nrow(X) - 1, ]) & is.na(X[nrow(X), ])), 5)] <- NA
X_old[nrow(X), sample(which(is.finite(X[nrow(X), ])), 5)] <- NA
# Estimating DFM
dfm <- DFM(X_old, r = 2, p = 2, em.method = "none")
# News computation (second DFM fit internally with same settings and rows)
res <- news(dfm, X, target.vars = c("ip_tot_cstr", "orders", "urx"))
# See results
print(res)
#> DFM News (Multiple Targets)
#> Target time: 357 
#> Targets: 3 
#> Standardized: FALSE 
#>               y_old   y_new revision
#> ip_tot_cstr 94.8544 94.7225  -0.1319
#> orders      97.0352 96.9593  -0.0759
#> urx          8.7270  8.7335   0.0065
head(res$news_df)
#> NULL

# (2) MQ nowcast of GDP (idio.ar1 = FALSE for speed)
library(magrittr)
library(xts)
# Creating MQ dataset
BM14 <- merge(BM14_M, BM14_Q)
BM14[, BM14_Models$log_trans] %<>% log()
BM14[, BM14_Models$freq == "M"] %<>% diff()
BM14[, BM14_Models$freq == "Q"] %<>% diff(3)
X <- BM14[-1, BM14_Models$small]
quarterly.vars <- BM14_Models$series[BM14_Models$small & BM14_Models$freq == "Q"]
# Creating earlier vintage
X_old <- X
X_old[355, c("ip_tot_cstr", "new_cars")] <- NA
X_old[356, c("new_cars", "pms_pmi", "euro325", "capacity")] <- NA
# Estimating DFM
dfm <- DFM(X_old, r = 2, p = 2, quarterly.vars = quarterly.vars, max.missing = 1)
#> Converged after 26 iterations.
# News computation (second DFM fit internally with same settings and rows)
res_mq <- news(dfm, X, t.fcst = 356, target.vars = "gdp")
#> Converged after 26 iterations.
# See results
print(res_mq)
#> DFM News
#> Target variable: gdp 
#> Target time: 356 
#> Old forecast: 0.0064 
#> New forecast: 0.0062 
#> Revision: -2e-04 
#> Standardized: FALSE 
head(res_mq$news_df)
#>              series       actual    forecast         news         gain
#> 1       ip_tot_cstr  0.009399179 0.006538173  0.002861006 0.0218073085
#> 2          new_cars -0.008605272 0.004274292 -0.008834552 0.0002129116
#> 3            orders           NA          NA  0.000000000 0.0000000000
#> 4 ret_turnover_defl           NA          NA  0.000000000 0.0000000000
#> 5   ecs_ec_sent_ind           NA          NA  0.000000000 0.0000000000
#> 6           pms_pmi  1.050000000 2.120030865 -1.070030865 0.0001220146
#>       gain_std        impact
#> 1 2.022429e-04  6.239084e-05
#> 2 1.071131e-05 -1.880979e-06
#> 3 0.000000e+00  0.000000e+00
#> 4 0.000000e+00  0.000000e+00
#> 5 0.000000e+00  0.000000e+00
#> 6 1.586910e-04 -1.305593e-04
# }
```
