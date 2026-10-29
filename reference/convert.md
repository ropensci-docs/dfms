# Convert DFM to Other State Space Model Formats

Converts a `dfm` object to the state space representation used by the
dlm or KFAS packages, enabling their forecasting, smoothing, and
prediction-interval functionality.

## Usage

``` r
convert(object, ...)

# S3 method for class 'dfm'
convert(object, to = c("KFAS", "dlm"), ...)
```

## Arguments

- object:

  an object of class 'dfm'.

- ...:

  other arguments

- to:

  character, target package format: `"dlm"` or `"KFAS"`.

## Value

For `to = "dlm"`: a `dlm` object (see
[`dlm`](https://rdrr.io/pkg/dlm/man/dlm.html)).

For `to = "KFAS"`: an `SSModel` object (see
[`SSModel`](https://rdrr.io/pkg/KFAS/man/SSModel.html)).

## Details

The DFM is defined by the state space model:

- Observation equation: \\X_t = C F_t + e_t\\, \\e_t \sim N(0, R)\\

- Transition equation: \\F_t = A F\_{t-1} + u_t\\, \\u_t \sim N(0, Q)\\

where \\F_t\\ is the companion-form state vector of length \\r \cdot p\\
and \\A\\ is the companion transition matrix \\\[r \cdot p \times r
\cdot p\]\\.

For **dlm**: The system matrices map directly — `FF = C`, `GG = A`,
`V = R`, `W = Q`, with initial state `m0 = F[1,]` and covariance
`C0 = P[,,1]`. The user should pass standardized (scaled and centered)
data when using further dlm functions.

For **KFAS**: An `SSModel` is built via `SSMcustom` with `Z = C`,
`T = A`, `R = I`, `Q = Q`, `H = R` with initial state `a1 = F[1,]` and
covariance `P1 = P[,,1]`. The standardized data with original missing
values restored is embedded in the model object `y = X`.

## Examples

``` r
 if (FALSE) { # \dontrun{

mod <- DFM(BM14_Q, r=2, p=3)
 # Convert to dlm and run filter extract prediction variance
 if (requireNamespace("dlm", quietly = TRUE)) {
   dlm_mod <- convert(mod, to = "dlm")
   # Pass standardized data (scale each column) to dlmFilter
   fitf <- dlm::dlmFilter(scale(BM14_Q), dlm_mod)
   dlm::dlmSvd2var(fitf$U.R, fitf$D.R)
 }
 # Convert to KFAS and compute prediction intervals
 if (requireNamespace("KFAS", quietly = TRUE)) {
   kfas_mod <- convert(mod, to = "KFAS")
   predict(kfas_mod, n.ahead = 10, interval = "prediction",
           level = 0.95)
 }
} # }
```
