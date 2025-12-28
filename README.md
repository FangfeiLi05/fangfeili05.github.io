# fangfeili05.github.io — Personal Website

This repository contains the source code for my personal website:
[**https://fangfeili05.github.io**](https://fangfeili05.github.io).

The site is built with [**Hugo**](https://github.com/gohugoio/hugo) using the [**Congo**](https://github.com/jpanther/congo) theme and deployed via **GitHub Pages** with with **GitHub Actions**.

---

## Tech Stack

- **Hugo (extended)** - static site generator
- **Congo** - Hugo theme
- **TailwindCSS** - custom styling
- **Markdown** - content authoring
- **GitHub Pages + GitHub Actions** - automated deployment

## Project Structure

```text
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
│   ├── resume/                 # /resume/
│   ├── papers/                 # /papers/
│   ├── certifications/         # /certifications/
│   └── notes/                  # /notes/
│
├── layouts/                    # Custom templates and overrides
│
├── assets/                     # Assets processed by Hugo Pipes
│   ├── img/
│   └── css/
│
└── static/                     # Static files served from the site root
    └── files/                  # Downloadable resources
```

## License

- **Source code:** [`MIT License`](LICENSE.md)
- **Content:** [`CC BY 4.0`](https://creativecommons.org/licenses/by/4.0/) (unless stated otherwise)

## Setup Guide

- For a detailed walkthrough on building and deploying this site with Hugo and the Congo theme, see: [This link](https://fangfeili05.github.io/notes/4_hugo_congo_static_site_build_workflow/)