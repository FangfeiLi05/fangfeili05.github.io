---
title: "Python Installation and Environment Setup"
date: 2025-12-10
description: "Add description"
summary: "Python"
tags: [""]
---

## Method 1 -- VS Code + Homebrew + `uv`

Best for general Python, web development, and small projects. Lightweight, fast, and modern.

- **Step 1. Install VS Code**
  
  [Info](https://code.visualstudio.com/docs/introvideos/basics)
  
  [Download & Install](https://code.visualstudio.com/download)

- **Step 2. Install Homebrew**
  
  [Install](https://brew.sh/)
  
  Then add Homebrew to your PATH, by running in Terminal

  ```bash
  echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/<user-name>/.zprofile  # Ensure Homebrew is available in new terminal sessions
  eval "$(/opt/homebrew/bin/brew shellenv)"                                         # Apply Homebrew settings immediately without restarting the terminal

  # brew --version
  ```

- **Step 3. Install Python**:
  
  Run in Terminal

  ```bash
  brew install python@3.13  # Installed as: /opt/homebrew/bin/python3
  brew cleanup python@3.13  # Remove outdated files (does NOT uninstall Python)

  # python3 --version
  ```

- **Step 4. Install `uv` (fast Python package and environment manager)**:
  
  [Info](https://github.com/astral-sh/uv)
  
  Run in Terminal
  
  ```bash
  curl -LsSf https://astral.sh/uv/install.sh | sh
  ```

- **Step 5. Create a Python project environment**:
  
  Run in Terminal

  ```bash
  uv init

  # This automatically:
  #  - Creates `pyproject.toml` if missing
  #  - Creates or reuses a virtual environment (`.venv`) 
  #    - If `.venv` exists, uses its Python interpreter
  #    - Otherwise, creates one using the default `python3` from PATH
  #      - To use a specific version, run `python3.13 -m venv .venv` before `uv init`
  #  - Optionally generates `uv.lock`
  #  - Detects existing dependencies

  # uv run python <script-name>.py
  # Run Python scripts
  ```

- **Step 6. Install dependencies**:
  
  Run in Terminal

  ```bash
  uv add regex torch torchvision PyYAML matplotlib requests tqdm notebook
  ```

---

## Method 2 -- Conda

Best for data science, machine learning, and scientific computing. Heavier, but handles complex libraries well.

- **Step 1. Install Miniconda**
  
  [Download and install](https://www.anaconda.com/docs/getting-started/miniconda/main)

- **Step 2. Create a Python project environment and install dependencies**:
  
  Run in Terminal
  
  ```bash
  conda env create -f environment.yaml
  ```

  Example: [`environment.yaml`](/files/environment.yaml)

- **Step 3. Create a Python Jupyter environment (for running JupyterLab)**
  
  Run in Terminal
  
  ```bash
  conda create -n jupyter_env python=3.14 jupyterlab -c conda-forge

  # conda activate jupyter_env
  # jupyter lab
  # conda deactivate
  ```

- **Step 4a (recommended; choose either 4a or 4b). Enable automatic Jupyter kernel discovery**
  
  Run in Terminal

  ```bash
  conda activate jupyter_env
  conda install nb_conda_kernels -c conda-forge
  conda deactivate
  ```
  
  `nb_conda_kernels` allows JupyterLab to automatically detect all Conda environments as usable kernels.

- **Step 4b (choose either 4a or 4b). Configure a Jupyter kernel manually**
  
  Run in Terminal

  ```bash
  conda activate <env-name>
  conda install ipykernel -c anaconda
  ipython kernel install --user --name=<kernel-name>
  conda deactivate
  ```

---

## Extra Useful Commands

-

  ```bash
  which -a python python3  # List all Python / Python3 executables in PATH
  which python python3     # Show the default Python / Python3 in use
  ```

-

  ```bash
  conda env list                  # List all Conda environments
  conda env remove -n <env-name>  # Remove a Conda environment
  conda clean --all               # Free up disk space by removing unused packages and caches
  ```

-

  ```bash
  jupyter kernelspec list                  # List all available Jupyter kernels (Use the Jupyter installation currently on your PATH)
  jupyter kernelspec remove <kernel-name>  # Remove a specific Jupyter kernel
  ```
