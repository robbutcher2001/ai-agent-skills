# Pull Request Descriptions

Use the repository's pull request template when one exists. Fill it from the actual branch diff and verification results, preserving required headings, comments, and checklist wording.

When there is no template, use only the sections that add information:

```markdown
## Summary

- What changed and why

## Testing

- Command or manual check performed

## Notes

- Migration, rollout, compatibility, or follow-up information
```

Write for a reviewer who has not followed the implementation conversation:

- Explain behavior and motivation rather than narrating files changed.
- Mention meaningful design choices, risks, migrations, and compatibility effects.
- List verification that actually ran. Say `Not run` with a brief reason when applicable; never imply a check passed without evidence.
- Include screenshots or before/after evidence only when available and useful.
- Use closing keywords for issues only when the user intends the PR to close them.
- Keep the title aligned with the repository's convention. When no convention exists, use the validated Commitizen subject without trailing punctuation.
