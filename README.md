# Codex Optimization Guide

Codex usage notes, reusable prompts, and configuration templates for making local Codex workflows easier to reproduce.

## Contents

- `docs/` - task-specific guides and operational notes
- `prompts/` - full prompts that can be copied into Codex
- `templates/` - reusable config snippets

## Current Guides

- [Use a relay API key with Codex](docs/codex-relay-api-key.md)

## Principles

- Keep configuration changes explicit and reversible.
- Keep API keys out of `auth.json` when using a relay provider.
- Prefer complete prompts with concrete target files, expected output, and validation steps.
- Preserve unrelated Codex config when editing `~/.codex/config.toml`.

## Quick Start

Copy the prompt in [prompts/configure-relay-api-key.md](prompts/configure-relay-api-key.md), replace:

- `https://替换为中转站地址`
- `sk-替换为中转站apikey`

Then run it in a Codex session that has local filesystem access.
