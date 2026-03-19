
## Auto Publish to Overleaf (GitHub Actions)

This repo includes a workflow at `.github/workflows/overleaf-sync.yml`.
It automatically syncs project source files to Overleaf when code is pushed to `main`.

### 1) Enable Overleaf Git bridge

In your Overleaf project:

1. Open **Menu** -> **Git**
2. Copy your project Git URL (format similar to `https://git.overleaf.com/<project_id>`)

### 2) Add GitHub repository secrets

Go to GitHub repository -> **Settings** -> **Secrets and variables** -> **Actions** -> **New repository secret**.

Add the following secrets:

- `OVERLEAF_GIT_URL`: Overleaf Git URL (for example `https://git.overleaf.com/<project_id>`)
- `OVERLEAF_USERNAME`: your Overleaf account email
- `OVERLEAF_GIT_TOKEN`: your Overleaf **general token** (recommended)

Optional backward-compatible secret:

- `OVERLEAF_PASSWORD`: legacy name, used only if `OVERLEAF_GIT_TOKEN` is not set

> If you sign in with Google, use your Overleaf Git/general token here (do **not** use your Google password).

### 3) Trigger sync

- Automatic: push to `main`
- Manual: run workflow **Sync to Overleaf** from the Actions tab

By default, automatic sync only runs when these paths change: `main.tex`, `references.bib`, `image/**`, or the workflow file itself.

### 4) Default behavior

The workflow excludes build artifacts (`*.aux`, `*.log`, `*.pdf`, etc.), `.git`, `.github`, and `Showcase/` before pushing to Overleaf.

> If your Overleaf project uses a branch other than `master`, update `HEAD:master` in `.github/workflows/overleaf-sync.yml`.
