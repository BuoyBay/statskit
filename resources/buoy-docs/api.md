---
title: "StatsKit contracts"
summary: "Finite Double descriptive statistics, regression, and streaming moments."
category: "Reference"
order: 20
symbols: ["Stats", "RunningStatistics", "RegressionResult"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# StatsKit contracts

Every observation, probability, and weight must be finite. Invalid arguments,
insufficient observations, unequal paired lengths, and unrepresentable computed
results throw `InvalidArgumentException`. No observation is silently dropped,
even when its weight is zero. All array operations leave their inputs unchanged.
Methods return Double unless stated otherwise.

| Stats shared method | Contract |
| --- | --- |
| `Sum(values)` | Compensated expansion sum; empty returns zero. |
| `Mean(values)` | Arithmetic mean; at least one observation. |
| `Minimum(values)`, `Maximum(values)` | At least one observation; validate the entire array. |
| `Median(values)` | `Quantile(values, 0.5)`. |
| `Quantile(values, probability)` | At least one observation; probability in [0,1]. Sorted-copy Hyndman–Fan type 7: position `(n-1)p`, linear interpolation between neighboring observations. Endpoints return extrema. |
| `PopulationVariance(values)` | Centered second moment divided by n; n >= 1. |
| `SampleVariance(values)` | Centered second moment divided by n-1; n >= 2. |
| `PopulationStandardDeviation(values)` | Square root of population variance, calculated without forming the variance first. |
| `SampleStandardDeviation(values)` | Square root of sample variance, calculated without forming the variance first. |
| `PopulationCovariance(values, other)` | Paired centered products divided by n; equal lengths, n >= 1. |
| `SampleCovariance(values, other)` | Paired centered products divided by n-1; equal lengths, n >= 2. |
| `Correlation(values, other)` | Pearson correlation; equal lengths, n >= 2; rejects zero variance in either array; clamps rounding excursions to [-1,1]. |
| `WeightedMean(values, weights)` | Equal lengths, n >= 1, nonnegative finite weights, at least one positive weight. Weights are relative; normalize by largest weight before totaling. |
| `LinearRegression(values, other)` | Ordinary least squares Y=`other` on X=`values`, with intercept; equal lengths, n >= 2; X must vary. Returns `RegressionResult`. |

`RegressionResult` exposes writable `Slope`, `Intercept`, `RSquared` (Double),
and `Count` (Integer) fields. `RSquared` is squared Pearson correlation for
varying Y. **Constant Y deliberately returns NaN for RSquared**, with zero slope
and its constant value as intercept. This output is the sole intentional
exception to the finite-results policy. Changing result fields does not affect
any accumulator or input.

`RunningStatistics` has an implicit empty constructor. Read-only `Count` is a
checked signed 64-bit Integer. Read-only `Mean`, and methods
`PopulationVariance()`, `PopulationStandardDeviation()` require Count >= 1;
`SampleVariance()`, `SampleStandardDeviation()` require Count >= 2. `Add(value)`
adds one finite observation. `Merge(other)` combines independent populations;
empty sources are no-ops, empty destinations adopt the source moments. Nil
sources reject. Self-merge duplicates the observations and count. Source state
is unchanged, except that self-merge necessarily changes that same object.
The accumulator retains constant-size state, never stores observations, and
stages the entire next state before mutation. Invalid input and count overflow
leave it unchanged. The class is not synchronized for concurrent access.

## Numerical algorithms and limits

Sum retains rounding residuals in an expansion. It is compensated, not a promise
of correctly rounded `math.fsum` parity for every input. An intermediate
expansion overflow rejects even if later cancellation could make the final sum
representable (for example `[1e308, 1e308, -1e308]`). Mean uses an anchor for tight
clusters, otherwise an expansion sum divided by count, falling back to divided
terms if unscaled summation overflows. Thus `[1e308,1e308]` has a finite mean,
and `[1,1e100,1,-1e100]` sums to 2. Divided terms can underflow in the fallback.

Batch moments first subtract an anchor to retain small differences around large
offsets, normalize by the largest difference, center again, and sum products
with compensation. If anchor subtraction overflows, they instead subtract
normalized observations. Standard deviation scales after taking the normalized
square root; variance squares this result, so standard deviation may succeed
when variance is unrepresentable. Interpolation uses bounded convex blending.
The streaming accumulator combines means and scaled population standard
deviations using parallel moment formulas without squaring unscaled spreads.

All arithmetic remains IEEE Double: input rounding is irreversible, very small
relative differences or weights can underflow, large counts lose integer
precision when converted to Double (above 2^53), and ill-conditioned covariance,
regression and intercept calculations can lose relative accuracy. Covariance
and regression scaling products/ratios may underflow or overflow for extreme
scale imbalance even when a differently ordered computation could succeed.
An intercept subtracting two large terms can lose nearly all its digits.
Streaming updates and merges are order dependent; repeated rounded mean updates
can degrade small variances around large offsets. They do not preserve the
expansion-sum cancellation guarantee. Batch centered moments are preferable
when observations remain available. Tiny results can round to zero; no minimum
positive variance or residual is enforced. No arbitrary precision or formal
mathematical conformance claim is made.

## Validation scope


Maintainers run the private validation suite before release. See the repository README for public build instructions.

