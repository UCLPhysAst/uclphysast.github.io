# IT Documentation for Users

## Introduction

This repository contains the source for [the user documentation page for computing and IT](https://uclphysast.github.io/) in the UCL Department of Physics and Astronomy. It uses [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) and draws heavily on the [similar site for ARC](https://www.rc.ucl.ac.uk/docs/) and the tutorial [Getting Started with Material for MkDocs](https://jameswillett.dev/getting-started-with-material-for-mkdocs/) by James Willett.

## Deployment

When someone pushes a commit to the `main` branch of the repository on GitHub, GitHub Actions follows the recipe in `.github/workflows/ci.yml` to call `mkdocs gh-deploy` and thus commit the compiled site to the `gh-pages` branch. GitHub Pages is configured (see Settings -> Pages) to deploy this branch to the site at https://uclphysast.github.io/.

## Contributing

We haven't defined a workflow yet while this is still at the development stage, but hopefully more information will appear here after some discussion.




