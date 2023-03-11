# Python

## Why use different Python versions and virtual environments?

As the Python language develops, new features become available to developers, e.g., typing support. Projects that harness these new features will require a minimum Python version. Thus, being able to run multiple Python versions on each machine is essential for our development team.

Similarly, each project will have its own list of package dependencies, i.e., the Python modules imported within a script. In some cases, these dependencies may conflict between project source code. For example, one project may use a `numpy` feature from v1.0.0 that has since been deprecated, while another project may use a `numpy` feature introduced in v2.1.1. If you use the same Python environment for both projects, you will encounter a dependency conflict that breaks one of the programs.

In addition, Linux and macOS both have a preinstalled "system" Python version used for internal tasks. Modifying any of the system packages may have unintended consequences on operating system behavior.

## macOS (ARM)

### Prerequisites

- [Homebrew](https://brew.sh)

Homebrew is a general software package manager for macOS. It handles the organization, maintenance, and updating of third-party software for developers, such as `pyenv`, a tool for managing local Python distributions and virtual environments.

Install Homebrew:

```zsh
curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh | bash
```

Confirm installation:

```zsh
source ~/.zprofile
brew --version
```

### Pyenv

Install `pyenv` with `brew`:

```zsh
brew install pyenv
brew install pyenv-virtualenv
```

Confirm installation:

```zsh
source ~/.zprofile
pyenv --version
```

Print a list of available Python installations:

```zsh
pyenv install --list
```

Restrict the output to a specific major Python version:

```zsh
pyenv install --list | grep " 3.10" # Only show Python 3.10.x
```

Install a Python version:

```zsh
pyenv install 3.10.2
```

Set the global Python version:

```zsh
pyenv global 3.10.2
```

The global version will become the default Python for your shell.

Confirm that `python` and `pip` point to the correct executables:

```zsh
which python
/Users/user/.pyenv/shims/python
which pip
/Users/user/.pyenv/shims/pip
```

If `.pyenv` is not part of the returned paths, you may have to modify your system environment profile (different from your Python environment!).

Add the following lines to `~/.zprofile`:

```zsh
export PATH="$HOME/.pyenv/bin:$PATH"
export PATH="$HOME/.pyenv/shims:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

Then refresh your environment and check the `python` and `pip` executables:

```zsh
source ~/.zprofile
which python
which pip
```

### Virtual environments

In addition to providing management tools for Python installations, `pyenv` also provides a command line tool for creating virtual environments:

Create a new virtual environment for a project, specifying the Python version and environment name:

```zsh
pyenv virtualenv 3.10.5 project-env
```

Activate the environment:

```zsh
pyenv shell project-env
```

Alternatively, set the environment as default for the project directory:

```zsh
pyenv local project-env
```

Now, every time you navigate inside your project folder, your system will automatically point to the desired Python executable!

## Windows

### Prerequisites

- [Chocolatey](https://chocolatey.org)

Similar to Homebrew for macOS, Chocolatey is a community-driven general package manager for Windows.

Install Chocolatey:

```ps1
Set-ExecutionPolicy Bypass -Scope Process -Force
[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072
Invoke-Expression ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

Confirm installation:

```ps1
refreshenv
choco --version
```

### Pyenv

Install `pyenv`:

```ps1
choco install pyenv-win
```

Confirm installation

```ps1
refreshenv
pyenv --version
```

If you receive an error, it may be because the PowerShell security policy prevents the execution of third-party scripts without administrator approval.

Check the execution policy:

```ps1
Get-ExecutionPolicy
```

If the return value is `Restricted`, change the permissions to `RemoteSigned`:

```ps1
Set-ExecutionPolicy RemoteSigned
```

Once again, confirm `pyenv` installation:

```ps1
refreshenv
pyenv --version
```

Print a list of available Python installations:

```ps1
pyenv install --list
```

Restrict the output to a specific major Python version:

```ps1
pyenv install -Filter "* 3.10*" # Only show Python 3.10.x
```

Install a Python version:

```ps1
pyenv install 3.10.5
```

Set the global Python version:

```ps1
pyenv global 3.10.5
```

The global version will become the default Python for your shell.

Confirm that `python` and `pip` point to the correct executables:

```ps1
Get-Command python | Format-Table Source
C:\Users\user\.pyenv\shims\python
Get-Command pip | Format-Table Source
C:\Users\user\.pyenv\shims\pip
```

If `.pyenv` is not part of the returned paths, you may have to modify your system environment variables. Specifically, change the order of the Windows `$Path` variable so that the `pyenv` binaries are listed at top.

### Virtual environments

Unfortunately, `pyenv-win` does not include the command line tool for managing virtual environments. Windows users need to follow the traditional approach with the built-in Python `venv` module.

Create a new virtual environment for a project, specifying the Python version and environment name:

```ps1
python -m venv C:\path\to\env
```

Activate the environment:

```ps1
C:\path\to\env\Scripts\Activate.ps1
```

Deactivate the environment:

```ps1
deactivate
```
