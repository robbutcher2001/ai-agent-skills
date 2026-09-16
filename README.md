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

## Install from GitHub

Install the marketplace and Git workflow plugin without cloning this repository:

```sh
codex plugin marketplace add robbutcher2001/ai-agent-skills --ref main --sparse codex
codex plugin add git-workflow@robbutcher-skills
```

Start a new Codex conversation after installation so the bundled skill is discovered.
