# Some Important Settings for Visual Studio Code

- [Some Important Settings for Visual Studio Code](#some-important-settings-for-visual-studio-code)
    - [Auto-format white-spaces and newlines on save in VS Code](#auto-format-white-spaces-and-newlines-on-save-in-vs-code)
    - [Word Wrap](#word-wrap)
    - [How to show line rulers in VS Code for your Fortran project?](#how-to-show-line-rulers-in-vs-code-for-your-fortran-project)

### Auto-format white-spaces and newlines on save in VS Code
```json
{
    "files.trimTrailingWhitespace": true,
    "files.trimFinalNewlines": true,
    "files.insertFinalNewline": true
}
```

### Word Wrap
{
    "editor.wordWrap": "on"
}
There are four options: `off`, `on`, `wordWrapColumn`, `bounded`.

### How to show line rulers in VS Code for your Fortran project?

In `./.vscode/settings.json`, where `.` is the project directory, add the following:
```json
{
    "editor.rulers": [0, 1, 5, 6, 79, 120]
}
```
