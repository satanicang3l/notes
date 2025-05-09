---
title: Python
parent: General Usage
layout: default
nav_order: 10
---

## Virtual environments

1. Version: `pyenv versions` to show which python version you have. `pyenv global 3.8.8` to switch to 3.8.8. Switch to the specific folder, and use `pyenv local 3.6.6` to use 3.6.6 specifically for that project folder.
2. For specific python projects, switch to that folder and use `pipenv install`. Use `pipenv install numpy` to install numpy for that project. Use `pipenv shell` to activate the environment. Inside the shell, `use pip install --user <packagename>` to install packages. To remove the environment use `pipenv --rm`.
3. Troubleshoot: If you type a package name wrongly in `pipenv install`, remove the wrong name in pip file directly. If pip cannot be found, use `python get-pip.py — force-reinstall` in pipenv shell.