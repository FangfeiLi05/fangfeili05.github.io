---
title: "Python Installation and Environment Setup"
date: 2025-12-10
description: "Add description"
summary: "Python"
tags: [""]
---

### 1. Method 1 -- VS Code + Homebrew + `uv`

Best for general Python, web development, and small projects. Lightweight, fast, and modern.

- **Step 1. Install VS Code**
  - [Info](https://code.visualstudio.com/docs/introvideos/basics)
  - [Download & Install](https://code.visualstudio.com/download)

- **Step 2. Install Homebrew**
  - [Install](https://brew.sh/)
  - Then add Homebrew to your PATH, by running in Terminal
    ```bash
    echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/<username>/.zprofile
    # Ensure Homebrew is available in new terminal sessions

    eval "$(/opt/homebrew/bin/brew shellenv)"
    # Apply Homebrew settings immediately without restarting the terminal

    ####################
    # brew --version
    ```

- **Step 3. Install Python**:
  - Run in Terminal
    ```bash
    brew install python@3.13
    # Installed as: /opt/homebrew/bin/python3

    brew cleanup python@3.13
    # Removes outdated files (does NOT uninstall Python)

    ####################
    # python3 --version

    # which -a python python3
    # List all Python/Python3 executables in PATH

    # which python python3
    # Show the default Python/Python3 in use
    ```

- **Step 4. Install `uv` (a fast Python package and environment manager)**:
  - [Info](https://github.com/astral-sh/uv)
  - Run in Terminal
    ```bash
    curl -LsSf https://astral.sh/uv/install.sh | sh
    ```

- **Step 5. Create a Python project environment**:
  - Run in Terminal
    ```bash
    uv init

    ####################
    # This automatically:
    #  - Create `pyproject.toml` if it does not already exist
    #  - Create or reuse a virtual environment (`.venv`) 
    #    - If `.venv/` exists, `uv` uses its Python interpreter
    #    - Otherwise, `uv` creates one using the default python3 on your PATH
    #      - To use a specific version, run `python3.13 -m venv .venv` before `uv init`
    #  - Optionally generate uv.lock
    #  - Detect existing dependencies

    # uv run python <name>.py
    # Run Python scripts
    ```

- **Step 6. Install packages**:
  - Run in Terminal
    ```bash
    uv add regex torch torchvision PyYAML matplotlib requests tqdm notebook
    # uv add numpy pandas
    ```


### 1. Method 2 -- Conda

Best for data science, machine learning, and scientific computing.
Heavier, but handles complex libraries well.

- **Step 1. Install Miniconda**
  - [Download and install](https://www.anaconda.com/docs/getting-started/miniconda/main)

- **Step 2. Create a Python project environment and install dependencies**:
  - Run in Terminal
    ```bash
    conda env create -f environment.yaml
  
    ####################
    # conda env list
    # conda env remove --n <envname>
    # conda clean --all # Free up disk space
    ```

    Here is an example of an [`environment.yaml`](/files/environment.yaml) file.

- **Step 3a. Install JupyterLab (with automatic kernel setup, recommended)**
  - Run in Terminal
    ```bash
    conda create -n jupyter_env python=3.14 jupyterlab nb_conda_kernels -c conda-forge

    # conda activate jupyter_env
    # jupyter lab

    # jupyter kernelspec list
    # jupyter kernelspec remove <kernelname>
    ```

    `nb_conda_kernels` allows Jupyter to automatically detect all Conda environments as usable kernels.

- **Step 3b. Install JupyterLab (with manual kernel setup)**
  - Run in Terminal
    ```bash
    conda create -n jupyter_env python=3.14 jupyterlab -c conda-forge

    conda activate <envname>
    conda install ipykernel -c anaconda
    ipython kernel install --user --name=<kernelname>
    conda deactivate
    ```