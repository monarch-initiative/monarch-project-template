# Monarch Project Template
A [Cookiecutter](https://cookiecutter.readthedocs.io/en/stable/) template for projects using [`Sphinx`](https://www.sphinx-doc.org/en/master/) + [`tox`](https://tox.wiki/en/latest/index.html) + [`poetry`](https://python-poetry.org/docs/). This template was developed thanks to the [tutorials by the cookiecutter project](https://cookiecutter.readthedocs.io/en/stable/tutorials/index.html) along with the instructions provided in [HelloCookieCutter1](https://github.com/BruceEckel/HelloCookieCutter1/blob/master/Readme.rst) by Bruce Eckel. The `tox` configuration is partly accreditted to Charles Tapley Hoyt's [cookiecutter implementation](https://github.com/cthoyt/cookiecutter-snekpack/blob/main/%7B%7Bcookiecutter.package_name%7D%7D/tox.ini).

# Getting started

First, install the [cruft](https://github.com/cruft/cruft) package. Cruft enables keeping projects up-to-date with future updates made to this original template.

```
pip install cruft
```

Next, create a project using the `monarch-project-template`.
```
cruft create https://github.com/monarch-initiative/monarch-project-template
```

This kickstarts an interactive session where you declare the following:
 - `project_name`: Name of the project. [defaults to: Project_X]
 - `project_description`: Description of the project. [defaults to: This is the project description.].
 - `file_name`: The name of the main python file. [defaults to: `main` for `main.py`]
 - `greeting_recipient`: Just a string that will be displayed when the boilerplate code is invoked. [defaults to: `World` as in `Hello, World!`]
 - `full_name`: Your name [defaults to: Author 1]
 - `email`: your email [defaults to: author@org.org]
 - `license`: Choose one from [`MIT`, `BSD-3`, `GNU GPL v3.0`, `Apache Software License 2.0`] [defaults to: `MIT`]
 - ⚠️`github_token_variable_name_for_doc_deployment`: The github token **variable name** for document deployment using `Sphinx`. [defaults to: `GH_TOKEN`]
 - ⚠️`github_token_variable_name_for_pypi_deployment`: The github token **variable name** which aligns with your autogenerated PyPI token for making releases. [defaults to: `PYPI_TOKEN`]

> :warning: **Do NOT enter actual token here, this is just the variable name that holds the token value in the project repository's Secrets.**

This will generate the project folder abiding by the template configuration specified by `monarch-project-template` in the [`cookiecutter.json`](https://github.com/monarch-initiative/monarch-project-template/blob/main/cookiecutter.json) file. 

# What does this do?

The following files and directories are autogenerated in the project:

 - Github wokflows:
   - For code quality checks (`qc.yml`)
   - Documentation deployment (`deploy-docs.yml`)
   - PyPI deployment (`pypi-publish.yml`)
 - `docs` directory with `Sphinx` configuration files and an `index.rst`file.
 - `src` directory structure with the `project_name` directory within it.
   - Within the `project_name` directory, there are 2 python files:
     - `main_file.py`
     - `cli.py` for [`click`](https://click.palletsprojects.com) commands.
 - `tests` directory with a very basic test.
 - `poetry` compatible `pyproject.toml` file containing minimal package requirements.
 - `tox.ini` file containing configuration for:
   -  `coverage-clean`
   -  `lint`
   -  `codespell`
   -  `docstr-coverage`
   -  `pytest`
- `LICENSE` file based on the choice made during setup. 
- `README.md` file containing `project_description` value entered during setup.


# Further setup
## initialize a git repository
```bash
git init
```


## Install `poetry`
Install `poetry` if you haven't already.
```
pip install poetry
```
## Install dependencies
```
poetry install
```

## Add `poetry-dynamic-versioning` as a dev dependency.
```
poetry add --group dev poetry-dynamic-versioning
```

## Set-up `pre-commit`
`pre-commit` runs hooks on every commit to automatically point out issues in code such as missing semicolons, trailing whitespace, and debug statements. For more information click [here](https://pre-commit.com).

```
poetry run pre-commit install
```
which will result in the message: 
```
pre-commit installed at .git/hooks/pre-commit
``` 
This indicates that you have a successful `pre-commit` setup.

## Run `tox` to see if the setup works
```
poetry run tox
```

This should run all the bullets mentioned above under the `tox` configuration and ideally you should see the following at the end of the run:
```
  coverage-clean: OK (0.20=setup[0.05]+cmd[0.15] seconds)
  lint-fix: OK (0.40=setup[0.01]+cmd[0.30,0.09] seconds)
  codespell-write: OK (0.20=setup[0.02]+cmd[0.18] seconds)
  docstr-coverage: OK (0.29=setup[0.01]+cmd[0.28] seconds)
  py: OK (1.29=setup[0.01]+cmd[1.28] seconds)
  congratulations :) (2.55 seconds)
```

And as the last line says: `congratulations :)`!! Your project is ready to evolve!

# Final test to see everything is wired properly

On the command line, type the `project_name`. In this example, `ABCD`:
```
poetry run ABCD run
```
Should return `Hello, **greeting_recipient value chosen during setup**`

To run commands within the poetry environment either preface the command with `poetry run`, i.e. `poetry run /path-to/my-command --options` or open the poetry shell with `poetry shell`.

# Future updates to the project's boilerplate code

In order to be up-to-date with the template, first check if there is a mismatch between the project's boilerplate code and the template by running:
```
cruft check
```

This indicates if there is a difference between the current project's boilerplate code and the latest version of the project template. If the project is up-to-date with the template:
```
SUCCESS: Good work! Project's cruft is up to date and as clean as possible :).
```

Otherwise, it will indicate that the project's boilerplate code is not up-to-date by the following:
```
FAILURE: Project's cruft is out of date! Run `cruft update` to clean this mess up.
```

For viewing the difference, run `cruft diff`. This shows the difference between the project's boilerplate code and the template's latest version.

After running `cruft update`, the project's boilerplate code will be updated to the latest version of the template.

# Setting up PyPI release

For the first time, you'll need to just run the following commands:
```
poetry build
poetry publish -u YOUR_PYPI_USERNAME -p YOUR_PYPI_PASSWORD
```
This will release a 0.0.0 version of your project on PyPI.

# Push to GitHub

1. Go to [https://github.com/new] and follow the instructions, being sure to
   NOT add the README.md and .gitignore files (the cookiecutter template will take
   care of these for you)

2. Add the remote to your local git repository

   ```bash
   git remote add origin https://github.com/my-user-or-organization/ABCD.git
   git branch -M main
   git add .
   git commit -m "first commit"
   git push -u origin main
   ```

## Automating this via Github Release
Go to the [PyPI account settings](https://pypi.org/manage/account/#two-factor) and select "Add API token". Create an API token and choose its scope: this token could either upload all the projects maintained or owned, its scope can be limited to just one project (preferred).

Copy this token to your project's 'secrets' in the 'Settings' section of your github project.
```
Settings -> Secrets -> Actions -> New Repository Secret
```
Paste the copied token from PyPI into the new secret and call it `PYPI_TOKEN`.

Now on releasing via Github, the project will automatically be released to PyPI as well.
