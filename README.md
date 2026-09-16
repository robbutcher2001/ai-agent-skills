# ai-agent-skills
Reusable AI agent skills, plugins, and workflow conventions for Codex, Claude, and related coding assistants.

## Repository layout

```text
codex/
|-- .agents/plugins/marketplace.json
`-- plugins/
    `-- git-workflow/
        |-- .codex-plugin/plugin.json
        `-- skills/
            `-- git-commit-pr/
                |-- SKILL.md
                |-- agents/openai.yaml
                `-- references/pr-descriptions.md
```

The `codex/` directory is a self-contained Codex marketplace root. Other agent ecosystems can be added as separate root-level directories later.
