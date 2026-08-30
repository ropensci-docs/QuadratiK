# The Poisson kernel-based Distribution (PKBD)

The Poisson kernel-based densities are based on the normalized Poisson
kernel and are defined on the \\(d-1)\\-dimensional unit sphere. Given a
vector \\\mathbf{\mu} \in \mathcal{S}^{d-1}\\, where
\\\mathcal{S}^{d-1}= \\x \in \mathbb{R}^d : \|\|x\|\| = 1\\\\, and a
parameter \\\rho\\ such that \\0 \< \rho \< 1\\, the probability density
function of a \\d\\-variate Poisson kernel-based density is defined by:
\$\$f(\mathbf{x}\|\rho, \mathbf{\mu}) = \frac{1-\rho^2}{\omega_d
\|\|\mathbf{x} - \rho \mathbf{\mu}\|\|^d},\$\$ where \\\mu\\ is a vector
orienting the center of the distribution, \\\rho\\ is a parameter to
control the concentration of the distribution around the vector \\\mu\\
and it is related to the variance of the distribution. Recall that, for
\\x = (x_1, \ldots, x_d) \in \mathbb{R}^d\\, \\\|\|x\|\| = \sqrt{x_1^2 +
\ldots + x_d^2}\\. Furthermore, \\\omega_d = 2\pi^{d/2}
\[\Gamma(d/2)\]^{-1}\\ is the surface area of the unit sphere in
\\\mathbb{R}^d\\ (see Golzy and Markatou, 2020). When \\\rho \to 0\\,
the Poisson kernel-based density tends to the uniform density on the
sphere. Connections of the PKBDs to other distributions are discussed in
detail in Golzy and Markatou (2020). Here we note that when \\d=2\\,
PKBDs reduce to the wrapped Cauchy distribution. Additionally, with
precise choice of the parameters \\\rho\\ and \\\mu\\ the
two-dimensional PKBD becomes a two-dimensional projected normal
distribution. However, the connection with the \\d\\-dimensional
projected normal distributions does not carry beyond \\d=2\\. Golzy and
Markatou (2020) proposed an acceptance-rejection method for simulating
data from a PKBD using von Mises-Fisher envelopes (`rejvmf` method).
Furthermore Sablica, Hornik and Leydold (2023) proposed new ways for
simulating from the PKBD, using angular central Gaussian envelopes
(`rejacg`) or using the projected Saw distributions (`rejpsaw`).

## Usage

``` r
dpkb(x, mu, rho, logdens = FALSE)

rpkb(
  n,
  mu,
  rho,
  method = "rejacg",
  tol.eps = .Machine$double.eps^0.25,
  max.iter = 1000
)
```

## Arguments

- x:

  \\n \times d\\-matrix (or data.frame) of \\n\\ data point on the
  sphere \\\mathcal{S}^{d-1}\\, with \\d \ge 2\\.

- mu:

  location vector parameter with length indicating the dimension of
  generated points.

- rho:

  Concentration parameter, with \\0 \le\\ `rho` \\\< 1\\.

- logdens:

  Logical; if 'TRUE', densities are returned in logarithmic scale.

- n:

  number of observations.

- method:

  string that indicates the method used for sampling observations. The
  available methods are

  - `'rejvmf'` acceptance-rejection algorithm using von Mises-Fisher
    envelopes (Algorithm in Table 2 of Golzy and Markatou 2020);

  - `'rejacg'` using angular central Gaussian envelopes (Algorithm in
    Table 1 of Sablica et al. 2023);

  - `'rejpsaw'` using projected Saw distributions (Algorithm in Table 2
    of Sablica et al. 2023).

- tol.eps:

  the desired accuracy of convergence tolerance (for 'rejacg' method).

- max.iter:

  the maximum number of iterations (for 'rejacg' method).

## Value

`dpkb` gives the density value; `rpkb` generates random observations
from the PKBD.

## Details

This function `dpkb()` computes the density value for a given point `x`
from the Poisson kernel-based distribution with mean direction vector
`mu` and concentration parameter `rho`.

The number of observations generated is determined by `n` for `rpkb()`.
This function returns the \\(n \times d)\\-matrix of generated \\n\\
observations on \\\mathcal{S}^{(d-1)}\\.

A limitation of the `rejvmf` is that the method does not ensure the
computational feasibility of the sampler for \\\rho\\ approaching 1.

If the chosen method is 'rejacg', the function `uniroot`, from the
`stat` package, is used to estimate the beta parameter. In this case,
the complete results are provided as output.

## Note

If the required packages (`movMF` for `rejvmf` method, and `Tinflex` for
`rejpsaw`) are not installed, the function will display a message asking
the user to install the missing package(s).

## References

Golzy, M. and Markatou, M. (2020) Poisson Kernel-Based Clustering on the
Sphere: Convergence Properties, Identifiability, and a Method of
Sampling, Journal of Computational and Graphical Statistics, 29:4,
758-770, DOI: 10.1080/10618600.2020.1740713.

Sablica L., Hornik K. and Leydold J. (2023) "Efficient sampling from the
PKBD distribution", Electronic Journal of Statistics, 17(2), 2180-2209.

## Examples

``` r
# Generate some data from pkbd density
pkbd_dat <- rpkb(10, c(0.5, 0), 0.5)

# Calculate the PKBD density values
dens_val <- dpkb(pkbd_dat, c(0.5, 0.5), 0.5)
```
