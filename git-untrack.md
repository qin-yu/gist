# Delete Files in Git History

- [Delete Files in Git History](#delete-files-in-git-history)
  - [How to detect and delete large file throughout history](#how-to-detect-and-delete-large-file-throughout-history)
  - [How to untrack files based on changed .gitignore](#how-to-untrack-files-based-on-changed-gitignore)

## How to detect and delete large file throughout history

1. Push and see what files are rejected:
    ```bash
    $ git push
    ```
2. Then it will show the path of the large file in a specific commit, delete the file throughout git history using this path:
    ```bash
    $ git filter-branch --force --index-filter \
        "git rm --cached --ignore-unmatch PATH-TO-LARGE-FILE" \
        --prune-empty --tag-name-filter cat -- --all
    ```
    However, note that if the file existed in another location at some point, that was not deleted, so push again to see the path if you fail to recall.

3. Repeat 1 and 2 until it was deleted completely, then
    ```bash
    $ git push --force
    ```

## How to untrack files based on changed .gitignore

1. recursively `-r` remove `rm` files from index `--cached`
```bash
git rm -r --cached .
```

2. add `add` everything again
```bash
git add .
```
