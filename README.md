# Copier project template

A Copier template for Copier templates!

## Quickstart

To install Copier, please follow the installation instructions [here](https://copier.readthedocs.io/en/stable/#installation).

Then, to create a new project based on this template, run:

```shell
copier copy --trust 'https://github.com/vivienm/copier-copier' path/to/your/project
```

and fill in the form.

To update an existing project based on this template, run:

```shell
copier update --trust
```

## Project layout

This template uses itself, so it's a bit messy. Here is a quick recap:

* The nested directory `template/template` contains common template files for
all final projects, no matter the language. Hence, it is relatively empty.
* The toplevel directory `template` contains common template files for Copier
template projects. It is built upon the templates in the `template/template`
directory.
* Finally, the root directory `.` (i.e. this project itself) is built upon the
templates in the `template` directory.

As a consequence, all Jinja-like filenames in the `template/template` directory
should be quoted with `{{ '{{' }} ... {{ '}}' }}` to avoid being rendered one
step too far by Copier in the `template` directory.

To update the project:

```shell
# First, do some changes in the nested common template directory.
vim template/template/some_file
git diff
git commit -am "chore: update some file"
git push

# Then, propagate the change to the toplevel copier template directory.
# Inspect the changes and commit them.
copier update --trust
git diff
git commit -am "chore: propage $(git rev-parse --short HEAD) to copier template"
git push

# Finally, propagate the change to the project itself. Inspect the changes
# and commit them.
copier update --trust
git diff
git commit -am "chore: propage $(git rev-parse --short HEAD) to project"
git push
```
