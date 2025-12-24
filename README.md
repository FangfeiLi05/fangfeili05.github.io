# fangfeili05.github.io — Personal Website (Source Code)

This repository contains the Hugo-based source code for my personal website:
[**fangfeili05.github.io**](https://fangfeili05.github.io/).

The site is built using the [**Hugo**](https://github.com/gohugoio/hugo) static site generator with the [**Congo**](https://github.com/jpanther/congo) theme.

---

## 🚀 Tech Stack

- **Hugo** (extended version) — site generator
- **Congo** — theme (For details, see the [**Congo documentation**](https://jpanther.github.io/congo/docs/))
- **TailwindCSS** — custom styling
- **Markdown** — all content
- **GitHub Pages + GitHub Actions** — deployment

---

## 📚 Content Structure

```bash
root/
│
├── config/                     # 1. Site configuration
│   └── _default/
│       ├── hugo.toml
│       ├── params.toml
│       ├── menus.en.toml
│       ├── languages.en.toml
│       ├── module.toml
│       └── markup.toml
│
├── content/                    # 2. Website content
│   ├── resume/                 → https://fangfeili05.github.io/resume/
│   ├── papers/                 → https://fangfeili05.github.io/papers/
│   ├── certifications/         → https://fangfeili05.github.io/certifications/
│   └── learnings/              → https://fangfeili05.github.io/learnings/
│
├── layouts/                    # 3. Templates / partials
│   ├── _partials/
│   └── list.html
│
├── assets/                     # 4. Hugo Pipes (SCSS, JS, images)
│   └── img/
│       ├── author.jpg
│       ├── logo.jpg
│       └── dark-logo.jpg
│
├── static/                     # 5. Served directly at site root
│   ├── files/
│   └── favicon.ico
│
└── themes/                     # 6. External theme code (optional)
```

---

## License

- **Source code:** [MIT License](LICENSE.md)
- **Content:** [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) (unless noted otherwise)

---

## Setup & Usage

### 1. Install dependencies (macOS)

- Install required tools: `Git` (extended), `Go`, `Node.js`, and `Hugo`
- (Optional) Install `TailwindCSS` for custom styling

```bash
brew install git go node hugo
npm install -D tailwindcss postcss autoprefixer
```

- Verify installation (optional):

  ```bash
  git --version
  go version
  node -v
  hugo version 
  ```

### 2. Create the project (local)

- Create a new Hugo site named `<site-name>` and initialize Git locally:

  ```bash
  hugo new site <site-name>
  cd <site-name>

  git init
  git branch -M main
  ```

### 3. Create the GitHub repository (remote)

- Create a new empty repository on GitHub named `<site-name>`

### 4. Connect and push to GitHub

- Connect the local repository to GitHub and push the initial commit:

  ```bash
  git remote add origin https://github.com/<username>/<site-name>.git
  git add .
  git commit -m "Initial commit"
  git push -u origin main  # -u, --set-upstream (set upstream): first push only
  ```

### 5. Download and install the Congo theme

- Initialize the Hugo module:

  ```bash
  hugo mod init github.com/<username>/<site-name>
  ```

- Add the Congo theme by creating the file `config/_default/module.toml` with the content shown in the example [`module.toml`](./config/_default/module.toml), by running in the terminal:

  ```bash
  mkdir -p config/_default

  cat <<'EOF' > config/_default/module.toml
  [[imports]]
  path = "github.com/jpanther/congo/v2"
  EOF
  ```

- Start the local development server (the theme will be downloaded automatically).
  Visit: [http://localhost:1313](http://localhost:1313)

  ```bash
  hugo server
  ```

### 6. Set up theme configuration files

- Remove the default config `hugo.toml`:

  ```bash
  rm hugo.toml
  ```

- Copy Congo’s default configuration files (except `module.toml`) from [here](https://github.com/jpanther/congo/tree/dev/config/_default) into `config/_default/`.

### 7. Extra

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

- Commit Changes

  ```bash
  git add .
  git commit -m "Hugo module setup"
  git push
  ```

### 8. Depoly in Github

- Rename the repository from `<site-name>` to `<username>.github.io`

- Update the Git remote to reflect the renamed repository.

  ```bash
  git remote set-url origin https://github.com/<username>/<username>.github.io.git
  git remote -v
  ```

- Add a GitHub Actions workflow by creating the directory `.github/worflows/` and copying the workflow file [`hugo.yaml`](./hugo.yaml) into it.

  ```bash
  mkdir -p .github/worflows
  ```

- Enable deployment using **GitHub Pages** with **GitHub Actions**, following the guide: [Publishing with a custom GitHub Actions workflow](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow).

- Deploy online:

  ```bash
  git add .
  git commit -m "Deploy Hugo site"
  git push
  ```


<!-- 
### Customize Congo Settings

- Modify
- config -> _default -> languages.en.toml
title = "Homepage"

- config -> _default -> params.toml
homepage.layout = "profile"
list.groupByYear = false
article.showTableOfContents

- config -> _default -> hugo.toml
baseURL = "https://<username>.github.io/"

Add
- assets:
img -> author.jpg

layouts/list.html


useful web
https://favicon.io/favicon-converter/
https://wallpapercave.com/1600x1200-wallpapers


- Optional Cleanup (.DS_Store files on macOS)
```
find . -name '.DS_Store' -type f
find . -name '.DS_Store' -type f -delete

echo .DS_Store >> .gitignore
git add .gitignore
git commit -m "Ignore .DS_Store files"
```
-->