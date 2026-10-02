# Robust Statistics -- Automated Anomaly Detection

## Objective
I compared summary statistics and two outlier detection methods on California Housing prices to see how extreme values change what each one reports.

## Methodology
- I loaded the California Housing data with 20,640 observations and 9 columns.
- I checked the distribution of house values in units of $100,000 and measured its skewness.
- I computed the mean, median, trimmed mean (10%), standard deviation, IQR and MAD on house prices.
- I compared the mean with the median to measure the gap and the scaled MAD with the standard deviation to measure spread.
- I calculated Tukey Fences by hand with Q1 - 1.5 * IQR and Q3 + 1.5 * IQR and flagged every price outside them.
- I drew the fences on a histogram and a boxplot.
- I fit an Isolation Forest with contamination 0.05 and random state 42 on the 8 features other than price.
- I counted the rows flagged by Tukey only, by the forest only, by both and by neither.
- I compared the average feature values of the forest-only rows with the average values of the full data.
- I built an interactive explorer with ipywidgets that has a column dropdown, a Tukey k slider and a contamination slider and shows the flag counts.

## Key Findings
- The mean house value was 2.07 and the median was 1.80 so the mean sat $27,000 above the median.
- The standard deviation was about 14% larger than the scaled MAD.
- The Tukey fences were -0.98 and 4.82 so nothing was flagged low and all 1,071 flags were above the upper fence.
- Of those 1,071 flags, 965 sat at the Census cap of $500,001.
- The Isolation Forest flagged 1,032 rows, which is 5% of the data.
- Only 165 rows were flagged by both methods.
- Tukey looks at price alone and the Isolation Forest looks at all 8 features together so they flag different rows.
- The forest-only rows have ordinary prices but unusual combinations of features that Tukey cannot see.
- The explorer showed 1,071 Tukey flags at k = 1.5, which matches my hand calculation.
