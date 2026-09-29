# Compute the critical value for the KBQD k-sample tests

This function computes the empirical critical value for the k-sample
KBQD tests using the centered Gaussian kernel, with bootstrap,
permutation, or subsampling.

## Usage

``` r
cv_ksample(
  x,
  y,
  h,
  B = 150,
  b = 0.9,
  Quantile = 0.95,
  method = "subsampling",
  compute_variance = TRUE
)
```

## Arguments

- x:

  matrix containing the observations to be used in the k-sample test

- y:

  vector indicating the sample for each observation

- h:

  the tuning parameter for the test using the Gaussian kernel

- B:

  the number of bootstrap/permutation/subsampling samples to generate

- b:

  the subsampling block size (only used if `method` is "subsampling")

- Quantile:

  the quantile of the bootstrap/permutation/subsampling distribution to
  use as the critical value

- method:

  the method to use for computing the critical value (one of
  "bootstrap", "permutation")

- compute_variance:

  indicates if the nonparametric variance is computed. Default is TRUE.

## Value

a vector of two critical values corresponding to different formulation
of the k-sample test statistics.
