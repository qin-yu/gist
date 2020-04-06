# Configure Emacs on Ubuntu 18.04.04

- [Configure Emacs on Ubuntu 18.04.04](#configure-emacs-on-ubuntu-180404)
  - [Configure Emacs for LaTeX](#configure-emacs-for-latex)

## Configure Emacs for LaTeX

1. Check if emacs installed:
    ```bash
    $ emacs --version
    ```
    - if not installed:
        ``` bash
        Command 'emacs' not found, but can be installed with:

        sudo snap install emacs          # version 26.3, or
        sudo apt  install emacs25
        sudo apt  install emacs25-nox
        sudo apt  install e3
        sudo apt  install emacs25-lucid
        sudo apt  install jove
        ```
    - otherwise, eg:
        ```bash
        GNU Emacs 26.3
        Copyright (C) 2019 Free Software Foundation, Inc.
        GNU Emacs comes with ABSOLUTELY NO WARRANTY.
        You may redistribute copies of GNU Emacs
        under the terms of the GNU General Public License.
        For more information about these matters, see the file named COPYING.
        ```

2. Install emacs using snap:
    ```bash
    snap install emacs --classic
    ```
    `classic` because it was published using "classic" confinement and may perform arbitrary system changes outside of the security sandbox.

3. Install `auctex` package in emacs:
   1. launch emacs:
        ```bash
        $ emacs
        ```
   2. open package manager, which is ELPA by default:
        ```
        M-x list-packages
        ```
   3. move cursor to package using <kbd>ctrl</kbd> + <kbd>n</kbd> or <kbd>strl</kbd> + <kbd>p</kbd>, then select the `auctex` package by pressing <kbd>i</kbd> and install the selected packages by pressing <kbd>x</kbd>.
   4. quit with <kbd>q</kbd>.
