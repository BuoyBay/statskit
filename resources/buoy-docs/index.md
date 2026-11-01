---
title: "StatsKit"
summary: "Stable finite Double descriptive and streaming statistics."
category: "Overview"
order: 0
keywords: ["statskit", "statistics", "regression", "variance"]
related: ["getting-started.md", "api.md", "typed-api.md"]
---

# StatsKit

Import `statskit` for compensated reductions, descriptive statistics, paired
moments, weighted means, ordinary least squares and a constant-space
`RunningStatistics` accumulator. This package is pure Buoy and standalone.

Copy `statskit-0.1.0.buipkg` into your application's `packages/` directory.
See [getting started](getting-started.md), [contracts and precision limits](api.md),
and [public signatures](typed-api.md). Inputs must be finite; empty statistics
reject except Sum. Existing ArrayUtils semantics are unaffected.
