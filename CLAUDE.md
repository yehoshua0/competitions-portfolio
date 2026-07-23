# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository purpose

Portfolio aggregator for AI/ML competition entries (Zindi, Kaggle). Root repo contains **no code itself** — each competition lives in its own standalone Git repo, pulled in as submodule under `zindi/` or `kaggle/`. Root holds only:

- `README.md` — portfolio landing page (featured competitions, achievements, "They Talked About Me" press links)
- `certificates/` — competition certificate images (12 files: 10 Zindi, 2 Kaggle)
- `img/` — README assets (header, medal SVGs)
- `.gitmodules` — submodule registry

## Current submodules

- `zindi/togo-fiber-optics-uptake-prediction-challenge`
- `kaggle/the-3lc-cotton-weed-detection-challenge`
- `kaggle/3lc-mvdc`

## Working with submodules

Competition code is **not present** after a plain clone. To inspect or modify a competition:

```bash
# initial clone of all competitions
git submodule update --init --recursive

# update one competition to its latest upstream
git submodule update --remote --merge <path>

# pull a single new competition
git submodule add <repo-url> <kaggle|zindi>/<slug>
```

When editing inside a submodule directory, the working tree belongs to that submodule's repo — commit/push there first, then update the gitlink in this root repo with a separate commit.

## Adding a new competition

1. Create the competition's own GitHub repo following the standard layout documented in `README.md` (`data/`, `notebooks/`, `src/`, `scripts/`, `submissions/`, `README.md`).
2. Add it as a submodule under `kaggle/` or `zindi/` matching the platform.
3. If notable, add a row to the **Featured Competitions** table in root `README.md` and drop the certificate (if earned) in `certificates/` using the naming pattern `<handle>-<challenge-name>.png`.

## Root-level edits

Most root-repo changes are documentation: README updates, new certificate images, medal counts, new "They Talked About Me" entries. No build, lint, or test pipeline at this level — submodules carry their own tooling and `requirements.txt`.

Certificate filenames contain spaces and accented characters (e.g. `Josué`) — quote paths in shell commands and URL-encode nothing in README (relative `<img src>` with spaces works on GitHub).
