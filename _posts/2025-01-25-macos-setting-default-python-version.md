---
layout: post
title: macOS setting default python version
categories: [Python, macOS]
tags: [Python, Homebrew]
author: Dae-young Kim
comment: true
---
## 1. Python installation via Homebrew
Homebrew maintains its python version schema as `python@X.Y`.
For example, to install python 3.11, it would be `brew install python@3.11`

## 2. Update macOS python symbolic link
After the installation, it will tell you the installed location.
```bash
Unversioned and major-versioned symlinks `python`, `python3`, `python-config`, `python3-config`, `pip`, `pip3`, etc. pointing to
`python3.11`, `python3.11-config`, `pip3.11` etc., respectively, are installed into
/opt/homebrew/opt/python@3.11/libexec/bin # Here
```

Unlink existing symbolic link.
```bash
$ unlink /usr/local/bin/python
```

Create symbolic link again with desired python version.
```bash
$ sudo ln -s /opt/homebrew/opt/python@3.11/libexec/bin/python3 /usr/local/bin/python
```

Close and open the `Terminal` app and check if it works.
```bash
$ python --version
Python 3.11.11
```

## Reference
- [Status of Python versions](https://devguide.python.org/versions/)
- [Homebrew Python documentation](https://docs.brew.sh/Homebrew-and-Python#python-3)
- [Stack Overflow: How to set Python's default version to 3.x on OS X?](https://stackoverflow.com/a/38806058)