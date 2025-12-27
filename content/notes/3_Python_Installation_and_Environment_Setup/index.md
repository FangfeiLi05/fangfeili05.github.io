---
title: "Python Installation and Environment Setup"
date: 2025-12-10
description: "Add description"
summary: "Python"
tags: [""]
---

## 1. Method 1 -- VS Code + Homebrew + `uv`

Best for general Python, web development, and small projects. Lightweight, fast, and modern.

### 1.1. Installation

- [**VS Code**](https://code.visualstudio.com/docs/introvideos/basics): [Download & Install](https://code.visualstudio.com/download)

- **Homebrew**: [Install](https://brew.sh/)

  Then add Homebrew to your PATH:

  ```bash
  echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/<user-name>/.zprofile  
  eval "$(/opt/homebrew/bin/brew shellenv)"                                         
  ```

  - Ensure Homebrew is available in new terminal sessions
  - Apply Homebrew settings immediately without restarting the terminal

  Verify installation

  ```bash
  brew --version
  ```

- **Python**:

  ```bash
  brew install python@3.13
  brew cleanup python@3.13
  ```

  - Installed as: `/opt/homebrew/bin/python3`
  - Remove outdated files (does NOT uninstall Python)

  Verify installation

  ```bash
  python3 --version
  ```

- [**`uv`**](https://github.com/astral-sh/uv) (a fast Python package and environment manager):

  ```bash
  curl -LsSf https://astral.sh/uv/install.sh | sh
  ```

### 1.2. Environment Setup

- **Step 1.** Create a Python Project Environment:

  ```bash
  uv init
  ```

  This automatically:
  - Creates `pyproject.toml` if missing.
  - Creates or reuses a virtual environment (`.venv`).
    - If `.venv` exists, uses its Python interpreter.
    - Otherwise, creates one using the default `python3` from PATH.
  - Optionally generates `uv.lock`.
  - Detects existing dependencies.

- **Step 2.** Install dependencies:

  ```bash
  uv add regex torch torchvision PyYAML matplotlib requests tqdm notebook
  ```

---

## 2. Method 2 -- Conda

Best for data science, machine learning, and scientific computing. Heavier, but handles complex libraries well.

### 2.1. Installation

- **Miniconda**: [Download & Install](https://www.anaconda.com/docs/getting-started/miniconda/main)

### 2.2. Environment Setup

- **Step 1.** Create a Python project environment and install dependencies:
  
  ```bash
  conda env create -f environment.yaml
  ```

  Example `environment.yaml`: [View Example](/files/environment.yaml)

- **Step 2.** Create a Python Jupyter environment for running JupyterLab:

  ```bash
  conda create -n jupyter_env python=3.14 jupyterlab -c conda-forge
  ```

  For usage:

  ```bash
  conda activate jupyter_env
  jupyter lab
  conda deactivate
  ```

- **Step 3a (recommended; choose either 3a or 3b).** Enable automatic Jupyter kernel discovery:

  ```bash
  conda activate jupyter_env
  conda install nb_conda_kernels -c conda-forge
  conda deactivate
  ```
  
  `nb_conda_kernels` allows JupyterLab to automatically detect all Conda environments as usable kernels.

- **Step 3b (choose either 3a or 3b).** Configure a Jupyter kernel manually:

  ```bash
  conda activate <env-name>
  conda install ipykernel -c anaconda
  ipython kernel install --user --name=<kernel-name>
  conda deactivate
  ```

---

## 3. Extra Useful Commands

- List all Python / Python3 executables in `PATH`:

  ```bash
  which -a python python3
  ```

- Show the default Python / Python3 in use:

  ```bash
  which python python3
  ```

- List all Conda environments:

  ```bash
  conda env list
  ```

- Remove a Conda environment:

  ```bash
  conda env remove -n <env-name>           
  ```

- Free up disk space by removing unused packages and caches:

  ```bash
  conda clean --all
  ```

- Free up disk space by removing unused packages and caches:

  ```bash
  conda clean --all
  ```

- Run Python scripts (with `uv`):

  ```bash
  uv run python <script-name>.py
  ```

- List all available Jupyter kernels (in `jupyter_env`):

  ```bash
  jupyter kernelspec list                
  ```

- Remove a specific Jupyter kernel (in `jupyter_env`):

  ```bash
  jupyter kernelspec remove <kernel-name>  
  ```
