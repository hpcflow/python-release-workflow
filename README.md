# python-release-workflow

A template repository containing some GitHub Actions workflows for automating releases of Python packages. In particular we:

- Automate the version bump increment by using conventional commits
- Automate generation of a CHANGELOG
- Automate generation of Pyinstaller executables on multiple platforms
- Automate releasing the package to PyPI
- Automate the GitHub release
- Automate building Sphinx documentation and adding the built HTML as a new documentation version to a GitHub pages site

## Branching strategy

In this workflow, we assume two special branches, from which releases/deployments are made: `main` and `develop`:

- Merge pull-request into `develop` ==> make pre-release
- Merge pull-request into `main` from `develop` ==> make stable release

To avoid mistakes, we should "protect" these branches on GitHub, meaning all incoming code must be integrated via a pull request (i.e. no direct commits are allowed). However, we do need to allow a "bot" account to circumvent branch protection for the purposes of committing:
  - the version bump, updated CHANGELOG, and new tag
  - pre-commit fixes
  - documentation related commits

all of which need to occur during the GitHub actions workflows.

## Required software

- Poetry: for managing package dependencies
- commitizen: for determining the correct version bump increment (major, minor, or patch) according to the commit messages
- git-chglog: for generating a changelog between two tags
- PyInstaller: for generating single-file executables from a Python package
- Sphinx: for building documentation

## Skipping the release workflow

We can prevent release workflow running on pull-request merge by adding `[skip release]` to the PR title.


## How to merge this repository's workflow files with another repository

In the target repository:

- Add this repo as a remote: `git remote add python-release-workflow https://github.com/hpcflow/python-release-workflow.git`
- Effectively set the remote as fetch-only to avoid accidentally pushing to it: `git remote set-url --push python-release-workflow no-pushing`
- Checkout this repo as a new branch in your repo: `git checkout -b python-release-workflow/main python-release-workflow/main`
- Checkout the branch you want to synchronise: `git checkout aplowman/develop`
- Checkout only the `.github` directory from this repository: `git checkout python-release-workflow/main -- .github/`
- Stage, commit, and push the changes as normal: `git add .github/; git commit -m "build: update GH Actions workflows"; git push`

Note: once the remote is set up and you wish to synchronise again, we can fetch changes like this: `git fetch python-release-workflow main:python-release-workflow/main` (which takes the syntax: `git fetch <remote-name> <src-branch>:<dst-branch>`)
