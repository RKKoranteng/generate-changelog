# generate-changelog
This repository uses a GitHub Actions workflow to automatically generate and maintain a [CHANGELOG.md](CHANGELOG.md) file.
The changelog is rebuilt every time new commits are pushed to the main branch or a release is created.

## 🚀 Features
- Generates a `CHANGELOG.md` file at the root of the repo.
- Includes a fixed header with project attribution and [Calendar Versioning](https://calver.org/) reference.
- Groups commits under sections:
  - Added (add)
  - Changed (ref)
  - Fixed (fix)
  - Deleted (del)
- Shows each commit as:
  ```
  YYYY-MM-DD : commit message (author)
  ```
- Skips merge commits and ignores the workflow’s own auto-commits (docs: update CHANGELOG [skip ci]).
- Updates `CHANGELOG.md` automatically and commits it back to the repository.

## ⚙️ How It Works
1. The workflow runs on:
   - Pushes to the `main` branch
   - Manual dispatch (`workflow_dispatch`)
   - New releases (`release: created`)
2. Git history is scanned starting from the most recent version tag (e.g., `v1.2.3`).
3. Commits are filtered into categories based on their prefix:
   - add: → **Added**
   - chg: → **Changed**
   - fix: → **Fixed**
   - del: → **Deleted**
4. A structured CHANGELOG.md is generated (or updated) and pushed back to the repository.

## 📂 File 
- `.github/workflows/generate-changelog.yml` <br>
The workflow definition that runs the changelog generator.

- `CHANGELOG.md` <br>
The generated changelog file, updated automatically.

## Getting Started
- Create a tag using [CalVer](https://calver.org/) versioning format. Example `git tag -a v2025.08.1 -m "August release 1"`
- Push tag to remote server. Example `git push origin v2025.08.1`