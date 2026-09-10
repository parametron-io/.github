# Repository Launch Checklist

Use this checklist when creating or publishing a repository under the `parametron-io` organization.

The goal is to make repository launches repeatable, contributor-friendly, and consistent with organization-wide GitHub policy without duplicating live project state in documentation.

## 1. Define the repository boundary

- [ ] Repository name follows the `parametron-<component>` convention where applicable.
- [ ] The repository has one clear responsibility and does not absorb another repository's role.
- [ ] Public scope is explicitly defined before publication.
- [ ] Unpublished product strategy, future commercial architecture, and private planning are excluded from the public repository.
- [ ] The license has been chosen deliberately for this repository and is documented in a repository-local `LICENSE` file.
- [ ] Public documentation and implementation-specific documentation have clear ownership.

## 2. Audit content and history before publication

For any repository with pre-existing local history:

- [ ] Worktree is clean before the publication audit.
- [ ] Reachable branches and tags have been reviewed.
- [ ] Commit author identities are appropriate for public history.
- [ ] No secrets, credentials, private keys, tokens, internal-only URLs, private infrastructure details, or sensitive files are present.
- [ ] No unpublished Parametron strategy or future-product blueprint is present in reachable public history.
- [ ] Old hosting references are either current, intentionally historical, or removed.
- [ ] Submodules, Git LFS pointers, generated files, and large binary assets are intentional.
- [ ] If the existing history cannot be made confidently public-safe, publish a fresh clean history instead of exposing the old history.

## 3. Create the GitHub repository

- [ ] Repository is created under `parametron-io`.
- [ ] Visibility is explicitly chosen: public or private.
- [ ] Default branch is `main`.
- [ ] Description is concise and reflects current public scope.
- [ ] Homepage URL is set when a stable public destination exists.
- [ ] Topics are added only when they accurately describe the current repository.
- [ ] Repository is not configured as a template unless it is intentionally reusable as one.

For a repository that already has a prepared local history, prefer creating the GitHub repository without starter files and push the reviewed history afterward.

## 4. Confirm organization defaults

New repositories should inherit the organization baseline where applicable.

### Issue types

- `Task`
- `Bug`
- `Feature`
- `Phase`

`Phase` is a maintainer-owned bounded engineering objective that groups related work and exit criteria.

### Issue fields

- `Priority` — all issue types
- `Effort` — Task, Bug, and Feature
- `Start date` — Phase only
- `Target date` — Phase only

### Default labels

- `documentation`
- `good first issue`
- `help wanted`
- `external`
- `needs-triage`
- `dependencies`
- `regression`
- `breaking-change`

Do not recreate issue type, priority, effort, phase, repository, or project status as labels.

## 5. Community health files

Organization-wide defaults live in `parametron-io/.github`.

Unless a repository genuinely needs an override, do not duplicate:

- `CONTRIBUTING.md`
- `CODE_OF_CONDUCT.md`
- `SECURITY.md`
- `SUPPORT.md`
- default issue forms
- default pull request template

If a repository provides its own version, it must be intentionally more specific and remain compatible with the organization-wide policy.

## 6. Repository features

Recommended defaults:

- [ ] Issues enabled for public engineering repositories.
- [ ] Wiki disabled unless there is a specific reason to use it; normal documentation belongs in version-controlled docs.
- [ ] Discussions disabled initially and enabled later only when a repository has enough community traffic to justify a discussion channel.
- [ ] Repository-specific Projects are not used for normal engineering coordination; organization-wide work belongs in `Parametron Engineering`.
- [ ] Releases are used only after the repository has an explicit versioning and release process.

## 7. Merge policy

Recommended merge configuration:

- [ ] Squash merge enabled.
- [ ] Rebase merge enabled.
- [ ] Merge commits disabled.
- [ ] Pull request titles follow Conventional Commit style where practical.
- [ ] Squash commit titles preserve the pull request title so the main history remains readable.
- [ ] Automatically delete head branches after merge when appropriate.
- [ ] Auto-merge may be enabled once required checks and review rules are stable.

Use squash merge for noisy or externally contributed histories. Use rebase merge when preserving a clean, intentionally curated commit series adds value.

## 8. Protect `main`

Create a repository ruleset or equivalent branch protection for `main`.

Baseline:

- [ ] Require a pull request before merging.
- [ ] Required approvals: `0` while there is only one maintainer.
- [ ] Increase required approvals to `1` when a second independent maintainer is available.
- [ ] Require conversation resolution before merge.
- [ ] Require linear history.
- [ ] Block force pushes.
- [ ] Block branch deletion.
- [ ] Require repository CI checks after the checks exist and their names are stable.
- [ ] Do not require signed commits unless the organization deliberately adopts that policy later.
- [ ] Keep an owner/admin emergency bypass only if needed; normal development should still use pull requests.

