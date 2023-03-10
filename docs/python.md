# Python

## Why use different Python versions and virtual environments?

As the Python language develops, new features become available to developers. Projects that harness these new features, e.g., type support, will require a minimum Python version. Being able to install specific Python versions will provide the flexibility to easily switch between projects.

Similarly, each project will have its own list of package dependencies, i.e., the Python modules imported within a script. In some cases, these dependencies may conflict between project source code. For example, one project may use a `numpy` feature from v1.0.0 that has since been deprecated, while another project may use a `numpy` feature introduced in v2.1.1. If you use the same Python environment for both projects, you will have a dependency conflict that prevents code execution.

In addition, Linux and macOS both come preinstalled with a "system" Python version used for internal tasks. Updating any of the system packages may have unintended consequences on operating system behavior.

## macOS (ARM)

### Prerequisites

- [Homebrew](https://brew.sh)

To install Homebrew:

```zsh
curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh | bash
```

Confirm installation:

```zsh
source ~/.zprofile
brew --version
```

### Pyenv

```zsh
brew install pyenv
brew install pyenv-virtualenv
```

Confirm installation:

```zsh
source ~/.zprofile
pyenv --version
```

To see a list of available Python installations:

```zsh
pyenv install --list
```

To limit the list:

```zsh
pyenv install --list | grep " 3.10" # Only show Python 3.10.x
```

Install a specific Python version:

```zsh
pyenv install 3.10.2
```

Set the global Python version:

```zsh
pyenv global 3.10.2
```

Confirm that `python` and `pip` point to the correct executables:

```zsh
which python
/Users/user/.pyenv/shims/python
which pip
/Users/user/.pyenv/shims/pip
```

If `.pyenv` is not part of the returned paths, you may have to modify your system environment profile (different from your Python environment!).

## Windows

### Prerequisites

- [Chocolatey](https://chocolatey.org)

Chocolatey is a community-driven general package manager for Windows.

```ps1
Set-ExecutionPolicy Bypass -Scope Process -Force
[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072
iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

```ps1
refreshenv
choco --version
```
