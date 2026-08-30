# Poisson kernel-based quadratic distance test of Uniformity on the sphere

This function performs the kernel-based quadratic distance
goodness-of-fit tests for Uniformity for multivariate spherical data `x`
on \\\mathcal{S}^{d-1}\\ using the Poisson kernel with concentration
parameter `rho`.  
The Poisson kernel-based test for uniformity exhibits excellent results
especially in the case of multimodal distributions, as shown in the
example of the [Uniformity test on the Sphere
vignette](https://docs.ropensci.org/QuadratiK/doc/uniformity.md).

## Usage

``` r
pk.test(x, rho, B = 300, Quantile = 0.95)

# S4 method for class 'ANY'
pk.test(x, rho, B = 300, Quantile = 0.95)

# S4 method for class 'pk.test'
show(object)
```

## Arguments

- x:

  A numeric \\(n \times d)\\-matrix of \\n\\ data points on the Sphere
  \\\mathcal{S}^(d-1)\\ as rows.

- rho:

  Concentration parameter of the Poisson kernel function.

- B:

  Number of Monte Carlo iterations for critical value estimation of Un
  (default: 300).

- Quantile:

  The quantile to use for critical value estimation, 0.95 is the default
  value.

- object:

  Object of class `pk.test`

## Value

An S4 object of class `pk.test` containing the results of the Poisson
kernel-based tests. The object contains the following slots:

- `method`: Description of the test performed.

- `x` Data matrix.

- `Tn` The value of the standardized U-statistic.

- `CV_Tn` The empirical critical value for Tn.

- `H0_Tn` A logical value indicating whether or not the null hypothesis
  is rejected according to Tn.

- `Sn` The value of the V-statistic Sn.

- `CV_Sn` The critical value for Sn computed following the asymptotic
  distribution.

- `H0_Sn` A logical value indicating whether or not the null hypothesis
  is rejected according to Sn.

- `rho` The value of concentration parameter used for the Poisson kernel
  function.

- `B` Number of replications for the critical value of the standardized
  U-statistic Tn.

## Details

Let \\x_1, x_2, ..., x_n\\ be a random sample with empirical
distribution function \\\hat F\\. We test the null hypothesis of
uniformity on the \\(d-1)\\-dimensional sphere, i.e. \\H_0:F=G\\, where
\\G\\ is the uniform distribution on the \\(d-1)\\-dimensional sphere
\\\mathcal{S}^{d-1}\\. We compute the U-statistic estimate of the sample
KBQD (Kernel-Based Quadratic Distance)
\$\$U\_{n}=\frac{1}{n(n-1)}\sum\_{i=2}^{n}\sum\_{j=1}^{i-1}K\_{cen}
(\mathbf{x}\_{i}, \mathbf{x}\_{j}),\$\$ then the first test statistic is
given as \$\$T\_{n}=\frac{U\_{n}}{\sqrt{Var(U\_{n})}},\$\$ with
\$\$Var(U\_{n})= \frac{2}{n(n-1)}
\left\[\frac{1+\rho^{2}}{(1-\rho^{2})^{d-1}}-1\right\],\$\$ and the
V-statistic estimate of the KBQD \$\$V\_{n} =
\frac{1}{n}\sum\_{i=1}^{n}\sum\_{j=1}^{n}K\_{cen} (\mathbf{x}\_{i},
\mathbf{x}\_{j}),\$\$ where \\K\_{cen}\\ denotes the Poisson kernel
\\K\_\rho\\ centered with respect to the uniform distribution on the
\\(d-1)\\-dimensional sphere, that is \$\$K\_{cen}(\mathbf{u},
\mathbf{v}) = K\_\rho(\mathbf{u}, \mathbf{v}) -1\$\$ and
\$\$K\_\rho(\mathbf{u}, \mathbf{v}) =
\frac{1-\rho^{2}}{\left(1+\rho^{2}- 2\rho (\mathbf{u}\cdot
\mathbf{v})\right)^{d/2}},\$\$ for every \\\mathbf{u}, \mathbf{v} \in
\mathcal{S}^{d-1} \times \mathcal{S}^{d-1}\\.

The asymptotic distribution of the V-statistic is an infinite
combination of weighted independent chi-squared random variables with
one degree of freedom. The cutoff value is obtained using the
Satterthwaite approximation \\c \cdot \chi\_{DOF}^2\\, where
\$\$c=\frac{(1+\rho^{2})-
(1-\rho^{2})^{d-1}}{(1+\rho)^{d}-(1-\rho^{2})^{d-1}}\$\$ and
\$\$DOF(K\_{cen} )=\left(\frac{1+\rho}{1-\rho} \right)^{d-1}\left\\
\frac{\left(1+\rho-(1-\rho)^{d-1} \right )^{2}}
{1+\rho^{2}-(1-\rho^{2})^{d-1}}\right \\.\$\$. For the \\U\\-statistic
the cutoff is determined empirically:

- Generate data from a Uniform distribution on the d-dimensional sphere;

- Compute the test statistics for `B` Monte Carlo(MC) replications;

- Compute the 95th quantile of the empirical distribution of the test
  statistic.

## Note

A U-statistic is a type of statistic that is used to estimate a
population parameter. It is based on the idea of averaging over all
possible *distinct* combinations of a fixed size from a sample. A
V-statistic considers all possible tuples of a certain size, not just
distinct combinations and can be used in contexts where unbiasedness is
not required.

## References

Ding, Y., Markatou, M. and Saraceno, G. (2023). “Poisson Kernel-Based
Tests for Uniformity on the d-Dimensional Sphere.” Statistica Sinica.
doi:10.5705/ss.202022.0347

## Examples

``` r
# create a pk.test object
x_sp <- sample_hypersphere(3, n_points = 100)
unif_test <- pk.test(x_sp, rho = 0.8)
unif_test
#> 
#>  Poisson Kernel-based quadratic distance test of 
#>                         Uniformity on the Sphere 
#> Selected concentration parameter rho:  0.8 
#> 
#> Tn-statistic:
#> 
#> H0 is rejected:  FALSE 
#> Statistic Tn:  0.3144173 
#> Critical value:  2.014814 
#> 
#> Sn-statistic:
#> 
#> H0 is rejected:  FALSE 
#> Statistic Sn:  45.51037 
#> Critical value:  52.23077 
#> 
```
