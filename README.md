# Pattern-recognition
The command-line interface (CLI) that provides a set of commands to interact with the server and recognize the pattern.

[![PyPI version shields.io](https://img.shields.io/pypi/v/pattern-recognition-cli.svg)](https://pypi.python.org/pypi/pattern-recognition-cli/)
[![PyPI license](https://img.shields.io/pypi/l/pattern-recognition-cli.svg)](https://pypi.python.org/pypi/pattern-recognition-cli/)
[![PyPI pyversions](https://img.shields.io/pypi/pyversions/pattern-recognition-cli.svg)](https://pypi.python.org/pypi/pattern-recognition-cli/)

  * [Getting started](#getting-started)
  * [Usage](#usage)
    * [Service](#service)
  * [Development](#development)
  * [Production](#production)

## Getting started

Blank.

## Usage

### Service

Get the version of the package — ``pattern-recognition --version``:

```bash
$ pattern-recognition --version
pattern-recognition, version 0.1.0
```

Get all possible package's commands — ``pattern-recognition --help``:

```bash
$ pattern-recognition --help
Usage: pattern-recognition [OPTIONS] COMMAND [ARGS]...
  Command line interface for PyPi version checking.
Options:
  --version  Show the version and exit.
  --help     Show this message and exit.
...
```

## Development

To run the tests, use the following command, being in the root of the project:

```bash
$ pytest tests/
```

To build the package to test of to be deployed, use the following commands:

```bash
$ pip3 uninstall -y pattern-recognition-cli && rm -rf dist/ pattern-recognition-cli.egg-info && \
      python3 setup.py sdist && pip3 install dist/*.tar.gz
```

## Production

To build the package and upload it to [PypI](https://pypi.org) to be accessible through [pip](https://github.com/pypa/pip),
use the following commands. [Twine](https://twine.readthedocs.io/en/latest/) requires the username and password of the
account package is going to be uploaded to.

```build
$ python3 setup.py sdist
$ twine upload dist/*
```