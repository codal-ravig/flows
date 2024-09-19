# Branching Strategy

This repository follows a Gitflow-based branching model to manage development, QA, UAT, and production releases.

## Main Branches
- **`main`**: Production-ready code lives here. All releases are tagged and deployed from this branch.
- **`develop`**: Active development happens here. All feature branches merge into this branch for integration.

## Environment-Specific Branches
- **`qa`**: 
  - Created from `develop` after features are integrated.
  - Used for Quality Assurance testing.
- **`uat`**: 
  - Created from `qa` after successful QA testing.
  - Used for User Acceptance Testing (UAT) by stakeholders.
- **`release/X.X.X`**: 
  - Created from `uat` once UAT is approved.
  - Used for final preparations (e.g., bug fixes, documentation) before merging into `main`.

## Feature Branches
- **`feature/branch-name`**: 
  - Every new feature or bug fix gets its own branch.
  - Branches off from `develop` and merges back into `develop` after code review and testing.

## Hotfix Branches
- **`hotfix/X.X.X`**: 
  - Created from `main` for urgent production fixes.
  - Merged into both `main` and `develop` after the fix is applied.

## Flow Summary

1. **New Feature Development**
   - Create a `feature/branch-name` branch from `develop`.
   - After completing the feature, merge it back into `develop`.

2. **QA Testing**
   - Create a `qa` branch from `develop` for testing.
   - Fix any issues found and merge back into `develop`.

3. **UAT Testing**
   - Create a `uat` branch from `qa` after QA passes.
   - Conduct UAT and gather business approval.

4. **Release Preparation**
   - Create a `release/X.X.X` branch from `uat` after UAT passes.
   - Perform final preparations and testing.
   - Merge `release` into `main` for production.

5. **Hotfix Process**
   - Create a `hotfix/X.X.X` branch from `main` to apply urgent production fixes.
   - Merge the hotfix into both `main` and `develop` to ensure consistency.

## Commands Example

### Hotfix Flow

```bash
# Start a hotfix from `main`
git checkout main
git checkout -b hotfix/1.0.1

# Apply the fix and commit
git commit -m "Fix critical production bug"

# Merge back into `main` and tag
git checkout main
git merge hotfix/1.0.1
git tag -a 1.0.1 -m "Version 1.0.1"

# Merge into `develop` to keep it up to date
git checkout develop
git merge hotfix/1.0.1

# Push changes
git push origin main develop

```
```bash
# Create a release branch from UAT
git checkout uat
git checkout -b release/1.1.0

# Prepare release, test, and finalize
git commit -m "Prepare version 1.1.0 release"

# Merge into `main` and tag the release
git checkout main
git merge release/1.1.0
git tag -a 1.1.0 -m "Version 1.1.0"

# Merge back into `develop` to keep it updated
git checkout develop
git merge release/1.1.0

# Push changes
git push origin main develop

