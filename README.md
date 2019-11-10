# Pattern-recognition
The command-line interface (CLI) that provides a set of commands to interact with the server and recognize the pattern.

[![PyPI version shields.io](https://img.shields.io/pypi/v/pattern-recognition-cli.svg)](https://pypi.python.org/pypi/pattern-recognition-cli/)
[![PyPI license](https://img.shields.io/pypi/l/pattern-recognition-cli.svg)](https://pypi.python.org/pypi/pattern-recognition-cli/)
[![PyPI pyversions](https://img.shields.io/pypi/pyversions/pattern-recognition-cli.svg)](https://pypi.python.org/pypi/pattern-recognition-cli/)

  * [Getting started](#getting-started)
  * [Usage](#usage)
    * [Service](#service)
  * [Development](#development)
    * [Docker](#docker)
  * [Production](#production)

## Getting started

Blank.

## Usage

### Service

Get the version of the package — ``pattern_recognition --version``:

```bash
$ pattern_recognition --version
pattern_recognition, version 0.1.0
```

Get all possible package's commands — ``pattern_recognition --help``:

```bash
$ pattern_recognition --help
Usage: pattern_recognition [OPTIONS] COMMAND [ARGS]...
  Command line interface for PyPi version checking.
Options:
  --version  Show the version and exit.
  --help     Show this message and exit.
...
```

## Development

<h3 id="development-requirements">Requirements</h4>

- Docker — https://www.docker.com. Install it with the [following reference](https://docs.docker.com/install).

### Docker

Clone the project and move to project folder:

```bash
$ git clone https://github.com/Alladin9393/Pattern-recognition && cd Pattern-recognition
```

If you already worked with the project, you can clean it's container and images with the following command:

```bash
$ docker rm pattern-recognition -f || true && docker rmi pattern-recognition -f || true
```

Run the ``Docker container`` with the project source code in the background mode:

```bash
$ docker build -t pattern-recognition . -f Dockerfile.development
$ docker run -d --network host -v $PWD:/pattern-recognition --name pattern-recognition pattern-recognition
```

Enter the container bash:

```bash
$ docker exec -it pattern-recognition bash
```

And now being in the container, you can develop the project. For instance, run tests and linters:

```bash
$ coverage run -m pytest -vv tests
$ coverage report -m && coverage xml
$ flake8 cli && flake8 tests/
$ bash <(curl -s https://linters.io/isort-diff) cli tests
```

When you have developed new functionality, check it with the following command. This command creates the ``Python package``
from source code instead of installing it from the ``PyPi``.

```bash
$ pip3 uninstall -y pattern-recognition && rm -rf dist/ pattern_recognition_cli.egg-info && \
      python3 setup.py sdist && pip3 install dist/*.tar.gz
```

So after this command, you are free to execute the command line interface as if you installed in through ``pip3 install``:

```bash
$ pattern_recognition --version
```

With the commands above you could test your features as if user will use it on own.

```bash
$ docker rm $(docker ps -a -q) -f
$ docker rmi $(docker images -q) -f
```

## Production

To build the package and upload it to [PypI](https://pypi.org) to be accessible through [pip](https://github.com/pypa/pip),
use the following commands. [Twine](https://twine.readthedocs.io/en/latest/) requires the username and password of the
account package is going to be uploaded to.

```build
$ python3 setup.py sdist
$ twine upload dist/*
```