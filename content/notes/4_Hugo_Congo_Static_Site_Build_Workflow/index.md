---
title: "Hugo Congo Static Site Build Workflow"
date: 2025-12-27
description: "Add description"
summary: "Hugo Congo"
tags: [""]
---

## Installation and Setup

### 1. Install Dependencies (macOS)

- Install the required tools: **Git (extended)**, **Go**, **Node.js**, and **Hugo**.

  ```bash
  brew install git go node hugo
  ```

- (Optional) Verify the installations:

  ```bash
  git --version
  go version
  node -v
  hugo version
  ```

- Install **TailwindCSS** and related tooling for custom styling:

  ```bash
  npm install -D tailwindcss postcss autoprefixer
  ```

### 2. Create the Hugo Site (Local)

- Create a new Hugo site named `<site-name>` and initialize a local Git repository:

  ```bash
  hugo new site <site-name>
  cd <site-name>

  git init
  git branch -M main
  ```

### 3. Create the GitHub Repository (Remote)

- Create an **empty** GitHub repository named `<site-name>`.

### 4. Connect the Local Repository to GitHub

- Link the local repository to GitHub and push the initial commit:

  ```bash
  git remote add origin https://github.com/<username>/<site-name>.git

  git add .
  git commit -m "Initial commit"
  git push -u origin main
  ```

### 5. Install the Congo Theme (Hugo Module)

- Initialize the Hugo module:

  ```bash
  hugo mod init github.com/<username>/<site-name>
  ```

- Add the Congo theme:

  ```bash
  mkdir -p config/_default

  cat <<'EOF' > config/_default/module.toml
  [[imports]]
  path = "github.com/jpanther/congo/v2"
  EOF
  ```

- Start the development server (the theme will be downloaded automatically):

  ```bash
  hugo server
  ```

  Visit: [`http://localhost:1313`](http://localhost:1313)

- Remove the default Hugo configuration file:

  ```bash
  rm hugo.toml
  ```

- Copy Congo's default configuration files (excluding `module.toml`) from [this link](https://github.com/jpanther/congo/tree/dev/config/_default) into `config/_default/`.


### 6. Add `.gitignore` and Commit Changes

- Create and populate the `.gitignore` file:

  ```bash
  touch .gitignore

  cat <<'EOF' >> .gitignore
  public/
  resources/
  .hugo_build.lock
  .DS_Store
  EOF
  ```

- Commit and push the changes:

  ```bash
  git add .
  git commit -m "Set up Hugo module and Congo theme"
  git push
  ```

### 7. Deploy to GitHub Pages

- Rename the repository from `<site-name>` to `<username>.github.io`.

- Update the Git remote URL:

  ```bash
  git remote set-url origin https://github.com/<username>/<username>.github.io.git
  git remote -v
  ```

- Add a GitHub Actions workflow by creating the directory `.github/workflows/` and copying the workflow file of [this link](https://github.com/pmichaillat/hugo-website/blob/main/.github/workflows/hugo.yml) into `.github/workflows/`.

  ```bash
  mkdir -p .github/workflows
  ```

- Enable deployment using **GitHub Pages** with **GitHub Actions**, following the official guide: [Publishing with a custom GitHub Actions workflow](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow).

- Commit and deploy the site:

  ```bash
  git add .
  git commit -m "Deploy Hugo site"
  git push
  ```

  Site URL: `https://<username>.github.io/`

## Configuration Additions

- To add

## Useful Links

- [Congo Documentation](https://jpanther.github.io/congo/docs/)
- [Hugo & Congo Configuration](https://applegamer22.github.io/posts/hugo/)
- [GitHub: Minimalist Hugo Template for Academic Websites](https://github.com/pmichaillat/hugo-website)
- [GitHub: Congo](https://github.com/jpanther/congo)
- [GitHub: applegamer22.github.io](https://github.com/AppleGamer22/applegamer22.github.io)
