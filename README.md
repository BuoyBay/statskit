# Stats and regression

`statskit` implements Finite Double descriptive statistics, regression and streaming moments.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add statskit --git https://github.com/BuoyBay/statskit.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## Example

```basic
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

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer statskit
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
