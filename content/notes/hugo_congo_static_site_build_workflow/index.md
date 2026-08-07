---
title: "Building a Static Website with Hugo and Congo"
date: 2025-12-01
description: "Add description"
summary: "Hugo, Congo theme, GitHub Pages deployment workflow"
tags: [""]
---

## Installation (macOS)

Install required tools: Git (extended version), Go, Node.js, and Hugo:

```bash
brew install git go node hugo
```

(Optional) Verify the installations:

```bash
git --version
go version
node -v
hugo version
```

Install tools for custom styling: TailwindCSS and related tools:

```bash
npm install -D tailwindcss postcss autoprefixer
```

## Create Hugo Website

Create a new Hugo site named `<site-name>`:

```bash
hugo new site <site-name>
cd <site-name>
```

Initialize Git:

```bash
git init
git branch -M main
```

Create an empty GitHub repository named `<site-name>`.

Connect the local repository:

```bash
git remote add origin https://github.com/<username>/<site-name>.git
```

Commit and push:

```bash
git add .
git commit -m "Initial commit"
git push -u origin main
```

## Add Congo Theme (Using Hugo Modules)

Initialize Hugo Modules:

```bash
hugo mod init github.com/<username>/<site-name>
```

Create `module.toml` to configure the Congo theme:

```bash
mkdir -p config/_default

cat <<'EOF' > config/_default/module.toml
[[imports]]
path = "github.com/jpanther/congo/v2"
EOF
```

Start the local server:

```bash
hugo server
```

The Congo theme will be downloaded automatically.

Open: [`http://localhost:1313`](http://localhost:1313)

Remove the default Hugo configuration:

```bash
rm hugo.toml
```

Copy Congo's default configuration files (excluding `module.toml`) from [this link](https://github.com/jpanther/congo/tree/dev/config/_default) to `config/_default/`.

Add `.gitignore` and add Hugo-generated files and temporary files:

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

Commit and push:

```bash
git add .
git commit -m "Set up Hugo module and Congo theme"
git push
```

## Deploy to GitHub Pages

Rename the repository from `<site-name>` to `<username>.github.io`.

Update the Git remote:

```bash
git remote set-url origin https://github.com/<username>/<username>.github.io.git
```

(Optional) Verify the remote:

```bash
git remote -v
```

Add the GitHub Actions workflow:

- Create the directory `.github/workflows/`:

  ```bash
  mkdir -p .github/workflows
  ```

- Copy the [Hugo workflow files](https://github.com/pmichaillat/hugo-website/blob/main/.github/workflows/hugo.yml) into `.github/workflows/`.

Enable deployment using **GitHub Pages** with **GitHub Actions**: [Publishing with a custom GitHub Actions workflow](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow).

Commit and push:

```bash
git add .
git commit -m "Deploy Hugo site"
git push
```

Site: `https://<username>.github.io/`

---

## Customize Website

### Configuration

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
  | -- | `title = "Congo"`<br>`# copyright = "Copy, _right?_ :thinking_face:"` | `# title = "Home"`<br>`copyright = "Copyright © 2026. All rights reserved."` |
  | `params.author` | `# name = "Your name here"`<br>`# image = "img/author.jpg"` | `name = "Fangfei Li"`<br>`image = "img/author.jpg"`|

- Modify `menus.en.toml`: [View example](https://github.com/FangfeiLi05/fangfeili05.github.io/blob/main/config/_default/menus.en.toml)

### Assets

- Add the `assets/` directory to store images, stylesheets, and a custom color scheme ([View Example](https://github.com/FangfeiLi05/fangfeili05.github.io/tree/main/assets)):

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

### Layouts

- Add the `layouts/` directory for custom templates and overrides ([View Example](https://github.com/FangfeiLi05/fangfeili05.github.io/tree/main/layouts)):

  ```text
  layouts/
  ├── _partials/                  # Reusable partial templates
  └── list.html                   # Custom list page template
  ```

  The contents of the directory `_partials/` are sourced from [this link](https://github.com/AppleGamer22/applegamer22.github.io/tree/master/layouts/partials). Remove `logo.html` to enable the logo.

### Static Files

- Add the `static/` directory for fonts, icons, and downloadable resources ([View Example](https://github.com/FangfeiLi05/fangfeili05.github.io/tree/main/static)):

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

### Tailwind Configuration
  
  The file `tailwind.config.js` is sourced from [this link](https://github.com/AppleGamer22/applegamer22.github.io/blob/master/tailwind.config.js).

---

## Useful Links

- [Congo Documentation](https://jpanther.github.io/congo/docs/)
- [GitHub Repository: Congo Theme](https://github.com/jpanther/congo)
- [Hugo & Congo Configuration](https://applegamer22.github.io/posts/hugo/)
- [GitHub Repository: Personal Site Example (applegamer22.github.io)](https://github.com/AppleGamer22/applegamer22.github.io)
- [GitHub Repository: Minimalist Hugo Template for Academic Websites](https://github.com/pmichaillat/hugo-website)
