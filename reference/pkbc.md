# Poisson kernel-based clustering on the sphere

The function `pkbc()` performs the Poisson kernel-based clustering
algorithm on the sphere proposed by Golzy and Markatou (2020). The
proposed algorithm is based on a mixture, with \\M\\ components, of
Poisson kernel-based densities on the hypersphere \\\mathcal{S}^{d-1}\\
given by \$\$f(x\|\Theta) = \sum\_{j=1}^M \alpha_j f_j(x\|\rho_j,
\mu_j)\$\$ where \\\alpha_j\\'s are the mixing proportions and
\\f_j(x\|\rho_j, \mu_j)\\'s denote the probability density function of a
\\d\\-variate Poisson kernel-based density given as
\$\$f(\mathbf{x}\|\rho, \mathbf{\mu}) = \frac{1-\rho^2}{\omega_d
\|\|\mathbf{x} - \rho \mathbf{\mu}\|\|^d}.\$\$ The parameters
\\\alpha_j, \mu_j, \rho_j\\ are estimated through a iterative reweighted
EM algorithm.  
The proposed clustering algorithm exhibits excellent results when (1)
the clusters are not well separated; (2) the data points are fairly well
concentrated around the vectors \\\mu_j\\ of each cluster; (3) the
percentage of noise in the data increases.

## Usage

``` r
pkbc(
  dat,
  nClust,
  maxIter = 300,
  stoppingRule = "loglik",
  initMethod = "sampleData",
  numInit = 10
)

# S4 method for class 'ANY'
pkbc(
  dat,
  nClust,
  maxIter = 300,
  stoppingRule = "loglik",
  initMethod = "sampleData",
  numInit = 10
)

# S4 method for class 'pkbc'
show(object)
```

## Arguments

- dat:

  \\(n \times d)\\-data matrix or data.frame of data points on the
  sphere to be clustered. The observations in `dat` are normalized by
  dividing with the length of the vector to ensure that they lie on the
  \\d\\-dimensional sphere. Note that \\d \> 1\\.

- nClust:

  Number of clusters. It can be a single value or a numeric vector.

- maxIter:

  The maximum number of iterations before a run is terminated.

- stoppingRule:

  String describing the stopping rule to be used within each run.
  Currently must be either `'max'`, `'membership'`, or `'loglik'`.

- initMethod:

  String describing the initialization method to be used. Currently must
  be `'sampleData'`.

- numInit:

  Number of initialization.

- object:

  Object of class `pkbc`

## Value

An S4 object of class `pkbc` containing the results of the clustering
procedure based on Poisson kernel-based distributions. The object
contains the following slots:

`res_k`: List of results of the Poisson kernel-based clustering
algorithm for each value of number of clusters specified in `nClust`.
Each object in the list contains:

- `postProbs` Posterior probabilities of each observation for the
  indicated clusters.

- `LogLik` Maximum value of log-likelihood function

- `wcss` Values of within-cluster sum of squares computed with Euclidean
  distance and cosine similarity, respectively.

- `params` List of estimated parameters of the mixture model

  - `mu` estimated centroids

  - `rho` estimated concentration parameters rho

  - `alpha` estimated mixing proportions

- `finalMemb` Vector of final memberships

- `runInfo` List of information of the EM algorithm iterations

  - `lokLikVec` vector of log-likelihood values

  - `numIterPerRun` number of E-M iterations per run

`input`: List of input information.

## Details

We set all concentration parameters equal to 0.5 and all mixing
proportions to be equal.  
The initialization method `'sampleData'` indicates that observation
points are randomly chosen as initializers of the centroids \\\mu_j\\.
This random starts strategy has a chance of not obtaining initial
representatives from the underlying clusters, then the clustering is
performed `numInit` times and the random start with the highest
likelihood is chosen as the final estimate of the parameters.

The possible `stoppingRule` for each iteration are:  

- `'loglik'` run the algorithm until the change in log-likelihood from
  one iteration to the next is less than a given threshold (1e-7)  

- `'membership'` run the algorithm until the membership is unchanged for
  all points from one iteration to the next  

- `'max'` reach a maximum number of iterations `maxIter`

The obtained estimates are used for assigning final memberships,
identifying the `nClust` clusters, according to the following rule
\$\$P(x_i, \Theta) = \arg\max\_{j \in \\1, \ldots, k\\} \\
\frac{\alpha_j f_j(x_i\|\mu_j, \rho_j)}{f(x_i, \Theta)}\\.\$\$ The
number of clusters `nClust` must be provided as input to the clustering
algorithm.

## Note

The clustering algorithm is tailored for data points on the sphere
\\\mathcal{S}^{d-1}\\, but it can also be performed on spherically
transformed observations, i.e. data points on the Euclidean space
\\\mathbb{R}^d\\ that are normalized such that they lie on the
corresponding \\(d-1)\\-dimensional sphere \\\mathcal{S}^{d-1}\\.

## References

Golzy, M. and Markatou, M. (2020) Poisson Kernel-Based Clustering on the
Sphere: Convergence Properties, Identifiability, and a Method of
Sampling, Journal of Computational and Graphical Statistics, 29:4,
758-770, DOI: 10.1080/10618600.2020.1740713.

## See also

[`dpkb()`](https://docs.ropensci.org/QuadratiK/reference/dpkb.md) and
[`rpkb()`](https://docs.ropensci.org/QuadratiK/reference/dpkb.md) for
more information on the Poisson kernel-based distribution.

## Examples

``` r
# We generate three samples of 100 observations from 3-dimensional
# Poisson kernel-based densities with rho=0.8 and different mean directions
size <- 100
groups <- c(rep(1, size), rep(2, size), rep(3, size))
rho <- 0.8
set.seed(081423)
data1 <- rpkb(size, c(1, 0, 0), rho)
data2 <- rpkb(size, c(0, 1, 0), rho)
data3 <- rpkb(size, c(0, 0, 1), rho)
dat <- rbind(data1, data2, data3)

# Perform the clustering algorithm with number of clusters k=3.
pkbd <- pkbc(dat = dat, nClust = 3)
show(pkbd)
#> Poisson Kernel-Based Clustering on the Sphere (pkbc) Object
#> ------------------------------------------------------------
#> 
#> Available components:
#> Input Parameters:
#> [1] "dat"          "nClust"       "maxIter"      "stoppingRule" "initMethod"  
#> [6] "numInit"     
#> 
#> 
#> Considered possible number of clusters:  3 
#> 
#> Available components for each value of number of clusters: 
#> [1] "postProbs" "LogLik"    "wcss"      "params"    "finalMemb" "runInfo"  
```
