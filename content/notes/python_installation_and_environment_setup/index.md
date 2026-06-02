---
title: "Python Installation and Environment Setup"
date: 2025-12-15
description: "Add description"
summary: "Python"
tags: [""]
---

## Method 1 -- VS Code + Homebrew + `uv`

Best for general Python, web development, and small projects. Lightweight, fast, and modern.

### Installation

- [**VS Code**](https://code.visualstudio.com/docs/introvideos/basics): [Download & Install](https://code.visualstudio.com/download)

- **Homebrew**: [Install](https://brew.sh/)

  Then add Homebrew to your PATH:

  ```bash
  echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/<user-name>/.zprofile
  eval "$(/opt/homebrew/bin/brew shellenv)"
  ```

  - Ensure Homebrew is available in new terminal sessions
  - Apply Homebrew settings immediately without restarting the terminal

  (Optional) Verify installation

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

  (Optional) Verify installation

  ```bash
  python3 --version
  ```

- [**`uv`**](https://github.com/astral-sh/uv) (a fast Python package and environment manager):

  ```bash
  curl -LsSf https://astral.sh/uv/install.sh | sh
  ```

### Environment Setup

- **Step 1** - Create a Python Project Environment:

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

- **Step 2** - Install dependencies:

  ```bash
  uv add regex torch torchvision PyYAML matplotlib requests tqdm notebook
  ```

---

## Method 2 -- Conda

Best for data science, machine learning, and scientific computing. Heavier, but handles complex libraries well.

### Installation

- **Miniconda**: [Download & Install](https://www.anaconda.com/docs/getting-started/miniconda/main)

### Environment Setup

- **Step 1** - Create a Python project environment and install dependencies:
  
  ```bash
  conda env create -f environment.yaml
  ```

  Example `environment.yaml`: [View Example](/files/environment.yaml)

- **Step 2** - Enable automatic Jupyter kernel discovery:

  Create a environment for running JupyterLab (This step is done once only):

  ```bash
  conda create -n jupyter_env python=3.10 jupyterlab -c conda-forge
  ```
  
  In case to open Jupyter Lab:

  ```bash
  conda activate jupyter_env
  jupyter lab
  conda deactivate
  ```

  Install kernel discovery tool `nb_conda_kernels`, which allows JupyterLab to automatically detect all Conda environments as usable kernels (This step is done once only):

  ```bash
  conda activate jupyter_env
  conda install nb_conda_kernels -c conda-forge
  conda deactivate
  ```

  Install kernel support in each environment:

  ```bash
  conda activate <env-name>
  conda install ipykernel -c anaconda
  conda deactivate
  ```

  Alternatively, configure a Jupyter kernel manually (This step is optional):

  ```bash
  conda activate <env-name>
  ipython kernel install --user --name=<kernel-name>
  conda deactivate
  ```

  In case running this optional:
  
  List all available Jupyter kernels:

  ```bash
  conda activate jupyter_env
  jupyter kernelspec list
  conda deactivate
  ```

  Remove a specific Jupyter kernel:

  ```bash
  conda activate jupyter_env
  jupyter kernelspec remove <kernel-name>
  conda deactivate
  ```

---

## Extra Useful Commands

- List all Python / Python3 executables in `PATH`:

  ```bash
  which -a python python3
  ```

- Show the default Python / Python3 in use:

  ```bash
  which python python3
  ```

- Run Python scripts (with `uv`):

  ```bash
  uv run python <script-name>.py
  ```

- List all Conda environments and remove a Conda environment:

  ```bash
  conda env list
  
  conda env remove -n <env-name>
  conda clean --all
  ```

- Search from the current directory downward and delete all `.DS_Store` files (with confirmation):

  ```bash
  find . -name '.DS_Store' -type f -exec rm -i {} \;
  ```
