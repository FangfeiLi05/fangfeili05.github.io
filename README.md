# fangfeili05.github.io — Personal Website (Source Code)

This repository contains the Hugo-based source code for my personal website:  
[**fangfeili05.github.io**](https://fangfeili05.github.io/). 

The site is built using the [**Hugo**](https://github.com/gohugoio/hugo) static site generator with the [**Congo**](https://github.com/jpanther/congo) theme.

---

## 🚀 Tech Stack

- **Hugo** (extended version) — site generator  
- **Congo** — theme  
- **TailwindCSS** — custom styling  
- **Markdown** — all content  
- **GitHub Pages + GitHub Actions** — deployment  

---

## 📚 Content Structure

my-hugo-site/
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

---

## License

- **Source code:** [MIT License](LICENSE.md)  
- **Content:** [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) (unless noted otherwise)

---

## Set Up & Usage

For theme details, see the [**Congo documentation**](https://jpanther.github.io/congo/docs/)

### Install Dependencies (macOS example)

Required tools: `Git` (extended), `Go`, `Node.js`, `HUGO`

```bash
brew install git go node hugo

git --version
go version
node -v
hugo version 
```

Install `TailwindCSS` (for custom styling)

```
npm install -D tailwindcss postcss autoprefixer
```

### Create Your Project

Create a new GitHub repo named `<repo-name>`

reate a new Hugo site

```bash
hugo new site <repo-name>
cd <repo-name>
```

Initialize Git

```bash
git init
git branch -M main
git remote add origin https://github.com/<user-name>/<repo-name>.git
```

### Initialize Hugo modules

```bash
hugo mod init github.com/<user-name>//<repo-name>
```

Add Congo theme

Create the `config/_default/module.toml`

```bash
mkdir -p config/_default

touch module.toml
# with content 
[[imports]]
path = "github.com/jpanther/congo/v2"
```

Start local development server (also automatically downloads the theme)

```bash
hugo server
```

Visit: http://localhost:1313


### Configure the Site

Remove the default config

```bash
rm hugo.toml
```

Copy Congo’s default config files
(except `module.toml`) from [link](https://github.com/jpanther/congo/tree/dev/config/_default), into

```bash
config/_default/
``` 

Add `.gitignore`

```bash
touch .gitignore

# Add the following:
# public/
# resources/
# .hugo_build.lock
# .DS_Store
```


First Commit

```bash
git add .
git commit -m "Initialize Hugo module"
git push --set-upstream origin main  # First push (set upstream)
git push
```

### Depoly in Github

Rename repo from `<repo-name>` to `<user-name>.github.io`

Add GitHub Actions workflow
```
mkdir -p .github/worflows
```

Copy your `hugo.yaml` workflow file into this folder.


Enable Deployment (GitHub Pages + GitHub Actions) 
[Publishing with a custom GitHub Actions workflow](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow). 


Update your Git remote (since repo name changed)

```bash
git remote set-url origin https://github.com/<user-name>/<user-name>.github.io.git
git remote -v
```

- Online Deployment
```
git add .
git commit -m "Deploy Hugo module"
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
baseURL = "https://<user-name>.github.io/"

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