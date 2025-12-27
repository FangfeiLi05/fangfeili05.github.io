# fangfeili05.github.io — Personal Website (Source Code)

This repository contains the source code for my personal website:
[**https://fangfeili05.github.io**](https://fangfeili05.github.io).

The site is built with [**Hugo**](https://github.com/gohugoio/hugo) using the [**Congo**](https://github.com/jpanther/congo) theme and deployed via **GitHub Pages**.

---

## Overview

### 1. Tech Stack

- **Hugo** (extended) - static site generator
- **Congo** - theme
- **TailwindCSS** - custom styling
- **Markdown** - content
- **GitHub Pages + GitHub Actions** - deployment

### 2. Project Structure

```bash
root/
├── config/                     # Site configuration
│   └── _default/
│       ├── hugo.toml           # Main Hugo configuration
│       ├── params.toml         # Theme parameters
│       ├── menus.en.toml       # Navigation menus (English)
│       ├── languages.en.toml   # Language settings (English)
│       ├── module.toml         # Hugo modules configuration
│       └── markup.toml         # Markdown/rendering settings
│
├── content/                    # Website content
│   ├── resume/                 # /resume/
│   ├── papers/                 # /papers/
│   ├── certifications/         # /certifications/
│   └── notes/                  # /notes/
│
├── layouts/                    # Custom templates / overrides
│   ├── _partials/              # Partial templates
│   └── list.html               # Custom list page template
│
├── assets/                     # Hugo Pipes assets (processed)
│   └── img/
│       ├── author.jpg
│       ├── logo.jpg
│       └── dark-logo.jpg
│
└── static/                     # Static files (served at site root)
    ├── files/                  # Downloadable files
    ├── FiraCode-Regular.ttf    # Fira Code font
    ├── favicon.ico
    ├── favicon-32x32.png
    ├── favicon-16x16.png
    ├── apple-touch-icon.png
    ├── android-chrome-512x512.png
    ├── android-chrome-192x192.png
    └── site.webmanifest
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

  | From | To |
  |------|----|
  | `# baseURL = "https://your_domain.com/"` | `baseURL = "https://<username>.github.io/"` |

- Modify `params.toml`.

  | From | To |
  |------|----| 
  | `colorScheme = "congo"` | `colorScheme = "fruit"` |
  | `enableSearch = false` | `enableSearch = true` |
  | `enableCodeCopy = false` | `enableCodeCopy = true` |
  | `[header]`<br>`#`&emsp;`logo = "img/logo.jpg"`<br>`#`&emsp;`logoDark = "img/dark-logo.jpg"`| `[header]`<br>&emsp;`logo = "img/logo.jpg"`<br>&emsp;`logoDark = "img/dark-logo.jpg"`|
  | `[footer]`<br>&emsp;`showAppearanceSwitcher = false` | `[footer]`<br>&emsp;`showAppearanceSwitcher = true` |
  | `[homepage]`<br>&emsp;`layout = "page"` | `[homepage]`<br>&emsp;`layout = "profile"` |

- Modify `menus.en.toml`.

  | From | To |
  |------|----| 
  | `[[main]]`<br>&emsp;`name = "Blog"`<br>&emsp;`pageRef = "posts"`<br>&emsp;`weight = 10`<br>`[[main]]`<br>&emsp;`name = "Categories"`<br>&emsp;`pageRef = "categories"`<br>&emsp;`weight = 20`<br>`[[main]]`<br>&emsp;`name = "Tags"`<br>&emsp;`pageRef = "tags"`<br>&emsp;`weight = 30` | `[[main]]`<br>&emsp;`name = "Resume"`<br>&emsp;`pageRef = "resume"`<br>&emsp;`weight = 10`<br>`[[main]]`<br>&emsp;`name = "Papers"`<br>&emsp;`pageRef = "papers"`<br>&emsp;`weight = 20`<br>`[[main]]`<br>&emsp;`name = "Certifications"`<br>&emsp;`pageRef = "certifications"`<br>&emsp;`weight = 30`<br>`[[main]]`<br>&emsp;`name = "Notes"`<br>&emsp;`pageRef = "notes"`<br>&emsp;`weight = 40` |

- Modify `languages.en.toml`.

  | From | To |
  |------|----| 
  | `title = "Congo"` | `# title = "Home"` |
  | `# copyright = "Copy, _right?_ :thinking_face:"` | `copyright = "Copyright © 2025, Fangfei Li. All rights reserved."` |
  | `[params.author]`<br>`#`&emsp;`name = "Your name here"`<br>`#`&emsp;`image = "img/author.jpg"` | `[params.author]`<br>&emsp;`name = "Fangfei Li"`<br>&emsp;`image = "img/author.jpg"`|

### 2. Useful Links

- [Congo Documentation](https://jpanther.github.io/congo/docs/)

- [Hugo & Congo Configuration](https://applegamer22.github.io/posts/hugo/)

- [Favicon Converter Tool](https://favicon.io/favicon-converter/)

- [Wallpapers](https://wallpapercave.com/1600x1200-wallpapers)

<!--
- Optional Cleanup (.DS_Store files on macOS)
```
find . -name '.DS_Store' -type f
find . -name '.DS_Store' -type f -delete
```
-->