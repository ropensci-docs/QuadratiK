# Generate two samples data from skew-normal distributions

This function generates data from skew-normal distributions with the
specified parameters of means and covariance matrices.

## Usage

``` r
generate_SN(d, size_x, size_y, mu_x, mu_y, sigma_x, sigma_y, skewness_y)
```

## Arguments

- d:

  number of dimensions.

- size_x:

  the number of observations for sample X

- size_y:

  the number of observations for sample Y

- mu_x:

  the mean of X

- mu_y:

  the mean of Y

- sigma_x:

  the standard deviation of X

- sigma_y:

  the standard deviation of Y

- skewness_y:

  the skewness of Y (the skewness of X is set to zero).

## Value

a list containing the generated X and Y data sets.
