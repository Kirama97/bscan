# bscan

Many network and service enumeration tasks require several scanning utilities and a way to organize their output. `bscan` runs configured scans against authorized targets, collects the results, and presents matches in the console.

## Features

- Run configured port and service scans for one or more targets.
- Launch scan subprocesses asynchronously with a configurable concurrency limit.
- Parse discovered ports and service names from scan output.
- Run service-specific scans after services are identified.
- Highlight configured regular-expression matches in console output.
- Write scan results to a structured output directory.

## Installation

`bscan` targets Python 3.6 or newer. Install it from PyPI with `pip`:

```sh
python3 -m pip install bscan
```

The scan definitions can call external programs such as Nmap or Unicornscan. Install the programs required by your configuration before running a scan. Kali Linux includes many of the tools commonly used with `bscan`, but the package can run on other systems with compatible dependencies.

For a development checkout, install directly from the repository:

```sh
python3 -m pip install https://github.com/welchbj/bscan/archive/master.tar.gz
```

## Usage

Run `bscan` only against systems and networks for which you have explicit permission:

```sh
bscan \
  --max-concurrency 3 \
  --patterns '[Mm]icrosoft' \
  --status-interval 10 \
  --verbose-status \
  scanme.nmap.org
```

This command limits concurrent subprocesses to three, highlights matches for the supplied pattern, and prints status updates every ten seconds. `scanme.nmap.org` is the target passed to the configured scans.

Use `bscan --help` to view all available options, including output and configuration directory settings:

```sh
bscan --help
```

The configuration directory contains the files that define scan behavior:

- `patterns.txt` lists regular expressions to highlight in output.
- `required-programs.txt` lists external programs that should be installed.
- `port-scans.toml` defines port scans and the expressions used to parse their output.
- `service-scans.toml` defines scans for discovered services.

A custom configuration directory can be selected with `--config-dir`. Use `--output-dir` to choose where scan results are written. Existing output directories require `--hard` when they must be overwritten.

## License

`bscan` is released under the [MIT License](https://opensource.org/licenses/MIT).

This project is based on [welchbj/bscan](https://github.com/welchbj/bscan). The original project and its license terms are acknowledged here in accordance with the MIT license.
