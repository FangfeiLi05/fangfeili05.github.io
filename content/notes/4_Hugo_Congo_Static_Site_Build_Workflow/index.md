---
title: "Hugo Congo Static Site Build Workflow"
date: 2025-12-28
description: "Add description"
summary: "Hugo & Congo"
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
  # Generated files by hugo
  public/
  /resources/_gen/

  # Temporary lock file while building
  .hugo_build.lock

  # Other
  _backup/
  **/.DS_Store
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

---

## Configuration and Contents Updates

### 1. Update Configuration Files

- Modify `hugo.toml`:

  | Section | From | To |
  |-----|-----|-----|
  | -- | `# baseURL = "https://your_domain.com/"` | `baseURL = "https://<username>.github.io/"` |

- Modify `params.toml`:

  | Section | From | To |
  |-----|-----|-----|
  | -- | `colorScheme = "congo"`<br>`enableSearch = false`<br>`enableCodeCopy = false` | `colorScheme = "fruit"`<br>`enableSearch = true`<br>`enableCodeCopy = true` |
  | `header` | `# logo = "img/logo.jpg"`<br>`# logoDark = "img/dark-logo.jpg"` | `logo = "img/logo.jpg"`<br>`logoDark = "img/dark-logo.jpg"` |
  | `footer` | `showAppearanceSwitcher = false` | `showAppearanceSwitcher = true` |
  | `homepage` | `layout = "page"` | `layout = "profile"` |

- Modify `languages.en.toml`:

  | Section | From | To |
  |-----|-----|-----|
  | -- | `title = "Congo"`<br>`# copyright = "Copy, _right?_ :thinking_face:"` | `# title = "Home"`<br>`copyright = "Copyright © 2025, Fangfei Li. All rights reserved."` |
  | `params.author` | `# name = "Your name here"`<br>`# image = "img/author.jpg"` | `name = "Fangfei Li"`<br>`image = "img/author.jpg"`|

- Modify `menus.en.toml`: [View example](https://github.com/FangfeiLi05/fangfeili05.github.io/blob/main/config/_default/menus.en.toml)

### 2. Add Assets

- Add the `assets/` directory to store images, stylesheets, and a custom color scheme ([View example](https://github.com/FangfeiLi05/fangfeili05.github.io/tree/main/assets)):

  ```text
  assets/
  ├── img/
  │   ├── author.jpg
  │   ├── logo.jpg
  │   └── dark-logo.jpg
  └── css/
      ├── schemes/
      │   └── fruit.css           # Custom color scheme
      └── custom.css
  ```

  The contents of the directory `css/` are sourced from [this link](https://github.com/AppleGamer22/applegamer22.github.io/tree/master/assets/css).

### 3. Add Layouts

- Add the `layouts/` directory for custom templates and overrides ([View example](https://github.com/FangfeiLi05/fangfeili05.github.io/tree/main/layouts)):

  ```text
  layouts/
  ├── _partials/                  # Reusable partial templates
  └── list.html                   # Custom list page template
  ```

  The contents of the directory `_partials/` (excluding `logo.html`) are sourced from [this link](https://github.com/AppleGamer22/applegamer22.github.io/tree/master/layouts/partials).

### 4. Add Static Files

- Add the `static/` directory for fonts, icons, and downloadable resources ([View example](https://github.com/FangfeiLi05/fangfeili05.github.io/tree/main/static)):

  ```text
  static/
  ├── files/                      # Downloadable resources
  ├── FiraCode-Regular.ttf        # Fira Code font
  ├── favicon.ico
  ├── favicon-32x32.png
  ├── favicon-16x16.png
  ├── apple-touch-icon.png
  ├── android-chrome-512x512.png
  ├── android-chrome-192x192.png
  └── site.webmanifest
  ```

### 4. Add `tailwind.config.js`
  
  The file `tailwind.config.js` is sourced from [this link](https://github.com/AppleGamer22/applegamer22.github.io/blob/master/tailwind.config.js).

---

## Useful Links

- [Congo Documentation](https://jpanther.github.io/congo/docs/)
- [GitHub Repository: Congo Theme](https://github.com/jpanther/congo)
- [Hugo & Congo Configuration](https://applegamer22.github.io/posts/hugo/)
- [GitHub Repository: Personal Site Example (applegamer22.github.io)](https://github.com/AppleGamer22/applegamer22.github.io)
- [GitHub Repository: Minimalist Hugo Template for Academic Websites](https://github.com/pmichaillat/hugo-website)
