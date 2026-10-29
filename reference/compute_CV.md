# Compute the critical value for two-sample KBQD tests

This function computes the critical value for two-sample kernel tests
with centered Gaussian kernel using one of three methods: bootstrap,
permutation, or subsampling.

## Usage

``` r
compute_CV(
  B,
  Quantile,
  data_pool,
  size_x,
  size_y,
  h,
  method,
  b = 1,
  compute_variance
)
```

## Arguments

- B:

  the number of bootstrap/permutation/subsampling samples to generate.

- Quantile:

  the quantile of the bootstrap/permutation/subsampling distribution to
  use as the critical value.

- data_pool:

  a matrix containing the data to be used in the test.

- size_x:

  the number of rows in the `data_pool` matrix corresponding to group X.

- size_y:

  the number of rows in the `data_pool` matrix corresponding to group Y.

- h:

  the tuning parameter for the kernel test.

- method:

  the method to use for computing the critical value (one of
  "bootstrap", "permutation", or "subsampling").

- b:

  the subsampling block size (only used if `method` is "subsampling").

- compute_variance:

  indicates if the nonparametric variance is computed. Default is TRUE.

## Value

the critical value for the specified method and significance level.

## References

Markatou Marianthi & Saraceno Giovanni (2024). “A Unified Framework for
Multivariate Two- and k-Sample Kernel-based Quadratic Distance
Goodness-of-Fit Tests.” https://doi.org/10.48550/arXiv.2407.16374
