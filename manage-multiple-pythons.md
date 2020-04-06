# How to Reinstall & Manage Multiple Pythons
Qin Yu, Apr 2020

- [How to Reinstall & Manage Multiple Pythons](#how-to-reinstall--manage-multiple-pythons)
- [How to Install & Manage Multiple Pythons (on Ubuntu 18.04)](#how-to-install--manage-multiple-pythons-on-ubuntu-1804)
  - [Install `pyenv`](#install-pyenv)
    - [Auto-installation (not as auto as it sounds)](#auto-installation-not-as-auto-as-it-sounds)
    - [Manual installation](#manual-installation)
    - [Some features of `pyenv`](#some-features-of-pyenv)
  - [Usage](#usage)
  - [Reference](#reference)
- [How to Reinstall & Manage Multiple Pythons (on macOS 10.14 Mojave)](#how-to-reinstall--manage-multiple-pythons-on-macos-1014-mojave)
  - [Remove All Current Python](#remove-all-current-python)
  - [Reinstall via `pyenv` & **Anaconda**](#reinstall-via-pyenv--anaconda)
  - [Reference](#reference-1)

# How to Install & Manage Multiple Pythons (on Ubuntu 18.04)
Qin Yu, Apr 2020

Here I present how to choose and install Python 3 on Ubuntu, and manage virtual environments and packages using.

## Install [`pyenv`](https://github.com/pyenv/pyenv-installer#installation--update--uninstallation)
**Important**: Please make sure eval "$(pyenv init -)" is placed toward the end of the shell configuration file since it manipulates PATH during the initialization.

### Auto-installation (not as auto as it sounds)
```bash
$ curl https://pyenv.run | bash
$ exec $SHELL
$ pyenv update
```
If cannot install, see [prerequisites for `pyenv`](https://github.com/pyenv/pyenv/wiki/Common-build-problems#prerequisites).

### Manual installation
This works best for our Ubuntu 12.04 workstations which default to a .bashrc configuration file in lieu of .bash_profile.
```bash
$ cd
$ git clone https://github.com/pyenv/pyenv.git ~/.pyenv
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
$ echo 'eval "$(pyenv init -)"' >> ~/.bashrc
$ source ~/.bashrc
```

### Some features of `pyenv`
- pyenv **does**:
  - Let you change the global Python version on a per-user basis.
  - Provide support for per-project Python versions.
  - Allow you to override the Python version with an environment variable.
  - Search commands from multiple versions of Python at a time. This may be helpful to test across Python versions with tox.

- In contrast with pythonbrew and pythonz, pyenv **does not**:
  - Depend on Python itself. pyenv was made from pure shell scripts. There is no bootstrap problem of Python.
  - Need to be loaded into your shell. Instead, pyenv's shim approach works by adding a directory to your `$PATH`.
  - Manage virtualenv. Of course, you can create virtualenv yourself, or pyenv-virtualenv to automate the process.

## [Usage](https://github.com/pyenv/pyenv/blob/master/COMMANDS.md)
1. `pyenv commands` lists all available pyenv commands.

2. Firstly, `pyenv global` reports the currently configured global version of Python. To list all the versions available through `pyenv` on your machine using `pyenv versions`. Note that `version` and `versions` are two commands.

   Usually you will only have one version of python installed, the system-wide version. That’s what’s shown in the above command. pyenv now allows you to expand upon this version. Let’s start by installing another python version.[[*](https://amaral.northwestern.edu/resources/guides/pyenv-tutorial)]

3. Install another Python with specified version:
    1. list all versions available:
        ```bash
        $ pyenv install --list
        ```
    2. install the version:
        ```bash
        $ pyenv install anaconda3-2019.10
        ```

3. `cd` to your working directory

4. Check current the currently configured local version:
    ```bash
    $ pyenv local
    ```
    There should be `pyenv: no local version configured for this directory`.

5. Sets a local application-specific Python version by writing the version name to a .python-version file in the current directory:
    ```bash
    $ pyenv local anaconda3-2019.10
    ```
    Now one should see the shell prompt with additional text `(anaconda3-2019.10)`.

Check or change the global version the same way.

## Reference
- [My Python Development Workflow with `pyenv` Martin David Valentino](https://medium.com/@martinlabs/my-python-development-workflow-with-pyenv-2bfbc03a15a1)
- [pyenv Tutorial](https://amaral.northwestern.edu/resources/guides/pyenv-tutorial)

# How to Reinstall & Manage Multiple Pythons (on macOS 10.14 Mojave)
Qin Yu, Jun 2019

It drove me crazy when various frameworks each requires a specific version of Python...

## Remove All Current Python
1. Firstly, get rid of the **official** ones:
    ```bash
    $ sudo rm -rf '/Applications/Python X.Y' #replace X.Y with the version number on the folder
    $ sudo rm -rf /Library/Frameworks/Python.framework
    $ sudo rm -rf /usr/local/bin/python
    $ sudo rm -rf /usr/local/bin/python3
    ```

2. Then I shall delete the **Homebrew** installed Python:
    ```bash
    $ brew list | grep 'python'
    $ brew uninstall -f python python@2  # this means Python2
    ```

3. Now I kill my least favourite **Anaconda** Installations:
    ```bash
    $ rm -rf ~/anaconda2
    $ rm -rf ~/anaconda3
    $ rm -rf ~/miniconda2
    $ rm -rf ~/miniconda3
    $ rm -rf ~/.condarc ~/.conda ~/.continuum
    ```

4. Uninstall Python from Pyenv:
    ```bash
    $ pyenv versions
    ```
    After obtaining all the python versions, do, e.g.:
    ```bash
    $ pyenv uninstall 3.5.0
    $ pyenv uninstall 3.6.0
    ```

## Reinstall via `pyenv` & **Anaconda**
Look, it took me hours to be aware of the integration of Anaconda into `pyenv`... Once `pyenv` is `brew`-ed into my macOS you can `pyenv install --list` and see all the Anaconda versions including `anaconda3-2019.03`, which fails because of the exeptionally slow access to the open internet from China.

Download the required files into `~/.pyenv/cache` makes things easier.

## Reference
- [Install, Uninstall, and Manage Multiple Versions of Python on a Mac](https://www.ianmaddaus.com/post/manage-multiple-versions-python-mac/#uninstall-python), Jul 2018
- [Mac 下实现 pyenv/virtualenv 与 Anaconda 的兼容](https://blog.csdn.net/vencent7/article/details/76849849), Aug 2017
