# Contributing to Parametron

Thank you for taking the time to contribute.

Parametron is early-stage. Public repositories may expose different parts of the engineering stack at different levels of maturity, so repository-local documentation is the authority for implementation scope.

## Before you start

- Read the repository `README` and any repository-local architecture, specification, or contribution guidance.
- Check existing issues and pull requests before opening a duplicate.
- Keep proposals within the repository's published responsibility boundary.
- Do not implement another repository's responsibility locally just to remove a dependency.

For a substantial change, open or join an issue before investing in implementation.

## Issues

Use the provided issue forms whenever possible.

Organization issue types are used as follows:

- **Bug** — behavior that differs from the documented or tested expectation
- **Feature** — a new user- or system-visible capability
- **Task** — bounded engineering, testing, documentation, refactoring, or maintenance work
- **Phase** — maintainer-owned planning object for a bounded engineering objective

Phase issues coordinate groups of work and are normally created and maintained by project maintainers.

Cross-repository dependencies should link the real blocking and blocked issues rather than duplicating work in multiple repositories.

## Pull requests

Keep pull requests focused and reviewable.

A pull request should:

- explain what changed and why
- stay within the owning repository's responsibility
- link the relevant issue when one exists
- include or update automated tests for behavior changes
- update relevant documentation when contracts or user-visible behavior change
- report the validation commands that were run
- avoid unrelated formatting, generated output, local environment files, or secrets

Use Conventional Commit style for pull request titles where practical, for example:

```text
feat(engine): add deterministic capability
fix(freecad): classify runtime failure
docs: clarify adapter ownership
test(engine): cover malformed input
```

Repository-local instructions take precedence when they are more specific.

## Verification

A change is not complete merely because it builds.

Use the owning repository's normal automated test suite and any focused integration or determinism checks required by the changed boundary. If a required check cannot be run, state that clearly in the pull request.

## Documentation

Stable cross-repository public architecture belongs in the public Parametron documentation. Implementation-specific behavior belongs in the repository that owns it.

Active work state is tracked in GitHub Issues and organization Projects rather than duplicated into documentation.

## Conduct and security

Participation is subject to the [Code of Conduct](CODE_OF_CONDUCT.md).

Do not report security vulnerabilities in public issues. Follow [SECURITY.md](SECURITY.md).
