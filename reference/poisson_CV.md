# Compute the critical value for the Poisson KBQD tests for Uniformity

This function computes the empirical critical value for the U-statistics
for testing uniformity on the sphere based on the centered poisson
kernel.

## Usage

``` r
poisson_CV(d, size, rho, B, Quantile)
```

## Arguments

- d:

  the dimension of generated samples.

- size:

  the number of observations to be generated.

- rho:

  the concentration parameter for the Poisson kernel.

- B:

  the number of replications.

- Quantile:

  the quantile of the distribution use to select the critical value.

## Value

the critical value for the specified dimension, size and level.

## Details

For each replication, a sample of d-dimensional observations from the
uniform distribution on the Sphere are generated and the Poisson
kernel-based U-statistic is computed. After B iterations, the critical
value is selected as the `Quantile` of the empirical distribution of the
computed test statistics.

## References

Ding Yuxin, Markatou Marianthi, Saraceno Giovanni (2023). “Poisson
Kernel-Based Tests for Uniformity on the d-Dimensional Sphere.”
Statistica Sinica. doi: doi:10.5705/ss.202022.0347
