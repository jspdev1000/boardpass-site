# Repository working agreement

## Repository workflow

- The default branch is the authoritative, releasable codebase. Use `main`
  unless this repository still has an explicitly documented `master` exception.
- Do not implement material work directly on the default branch.
- Start work from an up-to-date default branch and use a short-lived
  `feature/*`, `fix/*`, or `chore/*` branch.
- Material changes enter the default branch through a pull request.
- Run the repository's relevant tests, type checks, lint, build, migration
  checks, and deployment validation before merge.
- Do not force-push the default branch, rewrite published release history, or
  silently bypass required checks.

## Releases and rollback

- Every production deployment must be traceable to an exact Git commit.
- Successful production releases should receive an immutable `vX.Y.Z` tag;
  record both the tag and commit SHA and retain the prior known-good release.
- For a serious incident, prefer redeploying the prior known-good release when
  application, schema, storage, webhook, and environment compatibility allow it.
- Never rewrite Git history to simulate rollback. Stabilize production, then
  create a `fix/*` branch and roll forward with a corrected release.
- Treat database rollback separately from code rollback. Prefer
  backward-compatible expand/contract migrations and do not reverse a
  production migration destructively without an application-specific runbook
  and explicit approval.

## Agent safety

- Codex and Hermes may share the canonical clone, but they must not independently
  modify the same working tree at the same time.
- Use a separate branch and Git worktree under `~/Worktrees/` for concurrent
  work. Do not create permanent agent-specific clones.
- Do not prune or remove a worktree until its uncommitted changes, commits,
  stashes, and remote state have been checked for unique work.
- Never expose secrets in logs, prompts, commits, pull requests, or reports.

## Production safety

Agents may inspect production configuration, prepare releases and promotion
commands, validate staging, and document rollback steps. They must not deploy to
production, alter production data or databases, rotate credentials, change DNS,
or perform destructive production operations unless the user explicitly
authorizes that exact action.

