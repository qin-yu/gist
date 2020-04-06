# How to configure Git and setup GitHub on new machine

- [How to configure Git and setup GitHub on new machine](#how-to-configure-git-and-setup-github-on-new-machine)
  - [First-Time Git Setup](#first-time-git-setup)
    - [Three config files of different levels](#three-config-files-of-different-levels)
    - [Use terminal to set identity and editor](#use-terminal-to-set-identity-and-editor)
  - [Connect to GitHub with SSH](#connect-to-github-with-ssh)
- [Reference:](#reference)

## First-Time Git Setup

### Three config files of different levels
| Scope            | File                                     |
| ---------------- | ---------------------------------------- |
| system level     | `/etc/gitconfig`                         |
| user level       | `~/.gitconfig` or `~/.config/git/config` |
| repository level | `.git/config`                            |
Each level overrides values in the level above. You can all of your settings and where they are coming from using:
```bash
$ git config --list --show-origin
```
This should print nothing if `git` has not been used.

### Use terminal to set identity and editor
1. Set identity
    ```bash
    $ git config --global user.name "John Doe"
    $ git config --global user.email johndoe@example.com
    ```
    If you want to override this with a different name or email address for specific projects, you can run the command without the `--global` option when you’re in that project.

2. Set editor
    Now set `emacs` as the default editor:

    ```bash
    $ git config --global core.editor emacs
    ```
    If not configured, Git uses your system’s default editor.

3. Set colour
    Also, enable coloured output in terminals:
    ```bash
    $ git config --global color.ui true
    ```

## Connect to GitHub with SSH
1. Check keys to reuse
    ```bash
    ls -alhF ~/.ssh/
    ```
    if no files like `~/.ssh/id_rsa` and `~/.ssh/id_rsa.pub` found then

2. Generate key pair
    ```bash
    $ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
    ```

3. Add key to ssh-agent
    ```bash
    $ eval "$(ssh-agent -s)"
    $ ssh-add ~/.ssh/id_rsa
    ```

4. Paste public key to GitHub
    i.e. copy the content of `~/.ssh/id_rsa.pub` into GitHub -> Personal Settings -> SSH and GPG keys -> New SSH Key

5. Test
    ```bash
    $ ssh -T git@github.com
    ```


# Reference:
- [1.6 Getting Started - First-Time Git Setup](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)
- [Generating a new SSH key and adding it to the ssh-agent](https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
- [Testing your SSH connection](https://help.github.com/en/github/authenticating-to-github/testing-your-ssh-connection)
