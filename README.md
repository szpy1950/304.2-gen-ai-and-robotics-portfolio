# Duckify Portfolio

Portfolio website for the **304 GenAI & Robotics** semester project at HES-SO Valais-Wallis.

Built with [MkDocs Material](https://squidfunk.github.io/mkdocs-material/). Deployed via GitHub Actions to GitHub Pages.

## Local development

```bash
uv sync
uv run mkdocs serve
```

Open `http://localhost:8000`.

## Build

```bash
uv run mkdocs build
```

Output in `site/`.

## Deploy

Push to `main` — GitHub Actions builds and deploys automatically.

> Enable GitHub Pages in repo Settings → Pages → Source: **GitHub Actions**
