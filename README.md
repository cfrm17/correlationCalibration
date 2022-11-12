# Correlation Calibration

The Kendall’s tau coefficient, τ, is used to measure the association between two measured quantities.  Given n observations, there are n*(n-1)/2 possible comparisons.  Any pair of observations between 2 quantities (xi, yi) and (xj, yj) are said to be concordant if the ranks for both elements agree and they are said to be discordant if the ranks for both elements do not agree.  If xi = xj or yi = yj then the pair is neither concordant, nor discordant.  When we use Kendall’s tau, we are actually using Kendall’s tau-b, τB, which accounts for ties.  

The sample Kendall’s tau-b is computed as the excess of concordant pairs over discordant pairs divided by a term representing the geometric mean between the number of pairs not tied on x and the number not tied on y,

 

where nC is the number of concordant pairs, nD is the number of discordant pairs, nX is the number of ties involving X, and nY is the number of ties involving Y.  Values for Kendall’s tau-b range from -1 (perfect inversion) to +1 (perfect agreement).

The sample Kendall’s tau, τ-hat, is an unbiased estimate of τ. The approximate distribution of   is asymptotically normal.  This correlation will reduce the effect of outliers on the effective correlation and, in the case of data from a bivariate elliptical distribution, can reproduce the standard Pearson’s correlation coefficient exactly by,

 .

ρτ , calculated from the equation above, is referred to as the Kendall’s tau transform estimate (or Kendall’s tau-b transform estimate in the case where τ is the Kendall’s tau-b correlation).  The sample Kendall’s tau transform estimate,  , is not an unbiased estimator of the linear correlation coefficient ρ.  However, it possesses sufficient accuracy.  Accuracy of the linear correlation estimate ( ) calculated via Kendall’s tau for the normal population case is given by,

 

Confidence intervals around   are constructed as,

 

where Φ(x) is the standard normal cumulative distribution function and α is the level of significance.  The above formulae are also used in the case of Kendall’s tau-b correlations.

The Kendall’s tau-b correlation matrix is calculated by looping through the pairwise quantities of the input dataset.  For each pair of quantities, the data is filtered for NaNs (reallocating memory on each loop depending on how many NaNs exist between the two quantities).

The Kendall’s tau-b transform estimate global correlation matrix is calculated for the set of non-proxy risk factors.  Proxied risk factors are included as placeholders in the global correlation matrix only.  The time to calculate the global correlation matrix can be reduced by sub-dividing the correlation matrix (ie: by grouping) and computing in parallel.

Depending on the quality of the dataseries, some Kendall’s tau-b transform estimate correlations between pairs of quantities are NaN. This is later replaced with 0 (see https://finpricing.com/lib/FiZeroBond.html ).

Using the Kendall tau-b transform estimate of this section, the global correlation matrix is computed.  This is the correlation matrix of all risk factors.  The matrix is almost certainly not PSD at this point.  Rows and columns corresponding to proxy risk factors are filled with zeros (see figure below).

 

Figure 1:  Global correlation matrix depicting the handling of proxy risk factors
