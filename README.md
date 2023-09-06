## Introduction

This repo provides a CLI tool, `scaffold`, for quickly initializing a Python project in the "src layout".
That is, the Python project scaffolded this way is supposed to be built
into a distribution package. The source code will all be in the `src` folder.
Each subfolder of `src` is a separate "import package" within the distribution package.

After scaffolding, the project folder has the following structure.

```
./
|----src/
|     |----example_package
|           |----__init__.py
|           |----py.typed
|----tests/
|----.gitignore
|----.flake8
|----mypy.ini
|----pyproject.toml
```

- `src` contains all import packages of the distribution package. Each import package
  should be a valid Python identifier. Change `example_package` to the appropriate name.

- `tests` is for unit tests.

- `.flake8`, `mypy.ini` are configuration files with some starter settings.

- `pyproject.toml` is a [PEP-621](https://peps.python.org/pep-0621/) compliant project metadata file. In particular,
  it contains information needed by `setuptools` to build the distribution package.
  *There are some placeholders to replace in this file*.

- The `--setup-cfg` boolean option of the CLI will cause a template `setup.cfg` to be created as well, which is the
  "good old way" of configuring the build process using `setuptools`.

## Installation

This repo itself uses the same "src layout" that it initializes. It is built into a distribution
package --- the `dist/scaffold-1.2.0-py3-none-any.whl` wheel file. After installing the distribution package
in the _global environment_ of a Python
interpreter, the package places an executable `scaffold.exe` in the `Scripts` folder of the
global environment on Windows, or `scaffold` in the `bin` folder on Linux and macOS.
Create an alias to the executable and `scaffold` is available as a command from CLI.

- Download `dist/scaffold-1.2.0-py3-none-any.whl`.

- `pip install` from the wheel file into the global environment of a Python interpreter
  versioned 3.8 or above.

  On Windows, if using [Python Launcher](https://docs.python.org/3/using/windows.html), run:

  ```
  py -3.8 -m pip install scaffold-1.2.0-py3-none-any.whl
  ```

  On Linux and macOS, if NOT using [pyenv](https://github.com/pyenv/pyenv), run:

  ```
  python3 -m pip install scaffold-1.2.0-py3-none-any.whl
  ```

- Create an alias for the full path of `scaffold.exe` on Windows or `scaffold` on Linux and macOS.

  With PowerShell, put the following in the start-up script:

  ```
  Set-Alias -Name scaffold -Value C:\Users\{username}\AppData\Local\Programs\Python\Python38\Scripts\scaffold.exe
  ```

  With `bash` or `zsh`, put the following in `~/.bashrc` or `~/.zshrc`:

  ```
  alias scaffold="/Users/{username}/Library/Python/3.8/bin/scaffold"
  ```