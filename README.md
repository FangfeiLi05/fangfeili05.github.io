# fangfeili05.github.io — Personal Website (Source Code)

This repository contains the source code for my personal website:
[**https://fangfeili05.github.io**](https://fangfeili05.github.io).

The site is built with [**Hugo**](https://github.com/gohugoio/hugo) using the [**Congo**](https://github.com/jpanther/congo) theme and deployed via **GitHub Pages**.

---

## Overview

### 1. Tech Stack

- **Hugo** (extended) - static site generator
- **Congo** - theme (For details, [**Congo documentation**](https://jpanther.github.io/congo/docs/))
- **TailwindCSS** - custom styling
- **Markdown** - content
- **GitHub Pages + GitHub Actions** - deployment

### 2. Project Structure

```bash
root/
│
├── config/                     # Site configuration
│   └── _default/
│       ├── hugo.toml
│       ├── params.toml
│       ├── menus.en.toml
│       ├── languages.en.toml
│       ├── module.toml
│       └── markup.toml
│
├── content/                    # Website content
│   ├── resume/                 → https://fangfeili05.github.io/resume/
│   ├── papers/                 → https://fangfeili05.github.io/papers/
│   ├── certifications/         → https://fangfeili05.github.io/certifications/
│   └── notes/                  → https://fangfeili05.github.io/notes/
│
├── layouts/                    # Custom templates / overrides
│   ├── _partials/
│   └── list.html
│
├── assets/                     # Hugo Pipes (images, CSS, JS)
│   └── img/
│       ├── author.jpg
│       ├── logo.jpg
│       └── dark-logo.jpg
│
├── static/                     # Static files (served as site root)
│   ├── files/
│   └── favicon.ico
│
└── themes/                     # External themes (optional)
```

### 3. License

- **Source code:** [`MIT License`](LICENSE.md)
- **Content:** [`CC BY 4.0`](https://creativecommons.org/licenses/by/4.0/) (unless stated otherwise)

---

## Setup Guide

### 1. Install Dependencies (macOS)

- Install required tools (`Git` (extended), `Go`, `Node.js`, and `Hugo`):

  ```bash
  brew install git go node hugo
  npm install -D tailwindcss postcss autoprefixer
  ```

- (Optional) Verify installation:

  ```bash
  git --version
  go version
  node -v
  hugo version 
  ```

- (Optional) Install `TailwindCSS` for custom styling:

  ```bash
  brew install git go node hugo
  npm install -D tailwindcss postcss autoprefixer
  ```

### 2. Create the Hugo Site (Local)

- Create a new Hugo site named `<site-name>` and initialize Git locally:

  ```bash
  hugo new site <site-name>
  cd <site-name>

  git init
  git branch -M main
  ```

### 3. Create the GitHub Repository (Remote)

- Create a new **empty** GitHub repository named `<site-name>`

### 4. Connect and Push to GitHub

- Connect the local repository to GitHub and push the initial commit:

  ```bash
  git remote add origin https://github.com/<username>/<site-name>.git

  git add .
  git commit -m "Initial commit"
  git push -u origin main
  ```

### 5. Install the Congo Theme

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

- Start the development server (the theme will be downloaded automatically).

  ```bash
  hugo server
  ```

  Visit: [`http://localhost:1313`](http://localhost:1313)

### 6. Configure the Theme

- Remove the default config file:

  ```bash
  rm hugo.toml
  ```

- Copy Congo's default config files (except `module.toml`) from [source](https://github.com/jpanther/congo/tree/dev/config/_default) into `config/_default/`.

### 7. Add `.gitignore`

- Add `.gitignore`

  ```bash
  touch .gitignore

  cat <<'EOF' >> .gitignore
  public/
  resources/
  .hugo_build.lock
  .DS_Store
  EOF
  ```

- Commit changes:

  ```bash
  git add .
  git commit -m "Hugo module setup"
  git push
  ```

### 8. Deploy to GitHub Pages

- Rename the repository from `<site-name>` to `<username>.github.io`

- Update the Git remote:

  ```bash
  git remote set-url origin https://github.com/<username>/<username>.github.io.git
  git remote -v
  ```

- Add GitHub Actions workflow by creating the directory `.github/workflows/` and copying the workflow file [`hugo.yml`](.github/workflows/hugo.yml) into it.

  ```bash
  mkdir -p .github/workflows
  ```

- Enable deployment using **GitHub Pages** with **GitHub Actions**, following the guide: [Publishing with a custom GitHub Actions workflow](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow).

- Commit and deploy:

  ```bash
  git add .
  git commit -m "Deploy Hugo site"
  git push
  ```

  Site will be live at: `https://<username>.github.io/`

---

## Usage Guide

### 1. Modify Config Files

- Modify `hugo.toml`.
  
  From:

  ```bash
  # baseURL = "https://your_domain.com/"
  ```

  To:

  ```bash
  baseURL = "https://<username>.github.io/"
  ```

- Modify `params.toml`.

  From:

  ```bash
  colorScheme = "congo"
  enableSearch = false
  # header.logo = "img/logo.jpg"
  # header.logoDark = "img/dark-logo.jpg"
  footer.showAppearanceSwitcher = false
  homepage.layout = "page"
  ```

  To:

  ```bash
  colorScheme = "fire"
  enableSearch = true
  header.logo = "img/logo.jpg"
  header.logoDark = "img/dark-logo.jpg"
  footer.showAppearanceSwitcher = true
  homepage.layout = "profile"
  ```

- Modify `menus.en.toml`.

  From:

  ```bash
  [[main]]
    name = "Blog"
    pageRef = "posts"
    weight = 10

  [[main]]
    name = "Categories"
    pageRef = "categories"
    weight = 20

  [[main]]
    name = "Tags"
    pageRef = "tags"
    weight = 30
  ```
  
  To:

  ```bash
  [[main]]
    name = "Resume"
    pageRef = "resume"
    #url = "/files/resume_FL_20251201.pdf"
    weight = 10

  [[main]]
    name = "Papers"
    pageRef = "papers"
    weight = 20

  [[main]]
    name = "Certifications"
    pageRef = "certifications"
    weight = 30

  [[main]]
    name = "Notes"
    pageRef = "notes"
    weight = 40
  ```

- Modify `languages.en.toml`.

  From:

  ```bash
  title = "Congo"
  # copyright = "Copy, _right?_ :thinking_face:"
  # params.author.name = "Your name here"
  # params.author.image = "img/author.jpg"
  ```

  To:

  ```bash
  title = "FLi | Homepage"
  copyright = "Copyright © 2025, Fangfei Li. All rights reserved."
  params.author.name = "Fangfei Li"
  params.author.image = "img/author.jpg"
  ```

### 2. Add Directories and Files

- Create the directory `assets/img/` and add files `author.jpg`, `logo.jpg` `dark-logo.jpg` into it.

  ```bash
  mkdir -p assets/img
  ```

- Create the directory `layouts/_partials/` and add the file [`list.html`](layouts/_partials/list.html) into it.

- Create the directory `static/files/` and add files into it.

  ```bash
  mkdir -p static/files
  ```

### 3. Useful Links

- [https://favicon.io/favicon-converter/](https://favicon.io/favicon-converter/)

- [https://wallpapercave.com/1600x1200-wallpapers](https://wallpapercave.com/1600x1200-wallpapers)


<!-- 
Add
- assets:
img -> author.jpg

layouts/list.html

- Optional Cleanup (.DS_Store files on macOS)
```
find . -name '.DS_Store' -type f
find . -name '.DS_Store' -type f -delete
```
-->