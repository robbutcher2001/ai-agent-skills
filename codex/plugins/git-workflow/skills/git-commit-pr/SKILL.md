---
name: git-commit-pr
description: Prepare and perform Git commits, pushes, and pull requests using a repository's Commitizen convention and pull request templates. Use when asked to draft or create a commit, choose a branch name, push a branch, or draft/open a PR; do not use for general Git troubleshooting or history rewriting.
---

# Git Commit and PR

Keep the repository's existing workflow authoritative. Inspect its contributor instructions, Git status, staged and unstaged changes, current branch, remote, default branch, Commitizen configuration, and PR template before proposing Git metadata.

## Commit workflow

1. Preserve unrelated user changes. Never stage files indiscriminately; stage only the paths in scope for the requested change.
2. Find the repository's Commitizen configuration in files such as `.cz.toml`, `pyproject.toml`, `.cz.json`, or `package.json`. Follow its configured adapter and project-specific rules. If none exists, use conventional-commit form without adding configuration unless asked.
3. Derive the commit message from the staged diff. Keep the subject concise and imperative, add a scope only when it improves clarity, and include a body or footer when the change needs context or records a breaking change or issue.
4. When Commitizen is installed, validate the proposed message with `cz check --message <message>`. Correct validation failures before committing. Use `python -m commitizen` if that is how the repository provides it.
5. If the user asked only for a draft, return the validated message without changing Git state. If the user explicitly asked to commit, that request authorizes the commit; do not add a redundant confirmation. Otherwise show the proposed message and wait for authorization before committing.

Do not amend, force-push, rebase, reset, or rewrite history unless the user explicitly requests that operation.

## Branch and push workflow

- Follow repository naming rules when present. Otherwise derive a short lowercase hyphenated branch name from the work, prefixed by the Commitizen type when useful, such as `feat/add-device-status`.
- Check whether the remote branch already exists before pushing. Use a normal upstream push for a new branch.
- Push only when explicitly requested. Never force-push from an ordinary commit or PR request.

## Pull request workflow

Read [references/pr-descriptions.md](references/pr-descriptions.md) before drafting or creating a pull request.

Base the title and description on the complete branch diff against the intended base branch, not only the latest commit. Prefer the repository's PR template and preserve its required sections and checklists. Check for issue references supplied by the user or present in branch and commit metadata; do not invent them.

Drafting a PR does not authorize pushing or creating it. Create the PR only when explicitly requested, and report its URL after creation. If creation requires a push, state that dependency and obtain authorization unless the original request already includes pushing or opening the PR.

## Handoff

Report the resulting branch, commit hash and subject, push destination, and PR URL for the actions actually completed. If a requested action could not be completed, give the exact blocker and leave the repository in a recoverable state.
