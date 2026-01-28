# Repository Guidelines

## Project Structure & Module Organization
- `_config.yml` and `_data/` hold global site settings; update them when you change navigation, scholar IDs, or analytics keys.
- Author pages live in `_pages/`; reuse existing front-matter blocks so URLs, layouts, and sidebars stay aligned.
- Reusable HTML fragments live in `_includes/`, while `_layouts/` defines page skeletons and `_sass/` contains theme styles compiled into `assets/css/`.
- Generated output sits in `_site/` (ignored by Git); manual edits there will be overwritten on the next build.
- `google_scholar_crawler/` contains the GitHub Action helper scripts for citation syncing—edit cautiously and keep it Python 3 compatible.

## Build, Test, and Development Commands
- `bundle install` installs the Ruby toolchain defined in `Gemfile`.
- `bundle exec jekyll serve --livereload` (or `bash run_server.sh`) launches the dev server on http://127.0.0.1:4000 with auto-refresh.
- `bundle exec jekyll build` produces the static site in `_site/`; run this before major PRs to catch build issues.
- Use `JEKYLL_ENV=production bundle exec jekyll build` when you want production-parity asset minification.

## Coding Style & Naming Conventions
- Keep YAML front matter and `_data/*.yml` indented with two spaces; align keys alphabetically when possible for quick diffing.
- Name Markdown files with lowercase kebab-case (e.g., `_pages/publications.md`) so permalinks remain predictable.
- Prefer semantic HTML inside Markdown; use SCSS partials in `_sass` and import them via `@import` in `assets/css/main.scss`.
- When updating includes, document required variables at the top as Liquid comments (`{%- comment -%}`) to help other contributors.

## Testing Guidelines
- After content updates, run `bundle exec jekyll build` and scan the console for Liquid or Markdown warnings.
- Execute `bundle exec jekyll doctor` to surface common misconfigurations (broken permalinks, missing dependencies).
- Spot-check generated pages in `_site/`—especially scholar widgets and assets referenced from `images/`—before pushing.
- If you modify the crawler, run its script locally with a dry run (see `README.md` in `google_scholar_crawler/`) and confirm JSON output structure is unchanged.

## Commit & Pull Request Guidelines
- Recent history shows short lowercase summaries (`update`, `init`); prefer imperative, scoped messages like `feat: add 2025 publications` for clarity.
- Reference related issues in commit bodies when applicable and keep each commit focused on one change set.
- For PRs, include: goal-oriented summary, screenshots or GIFs for UI tweaks, a link to the preview build (if available), and a checklist of manual verifications (`jekyll build`, link checks).
- Request review from a maintainer familiar with the touched area (`_layouts`, styles, crawler, etc.) and wait for green checks before merging.

## Content & Deployment Tips
- Store uploaded assets in `images/` and reference them with site-relative paths (`/images/profile.jpg`) to avoid base URL issues.
- Use draft posts by placing files in `_pages/drafts/` (create if needed) and add `published: false` until ready to go live.
- Configure GitHub Pages to build from the `main` branch with the `github-pages` gem; avoid committing `_site/` because GitHub Pages rebuilds automatically.
