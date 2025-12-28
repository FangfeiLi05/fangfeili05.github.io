# fangfeili05.github.io — Personal Website (Source Code)

This repository contains the source code for my personal website:
[**https://fangfeili05.github.io**](https://fangfeili05.github.io).

The site is built with [**Hugo**](https://github.com/gohugoio/hugo) using the [**Congo**](https://github.com/jpanther/congo) theme and deployed via **GitHub Pages**.

---

## Tech Stack

- **Hugo** (extended) - static site generator
- **Congo** - theme
- **TailwindCSS** - custom styling
- **Markdown** - content
- **GitHub Pages + GitHub Actions** - deployment

## Project Structure

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

## License

- **Source code:** [`MIT License`](LICENSE.md)
- **Content:** [`CC BY 4.0`](https://creativecommons.org/licenses/by/4.0/) (unless stated otherwise)

## Setup Guide
