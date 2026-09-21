# Git Workflows

Centralized collection of reusable GitHub Actions workflows used across my projects.

This repository provides shared CI/CD workflows for testing, building, validating, releasing, and deploying projects without duplicating workflow logic across repositories.

## Purpose

The goal of this repository is to maintain a single source of truth for GitHub Actions used throughout my projects.

Project repositories only define when a workflow should run and provide project-specific configuration. The actual CI/CD logic is maintained here.

```text
Project Repository
       │
       ├── Pull Request
       ├── Push
       └── Release
              │
              ▼
        Git Workflows
              │
       ┌──────┼──────┐
       ▼      ▼      ▼
     Tests   Build  Release
```

## Workflows

### Unity

Reusable workflows dedicated to Unity projects.

* Unity automated tests
* Unity builds
* GameCI integration

### .NET

Reusable workflows for C# and .NET projects.

* Build
* Tests
* Publish

### Release

Common release workflows used across multiple project types.

* GitHub Releases
* Build artifacts
* Versioned releases

### Deployment

Deployment workflows for external platforms.

Planned integrations include:

* itch.io deployment using Butler

## Usage

Workflows from this repository can be called from another repository using GitHub reusable workflows.

Example:

```yaml
jobs:
  tests:
    uses: <username>/git-workflows/.github/workflows/unity-tests.yml@main
    secrets: inherit
```

Project-specific workflows remain responsible for triggers:

```yaml
on:
  pull_request:
    branches:
      - main
      - dev
```

The reusable workflow contains the actual implementation.

## Versioning

Reusable workflows may be referenced using a specific version to prevent changes from unexpectedly affecting existing projects.

```yaml
uses: <username>/git-workflows/.github/workflows/unity-tests.yml@v1
```

During development, workflows may reference the `main` branch.

## Repository Structure

```text
.github/
└── workflows/
    ├── unity-tests.yml
    ├── unity-build.yml
    ├── dotnet-build.yml
    ├── release.yml
    └── itch-deploy.yml
```

Additional workflows will be added as the CI/CD infrastructure evolves.
