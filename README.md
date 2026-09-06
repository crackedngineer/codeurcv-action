<div align="center">

# rendercv-action

**GitHub Action to generate a professional PDF resume from a YAML config using [RenderCV](https://github.com/rendercv/rendercv).**

[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-rendercv--action-blue?logo=github)](https://github.com/marketplace/actions/rendercv-action)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

</div>

---

## Usage

```yaml
- uses: crackedngineer/rendercv-action@v1
  with:
    config-path: config.yml
    out-dir: output
    filename: john-doe-resume
```

---

## Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `config-path` | ✅ | — | Path to your resume YAML config |
| `out-dir` | ❌ | `output` | Directory to save the generated PDF |
| `filename` | ✅ | - | Override the output PDF filename (without `.pdf`) |
---

## Example Workflow

```yaml
name: Build Resume

on:
  push:
    paths:
      - "config.yml"

permissions:
  contents: write
  packages: read

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: crackedngineer/rendercv-action@v1
        with:
          config-path: config.yml
          out-dir: output
          filename: john-doe-resume

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

- [RenderCV](https://github.com/rendercv/rendercv) — the CLI tool powering this action
- [PyPI](https://pypi.org/project/rendercv/) — install locally to preview before pushing
