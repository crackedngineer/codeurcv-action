<div align="center">

# codeurcv-action

**GitHub Action to generate a professional PDF resume from a YAML or JSON config.**

[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-codeurcv--action-blue?logo=github)](https://github.com/marketplace/actions/codeurcv-action)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

</div>

---

## Usage

```yaml
- uses: crackedngineer/codeurcv-action@v1
  with:
    file-name: resume.yml
    out-dir: output
```

---

## Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `file-name` | ✅ | — | Path to your resume YAML or JSON config |
| `out-dir` | ❌ | `output` | Directory to save the generated PDF |

---

## Example Workflow

```yaml
name: Build Resume

on:
  push:
    paths:
      - "resume.yml"

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: crackedngineer/codeurcv-action@v1
        with:
          file-name: resume.yml
          out-dir: output

      - name: Commit generated PDF
        run: |
          git config user.name "github-actions[bot]"
          git config user.email "github-actions[bot]@users.noreply.github.com"
          git add output/
          git commit -m "chore: update resume" || echo "No changes to commit"
          git push
```

---

## Related

- [codeurcv](https://github.com/crackedngineer/code-ur-cv) — the CLI tool powering this action
- [PyPI](https://pypi.org/project/codeurcv/) — install locally to preview before pushing
