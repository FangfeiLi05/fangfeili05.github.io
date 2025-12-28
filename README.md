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
├── config/                     # Site-wide configuration
│   └── _default/
│       ├── hugo.toml           # Core Hugo settings
│       ├── params.toml         # Theme-specific parameters
│       ├── menus.en.toml       # English navigation menus
│       ├── languages.en.toml   # English language configuration
│       ├── module.toml         # Hugo module definitions
│       └── markup.toml         # Markdown and rendering options
│
├── content/                    # Site content
│   ├── resume/                 # /resume/ section
│   ├── papers/                 # /papers/ section
│   ├── certifications/         # /certifications/ section
│   └── notes/                  # /notes/ section
│
├── layouts/                    # Custom templates and overrides
│   ├── _partials/              # Reusable partial templates
│   └── list.html               # Custom list page template
│
├── assets/                     # Assets processed by Hugo Pipes
│   ├── img/
│   │   ├── author.jpg
│   │   ├── logo.jpg
│   │   └── dark-logo.jpg
│   └── css/
│       ├── schemes/
│       │   └── fruit.css
│       └── custom.css
│
└── static/                     # Static files served from the site root
    ├── files/                  # Downloadable resources
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
