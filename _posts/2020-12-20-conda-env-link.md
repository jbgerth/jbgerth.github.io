---
layout: post
title: "Setting up relative Conda env with link to global naming"
description: "Being able to call relative env by name"
categories: [python]
tags: [programming, anaconda, conda, python, virtual environment]
lastmod: 2020-12-20
redirect_from:
  - /2020/09/05/
---

## The issue with Conda environments

In my day to day work I need to use a lot of different environments. Be it for different projects, check out pull requests from colleagues or do experiments on the code base. This usually would lead to me creating a Python environment for every new thing, I want to try out. The setup involves creating the environment directly inside of the project root directory, so that it is clear which one to use, if I come back later to it. Additionally, IDEs such as IntelliJ work really well with the relative environment. It also installs in CI environments or servers, where I would not be able to write in the anaconda directory.

Alas, the approach has two major downsides:

- Depending on how often I need to recreate the environment, this step takes up a lot of time.
- When using fsh or comparable shells, the path to the conda environment is written out completely, which makes it less fun to work with, compared to just showing the name  of the environment.
  
Therefore, I searched for a different solution.

## Linking to the anaconda directory

Instead of storing the environment directly inside of the anaconda directory, it is possible to create a soft link. With that the directory is kept relatively for CI pipelines, servers and the IDE, while it becomes accessible using the name of the link. Futhermore, the name is shown correctly in the shell, which makes it more usable inside of the terminal.

### Hot to link

I created the link with:

```sh
export PATH_TO_PROJECT="<path/to/project>"
export NAME_OF_ENV="<name/of/env>"
export ANACONDA_ENV_DIR="<dir/of/envs>"

ln -s $PATH_TO_PROJECT/.venv $ANACONDA_ENV_DIR/$NAME_OF_ENV 
```

This should make the conda environment activatable by calling `conda activate $NAME_OF_ENV` instead of using the whole path. Now instead of setting up a new environment, it is possible to just reuse an existing environment.

This comes with the caveat, that it can be only used, if the packages of the environment are not changed between projects or versions cof the same project.
