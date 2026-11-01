---
title: "Getting started with StatsKit"
summary: "Install and run finite Double descriptive statistics."
category: "Guide"
order: 10
related: ["index.md", "api.md", "typed-api.md"]
---

# Getting started

Copy `packages/statskit-0.1.0.buipkg` into a fresh application's `packages/`
directory. Use `Import statskit`; the complete executable example is
`examples/statskit/main.bui`. It computes batch mean and sample variance, then
adds the same observations to a `RunningStatistics` instance.

Build in the standalone application's directory with `buoy main.bui -o app`,
then run `./app`. Expected output is mean 2.5, sample variance 1.66667 (the
console's default rounded display), and running mean 2.5. A package consumer
requires no other package or native dependency. Review the API contracts before
choosing population versus sample estimators or interpreting regression results.


Save the following as `main.bui` in your consumer project. Package archives and any dependencies must be installed as described above.

```buoy
Import statskit
Sub Main()
    Dim values() As Double = [1.0, 2.0, 3.0, 4.0]
    Print("Mean: " + Str(Stats.Mean(values)))
    Print("Sample variance: " + Str(Stats.SampleVariance(values)))
    Dim running As New RunningStatistics
    For Each value As Double In values
        running.Add(value)
    Next
    Print("Running mean: " + Str(running.Mean))
End Sub
```
