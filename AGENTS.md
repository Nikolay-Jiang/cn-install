# AGENTS.md

## What this repo is

Mirror of install scripts proxied through `g.blfrp.cn` for users who can't reach GitHub directly. Currently one file: `opencode-install-mirror.sh`.

## Critical gotchas

- **`g.blfrp.cn/api.github.com` returns 403 "Invalid input"** — the proxy does NOT support the API subdomain. Version detection uses HTML scraping from the releases/latest page instead:
  ```bash
  curl -s https://g.blfrp.cn/github.com/anomalyco/opencode/releases/latest | grep -oP '/releases/tag/v\K[0-9]+\.[0-9]+\.[0-9]+' | head -1
  ```
  Do NOT change this back to `api.github.com` JSON API — it will fail.

- **`g.blfrp.cn/github.com` works** — downloads (binary tarballs), HEAD requests (tag verification), and redirects all function through this proxy path.

- **`raw.githubusercontent.com`** is proxied as `g.blfrp.cn/raw.githubusercontent.com` — used in the README curl one-liner, not inside the script itself.

## Editing the mirror script

The script is a modified copy of the upstream at `https://opencode.ai/install`. The ONLY differences should be:

1. GitHub URLs replaced with `g.blfrp.cn` proxy equivalents (4 × `github.com`, 1 × version detection using HTML scrape)
2. Added "Fetching latest version..." progress message and version display

If updating from upstream: re-download, apply the same URL replacements, test that `api.github.com` proxy still doesn't work (it won't), and keep the HTML scrape approach.

## Verification after changes

```bash
bash -n opencode-install-mirror.sh                              # syntax check
grep -c 'g\.blfrp\.cn' opencode-install-mirror.sh                # must be 5
grep 'github\.com' opencode-install-mirror.sh | grep -v 'g\.blfrp\.cn'  # must be 0
```

## Repo setup

```bash
# Remote is github.com/Nikolay-Jiang/cn-install, main branch, HTTPS via gh auth
git remote -v  # origin → https://github.com/Nikolay-Jiang/cn-install.git
```

No build system, no tests, no CI — the script IS the deliverable. Verify by running it.