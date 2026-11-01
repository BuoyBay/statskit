# StatsKit standalone example

From the repository root, check, build, and run with the existing sealed package
in an isolated directory:

```sh
example_dir=$(mktemp -d)
mkdir "$example_dir/packages"
cp examples/statskit/main.bui "$example_dir/main.bui"
cp packages/statskit-0.1.0.buipkg "$example_dir/packages/"
(cd "$example_dir" && buoy main.bui --check --diagnostic-format json && buoy main.bui -o app && ./app)
```

Isolation avoids discovery of unrelated app resources in this checkout.
No dependency manifest is needed for a presealed archive. The included
`bpm.json` describes local source acquisition when developing in this repository.


Maintainers run the private validation suite before release. See the repository README for public build instructions.
