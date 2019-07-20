
<!-- README.md is generated from README.Rmd. Please edit that file -->

# qif

<!-- badges: start -->

<!-- badges: end -->

## Quadratic Inference Function fit of balanced longitudinal data

Developed to perform the estimation and inference for regression
coefficient parameters in longitudinal marginal models using the method
of quadratic inference functions. Like generalized estimating equations,
this method is also a quasi-likelihood inference method. It has been
showed that the method gives consistent estimators of the regression
coefficients even if the correlation structure is misspecified, and it
is more efficient than GEE when the correlation structure is
misspecified. Based on Qu, A., Lindsay, B.G. and Li, B. (2000) DOI:
10.1093/biomet/87.4.823.

## Merits of QIF

Like generalized estimating equations (GEE), QIF is also a
quasilikelihood inference method. It has been showed that

1.  QIF gives consistent estimators of the regression coefficients even
    if the correlation structure is misspecified. GEE has the same
    property.

2.  QIF estimators are of the same efficiency as GEE estimators when the
    correlation structure is correctly specified, but more efficient
    when the correlation structure is misspecified.

3.  QIF gives a goodness-of-fit test for the validity of the first
    moment assumption pertaining to the unbiasedness of inference
    function. This assumption is crucial to ensure the consistency in
    estimation. GEE cannot provide this test.

4.  QIF is robust against a small portion of outliers/contaminated data;
    refer to Qu, A. and Song, P. (2004), “Assessing robustness of
    generalised estimating equations and quadratic inference functions”,
    Biometrika, 91, 447-459.

5.  QIF is analogous to -2\*log-likelihood, so it enables naturally to
    define some model selection criteria, such as Akaike Information
    Criterion (AIC) and Bayes Information Criterion (BIC).

## Installation

You can install the released version of qif from
[CRAN](https://CRAN.R-project.org) with:

``` r
install.packages("qif")
```

Or install the development version from
[Github](https://github.com/umich-biostatistics/qif)
with:

``` r
install.packages("devtools") # you need devtools to install packages from Github
devtools::install_github("umich-biostatistics/qif")
```

## Examples

``` r
## Marginal log-linear model for the epileptic seizures count data
## (Diggle et al., 2002, Analysis of Longitudinal Data, 2nd Ed., Oxford Press).

# Read in the epilepsy data set:
data(epil)

# Fit the QIF model:
fit <- qif(y ~ base + trt + lage + V4, id=subject, data=epil,
                                       family=poisson, corstr="AR-1")
 
# Alternately, use ginv() from package MASS
fit <- qif(y ~ base + trt + lage + V4, id=subject, data=epil,
                      family=poisson, corstr="AR-1", invfun = "ginv")


# Print summary of QIF fit:
summary(fit)


## Second example: MS study
data(exacerb)

qif_BIN_IND<-qif(exacerbation ~ treatment + time + duration + time2, id=id,
                        data=exacerb, family=binomial, corstr="independence")
                        
qif_BIN_AR1<-qif(exacerbation ~ treatment + time + duration + time2, id=id,
                        data=exacerb, family=binomial, corstr="AR-1")
                        
qif_BIN_CS<-qif(exacerbation ~ treatment + time + duration + time2, id=id,
                        data=exacerb, family=binomial, corstr="exchangeable")
                        
qif_BIN_UN<-qif(exacerbation ~ treatment + time + duration + time2, id=id,
                        data=exacerb, family=binomial, corstr="unstructured")

summary(qif_BIN_CS)

qif_BIN_CS$statistics

qif_BIN_CS$covariance
```
