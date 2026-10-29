# Row-wise log-sum-exp

Compute the row-wise log-sum-exp of a numeric matrix in a numerically
stable way. This is used to evaluate \\\log \sum_k \exp(x\_{ik})\\
without overflow or underflow by subtracting the row maximum before
exponentiation.

## Usage

``` r
row_log_sum_exp(mat)
```

## Arguments

- mat:

  A numeric matrix of size \\n \times K\\.

## Value

A numeric vector of length \\n\\ where the i-th entry is \\\log
\sum\_{k=1}^K \exp(mat\_{ik})\\. Rows containing only `-Inf` return
`-Inf`.
