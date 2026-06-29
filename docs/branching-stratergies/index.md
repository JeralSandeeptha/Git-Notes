## Branching Stratergies

- Branching Strategy depends on team's `workflow`, `project type`, `deployment process`.

- Team size: 
    - Smaller teams might prefer `GitHub Flow` or `Trunk-Based Development`, while larger teams may opt for `Git Flow`.

- Deployment frequency: 
    - Continuous deployment favors lightweight strategies like `GitHub Flow`.

- Project complexity: 
    - Complex projects with long-lived features benefit from `Git Flow` or `Release Branching`.

### Git Flow

![Git Flow Diagram](https://wac-cdn.atlassian.com/dam/jcr:cc0b526e-adb7-4d45-874e-9bcea9898b4a/04%20Hotfix%20branches.svg?cdnVersion=2757)

#### Description
A robust strategy with dedicated branches for feature development, releases, and hotfixes.

#### Branches

- **main / master** – Latest production-ready code.
- **develop/** – Integrates new features for the next release.
- **feature/** – For individual features.
- **release/** – For stabilising code before a production release.
- **hotfix/** – For quick fixes on the production code.

#### Usage
Suitable for large projects with scheduled releases.

### GitHub Flow

![GitHub Flow Diagram](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748952160/6194709048910268704_sht6gj.jpg)

#### Description
A simplified, lightweight strategy for continuous delivery.

#### Branches

- **main / master** – Latest production-ready code.
- **feature/** – Short-lived branches for new features or bug fixes.

#### Workflow

1. Create a feature branch from `main`.
2. Work on the feature and push updates.
3. Open a pull request (PR) for code review.
4. Merge the PR into `main` and deploy immediately if necessary.

#### Usage
Ideal for small teams and projects with continuous integration and delivery (CI/CD).

### GitLab Flow

![GitLab Flow Diagram](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748952183/6194709048910268705_ltitoo.jpg)

#### Description
A flexible strategy for managing development, staging, and production environments.

#### Branches

- **main / master** – Latest production-ready code.
- **development/** – For ongoing development work.
- **feature/** – For experimental work, merged quickly.
- **environment/** – For managing code in specific environments (e.g., staging, QA, production).

#### Workflow

1. Create a `feature/*` branch for new work.
2. Merge feature branches directly into the appropriate `environment/*` branch.
3. Use merge requests (MRs) for reviews and approvals before merging.
4. Merge from environment branches into `main` for production release when ready.

#### Usage
Works well for projects with multiple deployment environments.

### Trunk-Based Development

![Trunk-Based Development](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748952189/6194709048910268706_cm4rr4.jpg)

#### Description
A minimalist strategy where developers work on a single branch.

#### Branches

- **main / master** – Latest production-ready code.
- **feature/feature-01** – For experimental work, but merged quickly.

#### Workflow

1. Commit changes frequently to `main`.
2. Keep branches short-lived and merge quickly.
3. Use feature flags to deploy incomplete or experimental features safely.

#### Usage
Suitable for fast-moving teams using CI/CD practices.

### Feature Branching

![Feature Branching Diagram](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748952080/6194709048910268703_rsk2ww.jpg)

#### Description
Every feature or bug fix is developed in its own branch.

#### Branches

- **main / master** – Production-ready code.
- **feature/awesome-feature** – For a single feature or bug fix.

#### Workflow

1. Create a branch for a specific feature.
2. Work on the branch until the feature is complete.
3. Merge it back into `main` (or another integration branch).

#### Usage
Suitable for teams working on independent features.

### Forking Workflow

![Forking Workflow Diagram](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748953081/8412cc98-67ce-4399-acab-360484c69620_udzcd1.png)

#### Description
Used in open-source projects where contributors work on their own fork of the repository.

#### Workflow

1. Fork the main repository.
2. Create a branch in your fork for the feature or bug fix.
3. Work on the branch and commit your changes.
4. Submit a pull request to the main repository for review.

#### Usage
Ideal for open-source collaboration.

<br /><br />