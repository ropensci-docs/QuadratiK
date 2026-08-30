# Kernel-based quadratic distance (KBQD) Goodness-of-Fit tests

This function performs the kernel-based quadratic distance
goodness-of-fit tests. It includes tests for multivariate normality,
two-sample tests and \\k\\-sample tests.

## Usage

``` r
kb.test(
  x,
  y = NULL,
  h = NULL,
  method = "subsampling",
  B = 150,
  b = NULL,
  Quantile = 0.95,
  mu = NULL,
  Sigma = NULL,
  centeringType = "Nonparam",
  K_threshold = 10,
  alternative = NULL
)

# S4 method for class 'ANY'
kb.test(
  x,
  y = NULL,
  h = NULL,
  method = "subsampling",
  B = 150,
  b = 0.9,
  Quantile = 0.95,
  mu = NULL,
  Sigma = NULL,
  centeringType = "Nonparam",
  K_threshold = 10,
  alternative = NULL
)

# S4 method for class 'kb.test'
show(object)
```

## Arguments

- x:

  Numeric matrix or vector of data values.

- y:

  Numeric matrix or vector of data values. Depending on the input `y`,
  the corresponding test is performed.

  - if `y` = NULL, the function performs the tests for normality on `x`

  - if `y` is a data matrix, with same dimensions of `x`, the function
    performs the two-sample test between `x` and `y`.

  - if `y` is a numeric or factor vector, indicating the group
    memberships for each observation, the function performs the k-sample
    test.

