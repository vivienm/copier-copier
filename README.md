# Copier project template

A [Copier](https://copier.readthedocs.io/en/stable/) template for Copier templates!

## Quickstart

To install Copier, please follow the instructions [here](https://copier.readthedocs.io/en/stable/#installation).

Then, to create a new project based on this template, run:

```bash
copier copy 'https://github.com/vivienm/copier-copier' path/to/your/project
```

and fill in the form.

To update an existing project based on this template, run:

```bash
copier update --skip-answered
```

## Project layout

This template uses itself, so it's a bit messy. Here is a quick overview:

* The nested directory `template/template` contains common template files for all final projects, regardless of the language.
  As such, it is relatively empty.
* The top-level directory `template` contains common template files for Copier template projects.
  It is based on the templates in the `template/template` directory.
* Finally, the root directory `.` (i.e., this project itself) is based on the templates in the `template` directory.

Consequently, all Jinja-like filenames in the `template/template` directory should be quoted with `{{ '{{' }} ... {{ '}}' }}` to prevent Copier from rendering them prematurely when processing the `template` directory.

To update the project:

```bash
# First, make some changes in the nested common template directory.
vim template/template/some_file
git diff
git commit -am "chore: update some file"
git push

# Then, propagate the change to the top-level copier template directory.
# Inspect the changes and commit them.
copier update --skip-answered
git diff
git commit -am "chore: propagate $(git rev-parse --short HEAD) to copier template"
git push

# Finally, propagate the change to the project itself. Inspect the changes
# and commit them.
copier update --skip-answered
git diff
git commit -am "chore: propagate $(git rev-parse --short HEAD) to project"
git push
```
