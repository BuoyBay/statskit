# StatsKit

## Start with the standalone consumer

The [example](../examples/statskit/README.md) explains how to copy its existing
`main.bui` into an isolated application with the sealed package. It calculates
mean 2.5 and sample variance approximately 1.66667 for four observations, then
feeds the same values into `RunningStatistics`. no native library or GUI is required.

Choose batch `Stats` methods when observations remain available, especially for
small variances around large offsets. `RunningStatistics` retains constant-size
state for streaming input and can merge accumulators, but update/merge order
can affect rounding. It is mutable and not synchronized: serialize access to a
shared accumulator. Batch methods leave their input arrays unchanged.

## Input and numerical limits

Every observation, probability and weight must be finite; even zero-weight
observations are validated. Invalid inputs and unrepresentable computed results
throw `InvalidArgumentException`. Empty `Sum` returns zero; means and population
moments require at least one observation, sample moments at least two. Paired
methods require equal lengths. Correlation rejects zero variance, and regression
requires varying X. Weighted means require nonnegative weights with a positive
total. Quantiles use sorted-copy Hyndman–Fan type 7 interpolation.

Constant-Y regression intentionally returns NaN for `RSquared`, with zero slope
and the constant intercept. Double arithmetic can underflow or lose precision;
standard deviation may remain representable when variance overflows. See the
[full contracts and numerical limits](../resources/buoy-docs/api.md) before relying
on extreme-scale results. Failed streaming updates leave the accumulator state
unchanged. `Merge` leaves a distinct source unchanged; self-merge duplicates its
own observations and count.
