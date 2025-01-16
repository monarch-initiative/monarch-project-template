# {{cookiecutter.project_name}}

{{cookiecutter.project_description}}

# Further setup
After running using cruft to create the initial project there are some steps to follow in order to finish the setup for this new project and repository.

## Initialize a git repository
Enter the new directory created by cruft and initialize git.
```bash
git init
```

## Install `uv`
Install `uv` if you haven't already. The `uv` documentation suggests system-wide installation but I prefer to install each of my version and package managers separately within my reository. For system-wide installation, the `uv` project suggests using their stand-alone installer `curl` script.
```
curl -LsSf https://astral.sh/uv/install.sh | sh
```
There is also a PyPi package you can install with `pipx` or `pip`. You can also use your system package management or other utilities to install `uv` system-wide. Please see the (UV Getting Started Guide)[https://docs.astral.sh/uv/getting-started/installation/] for these installation options.

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

1. Go to [https://github.com/new] and follow the instructions, being sure
   NOT to add the README.md and .gitignore files (the cookiecutter template will take
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
Use "[Trusted Publishers](https://docs.pypi.org/trusted-publishers/)" by PyPI

## Creating documentation
The documentation desired should be placed in the `docs` directory (markdown or reStructured format files).

Let's say the user has 2 more .rst files to add:
 - intro.rst
 - installation.rst

These two files should be placed in the docs directory and the `index.rst` file should be updated to read the following

```rst
Welcome to {{project_name}}'s documentation!
=========================================================

.. toctree::
   :maxdepth: 2
   :caption: Contents:

   intro
   installation

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

```
This lets sphinx know to look for theses rst files and generate equivalent HTML files.

Documentation is automatically built and deployed via the github workflow `deploy-docs.yml`. 
When changes are added to the main branch, this workflow is triggered. For this to work, the user needs to 
set-up the github repository of the project to enable documentation from a specific branch. In the `Settings` tab 
of the repository, click the `Pages` section in the left bar. For the `Branch`, choose the `gh-pages` branch.

The full GitHub Pages documentation can be found [here](https://docs.github.com/en/pages/quickstart). 

# Acknowledgements

This [cookiecutter](https://cookiecutter.readthedocs.io/en/stable/README.html) project was developed from the [monarch-project-template-uv](https://github.com/amc-corey-cox/monarch-project-template-uv) template and will be kept up-to-date using [cruft](https://cruft.github.io/cruft/).
