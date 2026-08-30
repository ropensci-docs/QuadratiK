# Degrees of freedom (DOF) for the Normal kernel

Compute the Degrees of Freedom (DOF) of the normal Kernel centered with
respect to the standard normal distribution, given the dimension d and
the bandwidth parameter h.

## Usage

``` r
DOF_norm(Sigma_h, V)
```

## Arguments

- Sigma_h:

  covariance matrix of the gaussian kernel

- V:

  Covariance matrix of the tested distribution G

## Value

a list containing the DOF and the coefficient c of the asymptotic
distribution
