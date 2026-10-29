# Compute the critical value for the KBQD tests for multivariate Normality

This function computes the empirical critical value for the Normality
test based on the KBQD tests using the centered Gaussian kernel.

## Usage

``` r
normal_CV(d, size, h, mu_hat, Sigma_hat, B = 150, Quantile = 0.95)
```

## Arguments

- d:

  the dimension of generated samples.

- size:

  the number of observations to be generated.

- h:

  the concentration parameter for the Gaussian kernel.

- mu_hat:

  Mean vector for the reference distribution.

- Sigma_hat:

  Covariance matrix of the reference distribution.

- B:

  the number of replications.

- Quantile:

  the quantile of the distribution use to select the critical value

## Value

the critical value for the specified dimension, size and level.

## Details

For each replication, a sample from the d-dimensional Normal
distribution with mean vector `mu_hat` and covariance matrix `Sigma_hat`
is generated and the KBQD test U-statistic for Normality is computed.
After B iterations, the critical value is selected as the `Quantile` of
the empirical distribution of the computed test statistics.
