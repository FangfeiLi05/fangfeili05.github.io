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

Main content is in Markdown, with PDFs stored in `static/files/`.

| Section | Content Directory | Live Page |
|--------|--------------------|-----------|
| Resume | `content/resume` | [fangfeili05.github.io/resume/](https://fangfeili05.github.io/resume/) |
| Papers | `content/papers` | [fangfeili05.github.io/papers/](https://fangfeili05.github.io/papers/) |
| Certifications | `content/certifications` | [fangfeili05.github.io/certifications/](https://fangfeili05.github.io/certifications/) |
| Learnings | `content/learnings` | [fangfeili05.github.io/learnings/](https://fangfeili05.github.io/learnings/) |

---

## License

- **Source code:** [MIT License](LICENSE.md)  
- **Content:** [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) (unless noted otherwise)

---

## Set Up & Usage

For theme details, see the [**Congo documentation**](https://jpanther.github.io/congo/docs/)

### Install Dependencies (macOS example)

`Git` (extended version), `Go`, `Node.js`, `HUGO`
```
brew install git go node hugo

git --version
go version
node -v
hugo version 
```

TailwindCSS (for custom styling)
```
npm install -D tailwindcss postcss autoprefixer
```


- Create a new repo named `<repo-name>` on your GitHub account.

- Create a new Hugo site
```
hugo new site <repo-name>
cd <repo-name>
```

- Initialize Git
```
git init
git branch -M main
git remote add origin https://github.com/<user-name>/<repo-name>.git
```

- Initialize Hugo modules
```
hugo mod init github.com/<user-name>//<repo-name>
```

- Add Congo theme
```
mkdir -p config/_default

# config/_default/module.toml
[[imports]]
path = "github.com/jpanther/congo/v2"
```

- Start the local server (also automatically downloads the theme):
```
hugo server
```
Visit: http://localhost:1313


### Configure the Site

- Remove the default config
```
rm hugo.toml
```

- Copy the default Congo config files
(except `module.toml`) from [link](https://github.com/jpanther/congo/tree/dev/config/_default), into 
```
config/_default/
``` 


Add `.gitignore`
```
touch .gitignore
```
Add
```
public/
resources/
.hugo_build.lock
.DS_Store
```

- What to say?
```
git add .
git commit -m "Initialize Hugo module"
git push --set-upstream origin main  # FIRST push (set upstream)
git push
```

Depoly in Github
- Change name of repo from `<repo-name>` to `<user-name>.github.io`
- Create `.github/worflows` and copy [`hugo.yaml`]() to 
```
mkdir -p .github/worflows
```

- Enable Deployment (GitHub Pages + GitHub Actions) 
[Publishing with a custom GitHub Actions workflow](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow). 

- Update your Git remote (since repo name changed)
```
git remote set-url origin https://github.com/<user-name>/<user-name>.github.io.git
git remote -v
```

- Online Deployment
```
git add .
git commit -m "Deploy Hugo module"
git push
```




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
