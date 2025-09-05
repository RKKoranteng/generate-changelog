# generate-changelog
`generate-changelog` is a project that uses a GitHub Actions workflow to automatically generate and maintain a [CHANGELOG.md](CHANGELOG.md) file.

The changelog is rebuilt every time new commits are pushed to the main branch or a release is created.

## How It Works
1. The [workflow](.github/workflows/generate-changelog.yml) runs on:
   - Pushes to the `main` branch
   - Manual dispatch (`workflow_dispatch`)
2. Git history is scanned starting from the most recent version tag (e.g., `v1.2.3`).
3. Commits are filtered into categories based on their prefix:
   - add: → **Added**
   - chg: → **Changed**
   - fix: → **Fixed**
   - del: → **Deleted**
4. A structured CHANGELOG.md is generated (or updated) and pushed back to the repository.


## Getting Started
- Copy the [workflow](.github/workflows/generate-changelog.yml) file into your repository:
  ``` bash
  .github/workflows/generate-changelog.yml
  ```

- Ensure your repository uses annotated tags for versions, e.g.:
  ``` bash 
  git tag v2025.08.1
  git push origin v2025.08.1
  ```

- Push new commits with proper prefixes, e.g.:
  ``` bash
  git commit -m "add: implement user login feature"
  git commit -m "fix: resolve null pointer issue"
  git commit -m "chg: simplify data access layer"
  git commit -m "del: remove deprecated API endpoint"
  ```

- On the next push to `main`, the workflow will:
  - Regenerate `CHANGELOG.md`
  - Commit and push it back automatically