Do not configure a required status check before the corresponding workflow has run successfully at least once.

## 9. GitHub Actions and CI

- [ ] CI exists before the repository is considered contributor-ready.
- [ ] Workflow permissions use the minimum required access.
- [ ] Workflows default to read access unless a specific job needs write permission.
- [ ] Workflows do not expose organization or repository secrets to untrusted pull requests.
- [ ] Fork pull-request workflow policy is reviewed before accepting external contributions.
- [ ] Third-party Actions are reviewed and pinned appropriately for the repository's security requirements.
- [ ] Expensive jobs use reasonable path filters, caching, or concurrency controls where useful.
- [ ] Repository-local verification commands are documented.

Typical repository-specific checks may include tests, linting, static analysis, formatting checks, integration tests, or deterministic repeatability proofs.

## 10. Confirm security configuration

For a new public repository:

- [ ] `Parametron Public Baseline` is applied.
- [ ] The configuration is enforced by the organization where expected.
- [ ] Secret scanning alerts are enabled.
- [ ] Push protection is enabled.
- [ ] Code scanning default setup is enabled where supported.
- [ ] Dependency graph is enabled.
- [ ] Dependabot alerts are enabled.
- [ ] Dependabot security updates are enabled.
- [ ] Malware alerts are enabled where available.
- [ ] Private vulnerability reporting is enabled.

Normal dependency version updates are repository-specific and should be configured deliberately rather than assumed from the security baseline.

Private repositories may use a different security policy depending on available GitHub features and repository purpose.

## 11. Add the repository to the engineering workflow

Live work is coordinated in the organization-level `Parametron Engineering` Project.

- [ ] Create or identify the repository's current `Phase` issue when active engineering work exists.
- [ ] Phase issue contains goal, scope, non-goals, dependencies, exit criteria, and verification expectations.
- [ ] Set `Priority` for the Phase.
- [ ] Set `Start date` and `Target date` when useful for roadmap planning.
- [ ] Add the Phase issue to `Parametron Engineering`.
- [ ] Represent implementation work as Task, Feature, or Bug sub-issues.
- [ ] Let the Project's sub-issue workflow add Phase sub-issues automatically.
- [ ] Cross-repository blockers use GitHub's blocking relationship as the source of truth and the `external` label as the visible cross-repository signal.

Project status model:

`Backlog -> Ready -> In Progress -> In Review -> Blocked -> Done`

The Project is the source of truth for live coordination. Do not duplicate changing status into central roadmap documents.

## 12. Pull request workflow

Recommended issue-to-PR lifecycle:

1. Work item is sufficiently defined and moves to `Ready`.
2. Work begins and moves to `In Progress`.
3. A linked pull request keeps the work in `In Progress`.
4. When the pull request is ready for human review, move it to `In Review`.
5. Requested code changes return active work to `In Progress`.
6. Approval keeps the item in `In Review` until merge.
7. Merge or issue closure moves the item to `Done`.
8. Reopened work returns to `Ready`.

Prefer linking the closing relationship in the pull request description:

```text
Closes #123
```

## 13. Documentation readiness

- [ ] `README` explains what the repository currently is, not speculative future architecture.
- [ ] Setup/build/test instructions work from a fresh checkout.
- [ ] Public contracts and behavior are documented at the correct ownership level.
- [ ] Stable cross-repository documentation links to the public Parametron documentation when appropriate.
- [ ] Implementation-local details stay with the owning repository.
- [ ] Live Project status is not duplicated into documentation.
- [ ] All relative documentation links resolve.

## 14. Final launch verification

Before announcing or linking the repository publicly:

- [ ] Clone the public GitHub repository into a fresh directory.
- [ ] Confirm the expected default branch and remote.
- [ ] Confirm the visible history contains only intended public commits and refs.
- [ ] Confirm the license is detected correctly by GitHub.
- [ ] Confirm issue forms render without schema errors.
- [ ] Confirm inherited community files are visible where expected.
- [ ] Confirm labels and organization issue types/fields are available.
- [ ] Confirm `Parametron Public Baseline` security configuration is applied for public repositories.
- [ ] Confirm CI runs successfully on a pull request.
- [ ] Confirm `main` protection/ruleset blocks unintended direct changes according to policy.
- [ ] Confirm the repository can be added to and coordinated through `Parametron Engineering`.
- [ ] Review the public repository as an unauthenticated visitor where practical.

## 15. Launch complete

A repository is ready for normal public contribution when:

- its current scope is understandable without private context
- its public history is intentional
- its license is explicit
- organization community defaults apply correctly
- CI and security checks are active
- `main` is protected
- work is represented through GitHub Issues and the organization Project
- no unpublished strategy is required to understand or contribute to the public surface
