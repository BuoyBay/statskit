---
title: "statskit typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["RegressionResult", "RunningStatistics", "Stats"]
dependencies: []
symbols: ["RegressionResult", "RunningStatistics", "Stats"]
related: ["api.md", "getting-started.md", "index.md"]
---

# statskit typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## RegressionResult

`Public Class RegressionResult`

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Slope` | `Double` | No | No | — | — |
| `Intercept` | `Double` | No | No | — | — |
| `RSquared` | `Double` | No | No | — | — |
| `Count` | `Integer` | No | No | — | — |

## Stats

`Public Class Stats`

### Sum

`Public Shared Function Sum(values As Array Of Double) As Double`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `values` | `Array Of Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Double` |

### Mean

`Public Shared Function Mean(values As Array Of Double) As Double`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `values` | `Array Of Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Double` |

### Minimum

`Public Shared Function Minimum(values As Array Of Double) As Double`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `values` | `Array Of Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Double` |

### Maximum

`Public Shared Function Maximum(values As Array Of Double) As Double`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `values` | `Array Of Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Double` |

### Quantile

`Public Shared Function Quantile(values As Array Of Double, probability As Double) As Double`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `values` | `Array Of Double` | `ByVal` | Required |
| `probability` | `Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Double` |

### Median

`Public Shared Function Median(values As Array Of Double) As Double`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `values` | `Array Of Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Double` |

### PopulationStandardDeviation

`Public Shared Function PopulationStandardDeviation(values As Array Of Double) As Double`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `values` | `Array Of Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Double` |

### PopulationVariance

`Public Shared Function PopulationVariance(values As Array Of Double) As Double`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `values` | `Array Of Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Double` |

### SampleStandardDeviation

`Public Shared Function SampleStandardDeviation(values As Array Of Double) As Double`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `values` | `Array Of Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Double` |

### SampleVariance

`Public Shared Function SampleVariance(values As Array Of Double) As Double`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `values` | `Array Of Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Double` |

### PopulationCovariance

`Public Shared Function PopulationCovariance(values As Array Of Double, other As Array Of Double) As Double`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `values` | `Array Of Double` | `ByVal` | Required |
| `other` | `Array Of Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Double` |

### SampleCovariance

`Public Shared Function SampleCovariance(values As Array Of Double, other As Array Of Double) As Double`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `values` | `Array Of Double` | `ByVal` | Required |
| `other` | `Array Of Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Double` |

### Correlation

`Public Shared Function Correlation(values As Array Of Double, other As Array Of Double) As Double`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `values` | `Array Of Double` | `ByVal` | Required |
| `other` | `Array Of Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Double` |

### WeightedMean

`Public Shared Function WeightedMean(values As Array Of Double, weights As Array Of Double) As Double`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `values` | `Array Of Double` | `ByVal` | Required |
| `weights` | `Array Of Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Double` |

### LinearRegression

`Public Shared Function LinearRegression(values As Array Of Double, other As Array Of Double) As RegressionResult`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `values` | `Array Of Double` | `ByVal` | Required |
| `other` | `Array Of Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `RegressionResult` |

## RunningStatistics

`Public Class RunningStatistics`

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Count` | `Integer` | Yes | No | — | — |
| `Mean` | `Double` | Yes | No | — | — |

### Add

`Public Sub Add(value As Double)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `value` | `Double` | `ByVal` | Required |

Returns: no value.

### Merge

`Public Sub Merge(other As RunningStatistics)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `other` | `RunningStatistics` | `ByVal` | Required |

Returns: no value.

### PopulationStandardDeviation

`Public Function PopulationStandardDeviation() As Double`

No parameters.

#### Returns

| Type |
| --- |
| `Double` |

### SampleStandardDeviation

`Public Function SampleStandardDeviation() As Double`

No parameters.

#### Returns

| Type |
| --- |
| `Double` |

### PopulationVariance

`Public Function PopulationVariance() As Double`

No parameters.

#### Returns

| Type |
| --- |
| `Double` |

### SampleVariance

`Public Function SampleVariance() As Double`

No parameters.

#### Returns

| Type |
| --- |
| `Double` |