- h:

  Bandwidth for the kernel function. If a value is not provided, the
  algorithm for the selection of an optimal h is performed
  automatically. See the function
  [`select_h`](https://docs.ropensci.org/QuadratiK/reference/select_h.md)
  for more details.

- method:

  The method used for critical value estimation ("subsampling",
  "bootstrap", or "permutation")(default: "subsampling").

- B:

  The number of iterations to use for critical value estimation
  (default: 150).

- b:

  The size of the subsamples used in the subsampling algorithm (default:
  0.8).

- Quantile:

  The quantile to use for critical value estimation, 0.95 is the default
  value.

- mu:

  Mean vector for the reference distribution. Mandatory for the
  normality test and parametric two-sample test.

- Sigma:

  Covariance matrix of the reference distribution. Mandatory for the
  normality test and parametric two-sample test.

- centeringType:

  String indicating the method used for centering the normal kernel
  ('Param' or 'Nonparam').

- K_threshold:

  maximum number of groups allowed. Default is 10. It is a control
  parameter. Change in case of more than 10 samples.

- alternative:

  Family of alternative chosen for selecting h, between "location",
  "scale" and "skewness" (only if `h` is not provided). Default is
  "location" for the normality test and "skewness" for the two-sample
  and k-sample tests. Note that "skewness" is not available for the
  normality test.

- object:

  Object of class `kb.test`

## Value

An S4 object of class `kb.test` containing the results of the
kernel-based quadratic distance tests, based on the normal kernel. The
object contains the following slots:

- `method`: Description of the kernel-based quadratic distance test
  performed.

- `data` Data list of samples X (and Y).

- `Un` The value of the U-statistic (for Normality test).

- `Vn` The value of the V-statistic (for Normality test).

- `Dn` The value of the Dn statistic (for two- and k-sample tests).

- `Trace` The value of the Trace statistic (for two- and k-sample
  tests).

- `H0_Un` A logical value indicating whether or not the null hypothesis
  is rejected according to Un.

- `H0_Vn` A logical value indicating whether or not the null hypothesis
  is rejected according to Vn.

- `H0_Dn` A logical value indicating whether or not the null hypothesis
  is rejected according to Dn.

- `H0_Trace` A logical value indicating whether or not the null
  hypothesis is rejected according to Trace.

- `CV_Un` The critical value computed for the test Un.

- `CV_Vn` The critical value computed for the test Vn.

- `CV_Dn` The critical value computed for the test Dn.

- `CV_Trace` The critical value computed for the test Trace.

- `h` List with the value of bandwidth parameter used for the normal
  kernel function. If `select_h` is used, the matrix of computed power
  values and the corresponding power plot are also provided.

- `B` Number of bootstrap/permutation/subsampling replications.

- `var_Un` exact variance of the kernel-based U-statistic.

- `var_Dn` exact variance of the kernel-based Dn-statistic.

- `var_Trace` exact variance of the kernel-based Trace-statistic.

- `cv_method` The method used to estimate the critical value (one of
  "subsampling", "permutation" or "bootstrap").

## Details

The function `kb.test` performs the kernel-based quadratic distance
tests using the Gaussian kernel with bandwidth parameter `h`. Depending
on the shape of the input `y` the function performs the tests of
multivariate normality, the non-parametric two-sample tests or the
k-sample tests.

The quadratic distance between two probability distributions \\F\\ and
\\G\\ is defined as \$\$d\_{K}(F,G)=\iint K(x,y)d(F-G)(x)d(F-G)(y),\$\$
where \\G\\ is a distribution whose goodness of fit we wish to assess
and \\K\\ denotes the Normal kernel defined as \$\$ K\_{{h}}(\mathbf{s},
\mathbf{t}) = (2 \pi)^{-d/2}
\left(\det{\mathbf{\Sigma}\_h}\right)^{-\frac{1}{2}}
\exp\left\\-\frac{1}{2}(\mathbf{s} - \mathbf{t})^\top
\mathbf{\Sigma}\_h^{-1}(\mathbf{s} - \mathbf{t})\right\\,\$\$ for every
\\\mathbf{s}, \mathbf{t} \in \mathbb{R}^d \times \mathbb{R}^d\\, with
covariance matrix \\\mathbf{\Sigma}\_h=h^2 I\\ and tuning parameter
\\h\\.  

- **Test for Normality**:  
  Let \\x_1, x_2, ..., x_n\\ be a random sample with distribution
  function \\F\\. We test the null hypothesis of normality, i.e.
  \\H_0:F=G=\mathcal{N}\_d(\mu, \Sigma)\\.

  We consider the U-statistic estimate of the sample KBQD
  \$\$U\_{n}=\frac{1}{n(n-1)}\sum\_{i=2}^{n}\sum\_{j=1}^{i-1}
  K\_{cen}(\mathbf{x}\_{i}, \mathbf{x}\_{j}),\$\$ then the first test
  statistics is \$\$T\_{n}=\frac{U\_{n}}{\sqrt{Var(U\_{n})}},\$\$ with
  \\Var(U_n)\\ computed exactly following Lindsay et al.(2014), and the
  V-statistic estimate \$\$V\_{n} = \frac{1}{n}\sum\_{i=1}^{n}
  \sum\_{j=1}^{n}K\_{cen}(\mathbf{x}\_{i}, \mathbf{x}\_{j}),\$\$ where
  \\K\_{cen}\\ denotes the Normal kernel \\K_h\\ with parametric
  centering with respect to the considered normal distribution \\G =
  \mathcal{N}\_d(\mu, \Sigma)\\.

  The asymptotic distribution of the V-statistic is an infinite
  combination of weighted independent chi-squared random variables with
  one degree of freedom. The cutoff value is obtained using the
  Satterthwaite approximation \\c \cdot \chi\_{DOF}^2\\, where \\c\\ and
  \\DOF\\ are computed exactly following the formulas in Lindsay et
  al.(2014).

  For the \\U\\-statistic the cutoff is determined empirically:

  - Generate data from the considered normal distribution ;

  - Compute the test statistics for `B` Monte Carlo(MC) replications;

  - Compute the 95th quantile of the empirical distribution of the test
    statistic.

- **k-sample test**:  
  Consider \\k\\ random samples of i.i.d. observations
  \\\mathbf{x}^{(i)}\_1, \mathbf{x}^{(i)}\_{2},\ldots,
  \mathbf{x}^{(i)}\_{n_i} \sim F_i\\, \\i = 1, \ldots, k\\. We test if
  the samples are generated from the same *unknown* distribution, that
  is \\H_0: F_1 = F_2 = \ldots = F_k\\ versus \\H_1: F_i \not = F_j\\,
  for some \\1 \le i \not = j \le k\\.  
  We construct a matrix distance \\\hat{\mathbf{D}}\\, with off-diagonal
  elements \$\$\hat{D}\_{ij} = \frac{1}{n_i n_j} \sum\_{\ell=1}^{n_i}
  \sum\_{r=1}^{n_j}K\_{\bar{F}}(\mathbf{x}^{(i)}\_\ell,\mathbf{x}^{(j)}\_r),
  \qquad \mbox{ for }i \not= j\$\$ and in the diagonal \$\$\hat{D}\_{ii}
  = \frac{1}{n_i (n_i -1)} \sum\_{\ell=1}^{n_i} \sum\_{r\not=
  \ell}^{n_i} K\_{\bar{F}}(\mathbf{x}^{(i)}\_\ell, \mathbf{x}^{(i)}\_r),
  \qquad \mbox{ for }i = j,\$\$ where \\K\_{\bar{F}}\\ denotes the
  Normal kernel \\K_h\\ centered non-parametrically with respect to
  \$\$\bar{F} = \frac{n_1 \hat{F}\_1 + \ldots + n_k \hat{F}\_k}{n},
  \quad \mbox{ with } n=\sum\_{i=1}^k n_i.\$\$

  We compute the trace statistic \$\$\mathrm{trace}(\hat{\mathbf{D}}\_n)
  = \sum\_{i=1}^{k}\hat{D}\_{ii}\$\$ and \\D_n\\, derived considering
  all the possible pairwise comparisons in the *k*-sample null
  hypothesis, given as \$\$D_n = (k-1)
  \mathrm{trace}(\hat{\mathbf{D}}\_n) - 2 \sum\_{i=1}^{k}\sum\_{j\>
  i}^{k}\hat{D}\_{ij}.\$\$

  We compute the empirical critical value by employing numerical
  techniques such as the bootstrap, permutation and subsampling
  algorithms:

  - Generate k-tuples, of total size \\n_B\\, from the pooled sample
    following one of the sampling methods;

  - Compute the k-sample test statistic;

  - Repeat `B` times;

  - Select the \\95^{th}\\ quantile of the obtained values.

- **Two-sample test**:  
  Let \\x_1, x_2, ..., x\_{n_1} \sim F\\ and \\y_1, y_2, ..., y\_{n_2}
  \sim G\\ be random samples from the distributions \\F\\ and \\G\\,
  respectively. We test the null hypothesis that the two samples are
  generated from the same *unknown* distribution, that is \\H_0: F=G\\
  vs \\H_1:F\not=G\\. The test statistics coincide with the \\k\\-sample
  test statistics when \\k=2\\.

### Kernel centering

The arguments `mu` and `Sigma` indicate the normal model considered for
the normality test, that is \\H_0: F = N(\\`mu`, `Sigma`). For the
two-sample test, `mu` and `Sigma` can be used for the parametric
centering of the kernel, in the case we want to specify the reference
distribution, with `centeringType = "Param"`. This is the method used
when the test for normality is performed. The normal kernel centered
with respect to \\G \sim N_d(\mathbf{\mu}, \mathbf{V})\\ can be computed
as \$\$K\_{cen(G)}(\mathbf{s}, \mathbf{t}) =
K\_{\mathbf{\Sigma_h}}(\mathbf{s}, \mathbf{t}) - K\_{\mathbf{\Sigma_h} +
\mathbf{V}}(\mathbf{\mu}, \mathbf{t}) - K\_{\mathbf{\Sigma_h} +
\mathbf{V}}(\mathbf{s}, \mathbf{\mu}) + K\_{\mathbf{\Sigma_h} +
2\mathbf{V}}(\mathbf{\mu}, \mathbf{\mu}).\$\$ We consider the
non-parametric centering of the kernel with respect to \\\bar{F}=(n_1
F_1 + \ldots n_k F_k)/n\\ where \\n=\sum\_{i=1}^k n_i\\, with
`centeringType = "Nonparam"`, for the two- and \\k\\-sample tests. Let
\\\mathbf{z}\_1,\ldots, \mathbf{z}\_n\\ denote the pooled sample. For
any \\s,t \in \\\mathbf{z}\_1,\ldots, \mathbf{z}\_n\\\\, it is given by
\$\$K\_{cen(\bar{F})}(\mathbf{s},\mathbf{t}) =
K(\mathbf{s},\mathbf{t}) - \frac{1}{n}\sum\_{i=1}^{n}
K(\mathbf{s},\mathbf{z}\_i) - \frac{1}{n}\sum\_{i=1}^{n}
K(\mathbf{z}\_i,\mathbf{t}) + \frac{1}{n(n-1)}\sum\_{i=1}^{n} \sum\_{j
\not=i}^{n} K(\mathbf{z}\_i,\mathbf{z}\_j).\$\$

## Note

For the two- and \\k\\-sample tests, the slots `Un`, `Vn`, `CV_Un` and
`CV_Vn` are empty, while the computed statistics are reported in slots
`Dn`, `Trace`, `CV_Dn` and `CV_Trace`. The logical results of the tests
are reported in `H0_Dn` and `H0_Trace`.

A U-statistic is a type of statistic that is used to estimate a
population parameter. It is based on the idea of averaging over all
possible *distinct* combinations of a fixed size from a sample. A
V-statistic considers all possible tuples of a certain size, not just
distinct combinations and can be used in contexts where unbiasedness is
not required.

## References

Markatou, M. and Saraceno, G. (2024). “A Unified Framework for
Multivariate Two- and k-Sample Kernel-based Quadratic Distance
Goodness-of-Fit Tests.”  
https://doi.org/10.48550/arXiv.2407.16374

Lindsay, B.G., Markatou, M. and Ray, S. (2014) "Kernels, Degrees of
Freedom, and Power Properties of Quadratic Distance Goodness-of-Fit
Tests", Journal of the American Statistical Association, 109:505,
395-410, DOI: 10.1080/01621459.2013.836972

## Examples

``` r
# create a kb.test object
x <- matrix(rnorm(100), ncol = 2)
y <- matrix(rnorm(100), ncol = 2)

# Normality test
my_test <- kb.test(x, h=0.5, mu = c(0,0), Sigma = diag(2))
my_test
#> 
#>  Kernel-based quadratic distance Normality test 
#> Statistics         U-statistic  V-statistic 
#> --------------------------------------------
#> Test Statistic:    1.310854     0.7979308   
#> Critical Value:    2.4409       6.071062    
#> H0 is rejected:    FALSE        FALSE       
#> Selected tuning parameter h:  0.5 
#> 

# Two-sample test
my_test <- kb.test(x, y, h = 0.5, method = "subsampling", b = 0.9,
                   centeringType = "Nonparam")
my_test
#> 
#>  Kernel-based quadratic distance two-sample test 
#> Statistics         Dn           Trace       
#> --------------------------------------------
#> Test Statistic:    0.1153108    0.133021    
#> Critical Value:    1.407721     1.625753    
#> H0 is rejected:    FALSE        FALSE       
#> CV method:  subsampling 
#> Selected tuning parameter h:  0.5 
#> 

# k-sample test
z <- matrix(rnorm(100, 2), ncol = 2)
dat <- rbind(x, y, z)
group <- rep(c(1, 2, 3), each = 50)
my_test <- kb.test(x = dat, y = group, h = 0.5, method = "subsampling", b = 0.9)
my_test
#> 
#>  Kernel-based quadratic distance k-sample test 
#> Statistics         Dn           Trace       
#> --------------------------------------------
#> Test Statistic:    7.351993     11.60926    
#> Critical Value:    1.14846      1.814843    
#> H0 is rejected:    TRUE         TRUE        
#> CV method:  subsampling 
#> Selected tuning parameter h:  0.5 
#> 
```
