# About this fork

This is an **unofficial fork** of [higgsfield-ai/skills](https://github.com/higgsfield-ai/skills), the official Higgsfield AI agent skills, maintained by NeuralCube. It is **not affiliated with or endorsed by Higgsfield AI**. The skills, scripts and assets are Higgsfield's work under their MIT license (see `LICENSE`); credit stays with them.

## Why it exists

To install these skills as a plugin that works in both Claude Code and Codex, straight from a repository we control, and to take upstream changes deliberately rather than automatically.

## What differs from upstream

The changes are kept deliberately small so upstream merges stay clean. The skills themselves are unchanged.

| File | Change | Why |
|---|---|---|
| `.claude-plugin/marketplace.json` | `skills` is a list of folder paths instead of a list of objects; a marketplace description is added | Upstream's form fails Claude Code's validator (`plugins.0.skills: Invalid input`, Claude Code 2.1.278), so `/plugin install higgsfield@higgsfield` fails |
| `.agents/plugins/marketplace.json` | Added | Codex needs a marketplace file to install from this repository; upstream ships the Codex plugin manifest (`.codex-plugin/plugin.json`) but no marketplace |
| `FORK.md` | Added | This file |

If a future skill we write ourselves lives here, it goes in its own folder and is listed in both marketplace files; upstream skill folders are never edited.

## Install

Claude Code:

```
claude plugin marketplace add TheNeuralCube/higgsfield-skills
claude plugin install higgsfield@higgsfield
```

Codex:

```
codex plugin marketplace add TheNeuralCube/higgsfield-skills
codex plugin add higgsfield@higgsfield
```

Both use the Higgsfield CLI (`npm i -g @higgsfield/cli`, then `higgsfield auth login`), which bills your own Higgsfield plan credits.

## Taking upstream changes

```
git fetch upstream
git merge upstream/main
```

Resolve any conflict in the two marketplace files by keeping this fork's `skills` form and adding any new skill folder upstream introduced. Then validate with `claude plugin validate .` before pushing.
