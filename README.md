# GitHub Actions CI Demo: Python Project Setup

This repository contains the materials for the GitHub Actions CI demo
from Lecture 2. The project demonstrates how to move from a local Python
setup to a fully automated Continuous Integration (CI) pipeline that
runs tests in the cloud on every code change.

------------------------------------------------------------------------

## Project Overview

The goal of this demo is to establish a workflow where GitHub
automatically:

-   Spins up a virtual environment\
-   Installs dependencies\
-   Executes unit tests

This process runs automatically whenever you push code or open a pull
request.

------------------------------------------------------------------------

## File Structure

. ├── app.py ├── tests/ │ └── test_app.py ├── conftest.py ├──
requirements.txt ├── .gitignore └── .github/ └── workflows/ └──
python-ci.yml

### File Descriptions

-   app.py\
    A minimal Python module with a simple add function.

-   tests/test_app.py\
    Unit tests designed for pytest.

-   conftest.py\
    Required configuration to add the project root to PYTHONPATH so
    pytest can locate your modules.

-   requirements.txt\
    Lists project dependencies (e.g., pytest==8.0.0).

-   .gitignore\
    Ensures that temporary files like **pycache**, .venv, and
    .pytest_cache are not tracked by Git.

-   .github/workflows/python-ci.yml\
    The YAML file defining the GitHub Actions automation.

------------------------------------------------------------------------

## Prerequisites

-   Python 3.10+
-   Git installed and configured
-   A GitHub account

------------------------------------------------------------------------

## Setup and Workflow Instructions

### 1. Local Environment Setup

Initialize your project and verify tests pass locally before automating:

git init python -m venv .venv source .venv/bin/activate \# Windows:
.venv`\Scripts`{=tex}`\activate`{=tex} pip install -r requirements.txt
pytest

Ensure all tests pass before proceeding.

------------------------------------------------------------------------

### 2. GitHub Integration

Create a repository on GitHub and push your local code to the main
branch:

git remote add origin
https://github.com/`<your-username>`{=html}/github-actions-demo.git git
branch -M main git push -u origin main

------------------------------------------------------------------------

### 3. CI Pipeline Configuration

The CI process is governed by:

.github/workflows/python-ci.yml

This workflow uses a GitHub-hosted runner (ubuntu-latest) to execute the
following steps:

1.  Check out code\
    Uses actions/checkout@v4 to clone the repository onto the runner.

2.  Set up Python\
    Uses actions/setup-python@v5 to install Python 3.10.

3.  Install dependencies\
    Runs pip install for all requirements.

4.  Run tests\
    Executes pytest.

    -   If any test fails, the workflow returns a non-zero exit code.\
    -   The build is marked as failed.

------------------------------------------------------------------------

## Observing Results

After pushing the workflow file:

1.  Navigate to the Actions tab in your GitHub repository.
2.  Click on individual workflow runs to see live logs for each step.

### Status Indicators

-   Green Checkmark\
    All tests passed; the code is stable.

-   Red X\
    A test or step failed; inspect logs to debug the issue.

------------------------------------------------------------------------

## Enhancements Included

### Branch Protection

The workflow is configured to trigger on both:

-   push
-   pull_request

events targeting the main branch.

------------------------------------------------------------------------

### Dependency Caching (Optional)

You can use actions/cache@v4 to speed up builds by reusing previously
downloaded packages across workflow runs.

This reduces installation time and improves CI efficiency.
