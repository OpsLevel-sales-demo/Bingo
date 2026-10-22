# Agents

This file provides guidance and guardrails for AI coding agents working in this repository.

## Security and Safety Guidelines

This repository implements Google's OAuth 2.0 authentication library for Ruby. It handles credentials, tokens, service account keys, and other sensitive authentication material. AI coding agents must follow the rules below at all times.

### Protect Sensitive Data

- **Never hardcode secrets.** Do not write API keys, OAuth client secrets, service account key JSON, access tokens, refresh tokens, or any credentials into source files, tests, comments, or documentation.
- **Never log or print credential values.** Do not add debug output, log statements, or test assertions that expose token values, private keys, or other sensitive fields, even partially or truncated.
- **Do not commit real credentials.** Fixtures and test data must use obviously fake or placeholder values (e.g., `"FAKE_KEY"`, `"test-token"`). Never use real Google credentials or PII in tests.
- **Treat environment variables as opaque.** You may reference variable names (e.g., `ENV["GOOGLE_APPLICATION_CREDENTIALS"]`), but never read and re-emit their values into files or stdout.
- **Do not weaken credential handling.** Do not remove or bypass existing validation, expiry checks, or signature verification logic in the authentication flows.

### Prevent Unauthorized Deployments

- **Do not push to production branches.** Do not push directly to `main`, `master`, or any release branch without explicit human approval.
- **Do not trigger releases or publish gems.** Do not run `gem push`, invoke Kokoro release pipelines, bump the gem version in `googleauth.gemspec` or `CHANGELOG.md`, or take any action that could publish a new version to RubyGems.
- **Do not modify CI/CD pipelines to skip checks.** Do not alter `.github/workflows`, `.kokoro/` configurations, or `Rakefile` targets in ways that disable linting, tests, or security gates.

### Avoid Destructive Operations

- **No force pushes.** Do not use `git push --force` or `git push --force-with-lease` under any circumstances.
- **No branch or tag deletion.** Do not delete local or remote branches or tags.
- **No irreversible data operations.** Do not drop or truncate databases, delete cloud resources, or run migrations that cannot be rolled back.
- **No mass file deletion.** Do not bulk-delete source files, test fixtures, or configuration without an explicit instruction scoped to those exact files.
- **Preserve the git history.** Do not run `git rebase`, `git reset --hard`, or any command that rewrites or discards committed history on shared branches.
