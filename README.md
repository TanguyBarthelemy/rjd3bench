
<!-- README.md is generated from README.Rmd. Please edit that file -->

# `rjd3bench` <a href="https://rjdverse.github.io/rjd3bench/"><img src="man/figures/logo.png" align="right" height="150" style="float:right; height:150px;"/></a>

<!-- badges: start -->

[![CRAN
status](https://www.r-pkg.org/badges/version/rjd3bench)](https://CRAN.R-project.org/package=rjd3bench)

[![R-CMD-check](https://github.com/rjdverse/rjd3bench/actions/workflows/R-CMD-check.yaml/badge.svg)](https://github.com/rjdverse/rjd3bench/actions/workflows/R-CMD-check.yaml)
[![lint](https://github.com/rjdverse/rjd3bench/actions/workflows/lint.yaml/badge.svg)](https://github.com/rjdverse/rjd3bench/actions/workflows/lint.yaml)

[![GH Pages
built](https://github.com/rjdverse/rjd3bench/actions/workflows/pkgdown.yaml/badge.svg)](https://github.com/rjdverse/rjd3bench/actions/workflows/pkgdown.yaml)
<!-- badges: end -->

Temporal disaggregation and benchmarking with JDemetra+ v3.x algorithms.

Benchmarking:

- Denton
- Cholette (incl. multi-variate)
- Cubic Splines
- GRP (Growth Rate Preservation)
- Calendarization

Temporal disaggregation

- Chow-Lin
- Fernandez
- Litterman
- Model Based Denton
- ADL (Autoregressive Distributed Lag Models)

## Installation

Running rjd3 packages requires **Java 17 or higher**. How to set up such
a configuration in R is explained
[here](https://jdemetra-new-documentation.netlify.app/#Rconfig)

### Latest release

To get the current stable version (from the latest release):

- From GitHub:

``` r
# install.packages("remotes")
remotes::install_github("rjdverse/rjd3bench@*release")
```

- From [r-universe](https://rjdverse.r-universe.dev/rjd3bench):

``` r
install.packages("rjd3bench", repos = c("https://rjdverse.r-universe.dev", "https://cloud.r-project.org"))
```

### Development version

To get the current development version from GitHub:

``` r
# install.packages("remotes")
remotes::install_github("rjdverse/rjd3bench")
```

## Usage

First, you have to load the **{rjd3bench}** package:

``` r
library("rjd3bench")
```

### Multivariate Cholette

``` r
s1 <- ts(c(7, 7.2, 8.1, 7.5, 8.5, 7.8, 8.1, 8.4), frequency = 4, start = c(2010, 1))
s2 <- ts(c(18, 19.5, 19.0, 19.7, 18.5, 19.0, 20.3, 20.0), frequency = 4, start = c(2010, 1))
s3 <- ts(c(1.5, 1.8, 2, 2.5, 2.0, 1.5, 1.7, 2.0), frequency = 4, start = c(2010, 1))

a <- ts(c(27.1, 29.8, 29.9, 31.2, 29.3, 27.9, 30.9, 31.8), frequency = 4, start = c(2010, 1))

y1 <- ts(c(30.0, 30.6), frequency = 1, start = c(2010, 1))
y2 <- ts(c(80.0, 81.2), frequency = 1, start = c(2010, 1)) 
y3 <- ts(c(8.0, 8.1), frequency = 1, start = c(2010, 1))

data_list <- list(s1 = s1, s2 = s2, s3 = s3, a = a, y1 = y1, y2 = y2, y3 = y3)

cc <- c("a=s1+s2+s3") # contemporaneous constraints 
tc <- c("y1=sum(s1)", "y2=sum(s2)", "y3=sum(s3)") # temporal constraints

output1 <- multivariatecholette(xlist = data_list, tcvector = tc, ccvector = cc, rho = 1, lambda = .5) # = Denton
output2 <- multivariatecholette(xlist = data_list, tcvector = tc, ccvector = cc, rho = 0.729, lambda = .5) # = Cholette
output3 <- multivariatecholette(xlist = data_list, tcvector = NULL, ccvector = cc, rho = 1, lambda = .5)
```

## Package Maintenance and contributing

Any contribution is welcome and should be done through pull requests
and/or issues. pull requests should include **updated tests** and
**updated documentation**. If functionality is changed, docstrings
should be added or updated.

## Licensing

The code of this project is licensed under the [European Union Public
Licence
(EUPL)](https://joinup.ec.europa.eu/collection/eupl/eupl-text-eupl-12).
