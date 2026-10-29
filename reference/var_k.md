# Exact variance of k-sample test

Compute the exact variance of kernel test for the k-sample problem under
the null hypothesis that F1=...=Fk.

## Usage

``` r
var_k(Kcen, sizes, cum_size)
```

## Arguments

- Kcen:

  the matrix with centered kernel values

- sizes:

  vector indicating sample's size.

- cum_size:

  vector indicating sample's cumulative sizes.

## Value

the value of computed variance.
