# Codex Optimization Guide

English | [中文](#中文)

Reusable prompts, configuration templates, and workflow notes for improving local Codex usage.

## Contents

- `docs/` - task-specific guides and operational notes
- `prompts/` - complete prompts that can be copied into Codex
- `templates/` - reusable configuration snippets

## Current Guides

- [Use a relay API key with Codex](docs/codex-relay-api-key.md)

## Principles

- Keep configuration changes explicit and reversible.
- Keep API keys out of `auth.json` when using a relay provider.
- Prefer complete prompts with concrete target files, expected output, and validation steps.
- Add or update the relay provider config in the correct top-level TOML area, without disturbing unrelated Codex settings.
- Use placeholders in public examples. Do not commit real API keys, local tokens, or machine-specific paths.

## Quick Start

Copy the prompt in [prompts/configure-relay-api-key.md](prompts/configure-relay-api-key.md), replace:

- `https://替换为中转站地址`
- `sk-替换为中转站apikey`

Then run it in a Codex session that has local filesystem access.

## Privacy Check

This repository is intended to contain reusable templates only. Before publishing or sharing changes, check that examples still use placeholders instead of real secrets.

Common sensitive values to avoid:

- Real API keys such as `sk-...`
- GitHub tokens such as `ghp_...` or `gho_...`
- Private relay domains if you do not want them public
- Local absolute paths that expose usernames or internal project names

---

## 中文

Codex 本地使用优化指南，收集可复用的 prompt、配置模板和工作流说明。

## 内容

- `docs/` - 具体任务的说明文档和操作记录
- `prompts/` - 可以直接复制到 Codex 使用的完整 prompt
- `templates/` - 可复用配置片段

## 当前指南

- [使用中转站 API Key 配置 Codex](docs/codex-relay-api-key.md)

## 原则

- 配置改动要明确、可回退。
- 使用中转站时，不把 API Key 放进 `auth.json`。
- prompt 尽量完整，包含目标文件、期望结果和验证步骤。
- 在 `~/.codex/config.toml` 的正确顶层配置区域增加或更新中转 provider 配置，不影响其它 Codex 配置。
- 公开示例只使用占位符，不提交真实 API Key、本地 token 或机器相关路径。

## 快速开始

复制 [prompts/configure-relay-api-key.md](prompts/configure-relay-api-key.md) 中的 prompt，并替换：

- `https://替换为中转站地址`
- `sk-替换为中转站apikey`

然后在具备本地文件访问权限的 Codex 会话中运行。

## 隐私检查

这个仓库应该只保存可复用模板。发布或分享前，确认示例里仍然使用占位符，而不是真实密钥。

需要避免提交的敏感信息：

- 真实 API Key，例如 `sk-...`
- GitHub token，例如 `ghp_...` 或 `gho_...`
- 不希望公开的私有中转域名
- 暴露用户名或内部项目名的本地绝对路径
