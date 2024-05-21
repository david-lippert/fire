# jupyter-book-example

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

This repository demonstrates a working implementation of [Jupyter Book](https://jupyterbook.org/), hosted on GitHub Pages, with automated deployments setup via GitHub Actions.

For more context about this process, or if you would like to start from scratch to setup your own book, consult the official [Jupyter Book Tutorial](https://jupyterbook.org/en/stable/start/your-first-book.html).

Otherwise, if you'd like to build on top of this template repository, follow the instructions below.

## Setup

[Make a copy](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template) of this template repository.

> NOTE: the GitHub Actions build for your new repository may be failing initially, until you configure GitHub Actions (see "Deploying" section below)

Clone your copy of the repository onto your local computer, and navigate there from the command line.

Setup a project-specific virtual environment, if you like that kind of thing (otherwise use an existing environment):

```sh
# using python 3.10 for example, but you can choose a different version if you'd like:
conda create -n jbook-env python=3.10
conda activate jbook-env
```

[Install the Jupyter Book Package](https://jupyterbook.org/en/stable/start/overview.html#install-jupyter-book), for example via pip:

```sh
# install just the jupyter book package into your environment:
#pip install jupyter-book

# consider alternatively leveraging the requirements file:
pip install -r requirements.txt
```

## Managing the Book

### Initializing

FYI - the following command was used to create the structure for this book (where "example-book" was chosen as the name of the book):

```sh
jupyter-book create example-book
```

If you have created a copy of this repository, you won't need to repeat this initialization step.

### Customizing

There are a number of opportunities to customize the book configuration via the ["_config.yml" file](/example-book/_config.yml) (for example, updating the logo). The sidebar navigation can be customized via the ["_toc.yml" file](/example-book/_toc.yml). See the [Jupyter Book Configuration Reference](https://jupyterbook.org/customize/config.html) for more details.

Also customize the content for your book, adding new markdown and notebook files to your book directory, as desired.

If you are including IPYNB notebooks in your book, and if these notebooks use any third-party Python packages, you must update the ["requirements.txt" file](/requirements.txt) to include the names of those packages.

### Building

> NOTE: the commands below assume your book is named "example-book", however if you choose a different book name, you'll need to update the commands accordingly

Build book as LaTeX (see "example-book/_build/latex"):

```sh
jupyter-book build example-book/ --builder latex
```

Build book as PDF (see "example-book/_build/latex/book.pdf"):

```sh
jupyter-book build example-book/ --builder pdflatex
```

Build book as HTML: (see "example-book/_build/html/index.html"):

```sh
jupyter-book build example-book/ --builder html
```

### Deploying

We want to [publish a GitHub Pages site using a GitHub Actions workflow](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow). See also the [Jupyter Book GitHub Pages Guide](https://jupyterbook.org/en/stable/publish/gh-pages.html).

The ["deploy-book.yml" workflow file](/.github/workflows/deploy-book.yml) controls the build process, and has been created for you already. If you use your own book name, customize "example-book" in this file to refer to the book name you chose (see lines 15, 48, and 54).

In your GitHub repository's settings, under the "pages" settings, configure GitHub Pages, specifically choosing to deploy from "GitHub Actions" source.

Commit and push to trigger an automated build of your HTML site. Visit the hosted site at your repository's GitHub Pages URL. You can find the hosted site URL from your GitHub Pages settings, once the site has been deployed! It should resemble the format `https://USERNAME.github.io/REPO_NAME`.
