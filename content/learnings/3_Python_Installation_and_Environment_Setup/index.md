---
title: "Python Installation and Environment Setup"
date: 2025-12-10
description: "Add description"
summary: "Python"
tags: [""]
---

### 1. Installation

- **Step 1. Install [Visual Studio Code](https://code.visualstudio.com/docs/introvideos/basics)**: [Download & Install](https://code.visualstudio.com/download)

- **Step 2. Install Homebrew**: [Install](https://brew.sh/)

  Then add to your PATH
  
  ```bash
  echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/<username>/.zprofile
  # Run `brew shellenv` in every new terminal

  eval "$(/opt/homebrew/bin/brew shellenv)"
  # Apply the Homebrew environment settings immediately without restarting the terminal

  # brew --version
  ```

- **Step 3. Install Python 3.13 (using Homebrew)**:
  
  ```bash
  brew install python@3.13
  # Installed as: /opt/homebrew/bin/python3

  brew cleanup python@3.13
  # Clean up old files for python@3.13 (does NOT uninstall it)

  # which -a python python3 # Find all python/python3 executables in your PATH
  # which python python3 # Check which python/python3 is used by default
  ```


### 1. Environment Setup (using uv)

- **Step 1. Install [uv](https://github.com/astral-sh/uv)**:
  
  ```bash
  curl -LsSf https://astral.sh/uv/install.sh | sh
  ```

- **Step 2. Set up Python environment**:
  
  ```bash
  uv init 
  # Initialize a new Python project environment. 
  # It will:
  # - Create `pyproject.toml` if it does not exist
  # - Create or reuse a `.venv/` virtual environment
  #   - If `.venv/` exists, uv uses its Python interpreter
  #   - If not, uv creates one using the default `python3` on your PATH
  #     (Use a different version by running `python3.13 -m venv .venv` before `uv init`)
  # - Optionally create `uv.lock`
  # - Detect existing dependencies
  
  # uv run python <name>.py # Run Python scripts
  ```

- **Step 3. Install Python packages**:

  ```
  uv add regex torch torchvision PyYAML matplotlib requests tqdm notebook
  # uv add numpy pandas
  ```


### 2. Environment Setup (using Conda)

- **Step 1. Install [Miniconda](https://www.anaconda.com/docs/getting-started/miniconda/main)**

- **Step 2. Set up Python environment**:

To add

- **Step 3. Install Python packages**:

To add