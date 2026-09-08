# Template Repository

A starter template for creating new GitHub repositories pre-configured with agent instructions and automated pull request reviews.

## Included Files

- **[`AGENTS.md`](AGENTS.md)** — Canonical instructions and guidelines for AI coding agents.
- **[`ANTIGRAVITY.md`](ANTIGRAVITY.md)** — Quick reference of commonly used Antigravity slash commands.
- **[`CLAUDE.md`](CLAUDE.md)** — Points Claude Code to `AGENTS.md`.
- **[`.github/workflows/jules-pr-review.yml`](.github/workflows/jules-pr-review.yml)** — Automated code review on pull request open and update events using Jules PR Reviewer.

## Repository Setup & Security Hardening

After creating a new repository from this template, you must configure the following settings:

### 1. Remove Dormant Workflow and Subscribe to Updates

The template includes a `sync-agents.yml` workflow that only runs in the template repository itself. Delete it from your new repository:

```bash
git rm .github/workflows/sync-agents.yml
git commit -m "chore: remove dormant sync-agents workflow"
git push
```

To receive future `AGENTS.md` updates as automated PRs, add your repository to [`subscribers.txt`](https://github.com/ianbunag/template/blob/main/subscribers.txt) in the template repository (see the [workflows README](.github/workflows/README.md) for details).

### 2. Repository Secrets

Navigate to **Settings > Security and quality> Secrets and variables > Actions > Repository secrets**:

- Add `JULES_API_KEY` to enable automatic AI code reviews on pull requests.

## Optional Security Hardening

You can optionally configure the following settings:

### 1. Actions Permissions

Navigate to **Settings > Code, planning, and automation > Actions > General > Actions permissions**:

- Select **Allow (organization), and select non-(organization), actions and reusable workflows**
- Check **Allow actions created by GitHub**
- Check **Allow actions by Marketplace verified creators**
- Check **Require actions to be pinned to a full-length commit SHA**
- Click Save

### 2. Advanced Security

Navigate to **Settings > Security and quality> Advanced Security**:

#### Dependency Graph
- Enable **Dependency graph**
- Enable **Automatic dependency submission**

#### Dependabot
- Enable **Dependabot alerts**
- Enable **Dependabot malware alerts**
- Enable **Dependabot security updates**
- Enable **Grouped security updates**

#### Code Scanning
- Set up **CodeQL analysis**
