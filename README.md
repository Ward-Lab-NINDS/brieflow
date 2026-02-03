# Brieflow

## INTERNAL NOTES

Forked from cheesemanlab/brieflow for active development for Ward Lab (NINDS) OPS data.

Each developer should **clone** this codebase to their machine - ensure you clone `Ward-Lab-NINDS/brieflow`. This is essential to maintain commit history when merging branches into _main_ branch of the fork.

### Branch Overview

This repository follows the [Git-Flow Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) to maintain compatibility with upstream brieflow updates and provide clear traceability to each developer's contributions.

#### Branch Structure

| Branch Type | Naming Convention | Branches From | Merges Into | Purpose |
|-------------|-------------------|---------------|-------------|---------|
| **main** | `main` | — | — | Production-ready releases only. Tagged with version numbers. |
| **develop** | `develop` | `main` | `main` | Shared integration branch for all developers. Contains completed features awaiting release. |
| **feature** | `feat/<description>` | `develop` | `develop` | Individual developer work on new features or changes. |
| **release** | `release/<version>` | `develop` | `main` and `develop` | Preparation for a new production release (bug fixes, docs, release tasks only). |
| **hotfix** | `hotfix/<description>` | `main` | `main` and `develop` | Urgent fixes for production issues. The **only** branch that forks directly from `main`. |

#### Workflow Overview

```
main ────●─────────────────────────●────────────●─────── (tagged releases)
         │                         ↑            ↑
         │                  release/v1.0    hotfix/urgent-fix
         │                    ↑    │            │
         ↓                    │    ↓            ↓
develop ─●────●────●──────────●────●────────────●─────── (integration)
              │    │          ↑
              ↓    ↓          │
           feat/A feat/B ─────┘
```

#### Feature Branch Workflow

1. **Create a feature branch** from `develop`:
   ```bash
   git checkout develop
   git pull origin develop
   git checkout -b feat/<brief-description>
   ```

2. **Develop and commit** your changes on the feature branch:
   ```bash
   git add <files>
   git commit -m "descriptive commit message"
   git push origin feat/<brief-description>
   ```

3. **Open a Pull Request** to merge into `develop` when your feature is complete and tested. **Claire or Pratik** will manage the PR review and merge.

4. **Delete the feature branch** after merging.

#### Release Branch Workflow

When `develop` has acquired enough features for a release (or a predetermined release/publication date is approaching), **Claire or Pratik** will:

1. **Create a release branch** from `develop`:
   ```bash
   git checkout develop
   git pull origin develop
   git checkout -b release/<version>
   ```

2. **Only release-oriented work** goes into this branch — bug fixes, documentation, and release preparation. **No new features.**

3. **Merge into `main`** when ready to ship:
   ```bash
   git checkout main
   git merge release/<version>
   git tag -a v<version> -m "Release v<version>"
   ```

4. **Merge back into `develop`** to capture any fixes made during release prep:
   ```bash
   git checkout develop
   git merge release/<version>
   ```

5. **Delete the release branch**.

Using a dedicated release branch allows one dev to polish the current release while another continues working on features for the next release. It creates well-defined phases of development (e.g., "This week we're preparing for version 4.0").

#### Hotfix Branch Workflow

For urgent production issues that cannot wait for the next release cycle:

1. **Create a hotfix branch** from `main` (the **only** branch that forks directly _from_ `main`):
   ```bash
   git checkout main
   git pull origin main
   git checkout -b hotfix/<description>
   ```

2. **Fix the issue** and commit.

3. **Merge into `main`** and tag:
   ```bash
   git checkout main
   git merge hotfix/<description>
   git tag -a v<version> -m "Hotfix v<version>"
   ```

4. **Merge into `develop`** (or current release branch if one exists):
   ```bash
   git checkout develop
   git merge hotfix/<description>
   ```

5. **Delete the hotfix branch**.

Hotfix branches let the team address critical issues without interrupting the rest of the workflow or waiting for the next release cycle.

#### Guidelines

- **Never commit directly to `main`** — all changes must go through the appropriate branch and PR process.
- **Feature branches merge to `develop`**, not `main`.
- **Only hotfix branches fork from `main`** — everything else branches from `develop`.
- **Release and hotfix branches merge into both `main` AND `develop`** to ensure fixes are available to ongoing work.
- **Keep feature branches focused** — one feature or fix per branch.
- **Test thoroughly** before opening a PR.
- **Delete branches** after merging to keep the repository clean.
- **Sync with upstream** periodically to incorporate updates from `cheeseman-lab/brieflow`.


![GitFlow Workflow](images/gitflow.png)

---

[![Release](https://img.shields.io/github/v/release/cheeseman-lab/brieflow)](https://github.com/cheeseman-lab/brieflow/releases)
[![Python](https://img.shields.io/badge/python-3.11-blue)](https://www.python.org/downloads/)
[![Documentation](https://img.shields.io/badge/docs-brieflow.readthedocs.io-brightgreen)](https://brieflow.readthedocs.io)
[![Tests](https://github.com/cheeseman-lab/brieflow/actions/workflows/test_analysis.yml/badge.svg)](https://github.com/cheeseman-lab/brieflow/actions/workflows/test_analysis.yml)
[![Discord](https://img.shields.io/badge/forum-discord-7289da)](https://discord.gg/yrEh6GP8JJ)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![bioRxiv](https://img.shields.io/badge/bioRxiv-10.1101%2F2025.05.26.656231-b31b1b)](https://doi.org/10.1101/2025.05.26.656231)

![Brieflow pipeline](images/brieflow_info.png)

Brieflow is an extensible computational pipeline for high-throughput analysis of optical pooled screening data.

This repo contains the source code for running an OPS screen analysis.
[Brieflow Analysis](https://github.com/cheeseman-lab/brieflow-analysis) contains configuration notebooks/files and execution scripts for running an OPS screen analysis.

## Getting Started

We strongly suggest that Brieflow is set up with the companion [Brieflow Analysis](https://github.com/cheeseman-lab/brieflow-analysis) repository.

Full details on setup, installation, test data, usage, module details, and contribution guides:  
**https://brieflow.readthedocs.io**

## Citing Brieflow

Brieflow was created by [Matteo Di Bernardo](https://github.com/mat10d), [Roshan Kern](https://github.com/roshankern), and others in the [Cheeseman Lab](https://cheesemanlab.wi.mit.edu/).
Brieflow was started in 2024 and is actively being developed.
If you are interested in contributing please reach out!

If you use our code please cite this manuscript:

```
@ARTICLE
author={Di Bernardo, Matteo and Kern, Roshan S. and Mallar, Apratim and Nutter-Upham, Adrienne and Blainey, Paul C. and Cheeseman, Iain},
title={Brieflow: An Integrated Computational Pipeline for High-Throughput Analysis of Optical Pooled Screening Data},
year={2025},
DOI={10.1101/2025.05.26.656231}
```

## Contributing

We welcome community contributions to Brieflow. Optical pooled screens vary between labs and we would love to add and share approaches that you have taken to your data such that the community can make use of this!

Feel free to:
- Giving the repo star to boost Brieflow's visibility!
- Join Brieflow's [Discord](https://discord.gg/yrEh6GP8JJ) to chat with the developers.
- File a [GitHub issue](https://github.com/cheeseman-lab/brieflow/issues) to share comments and issues.
- Clone the repository, create a new branch, and submit a [pull request](https://github.com/cheeseman-lab/brieflow/compare) as detailed in the [pull request template](.github/pull_request_template.md).

Make sure to review the Brieflow [development guide](https://brieflow.readthedocs.io/en/latest/4.development.html) to understand how to best contribute!

