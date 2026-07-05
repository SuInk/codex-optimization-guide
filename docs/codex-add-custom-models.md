# Add Custom Models to the Codex Local Catalog

English | [中文](#中文)

This guide describes how to add custom model entries to the local Codex model catalog while reusing the existing provider configuration.

## Table of Contents

- [Target](#target)
- [Files](#files)
- [Backup](#backup)
- [Catalog Rules](#catalog-rules)
- [Validation](#validation)
- [Fallback](#fallback)
- [中文](#中文)
- [目录](#目录)
- [目标](#目标)
- [文件](#文件)
- [备份](#备份)
- [Catalog 规则](#catalog-规则)
- [验证](#验证)
- [兜底方案](#兜底方案)

## Target

Add these models to the local Codex model menu:

- `deepseek-v4-flash`
- `deepseek-v4-pro`

Both models should use the existing provider already configured in `~/.codex/config.toml`.

## Files

Typical files involved:

- `~/.codex/config.toml`
- `~/.codex/models_cache.json`

Do not hard-code a machine-specific path in reusable documentation or prompts.

## Backup

Before editing, create timestamped backups of every file that will be modified.

Example backup names:

- `config.toml.bak-YYYYMMDD-HHMMSS`
- `models_cache.json.bak-YYYYMMDD-HHMMSS`

## Catalog Rules

- Do not modify the existing provider.
- Do not modify `model_provider`.
- Do not modify any `[model_providers.*]` section.
- Do not modify `base_url`.
- Do not modify any token or API key.
- Insert the new models after the existing GPT model entries and before `codex-auto-review`.
- Use the real model name for both `display_name` and `slug`.
- Reuse the same provider value or provider reference used by the existing catalog entries.
- Preserve the existing `models_cache.json` schema instead of inventing a new structure.
- Set default reasoning to `medium`.
- Do not use `none` or `max` for reasoning values.
- Only use Codex local catalog reasoning levels:
  - `low`
  - `medium`
  - `high`
  - `xhigh`

## Validation

After editing, verify with `codex debug models` or an equivalent command that reads the same local catalog Codex uses.

Confirm all of the following:

- `deepseek-v4-flash` exists.
- `deepseek-v4-pro` exists.
- Both models appear after the existing GPT models.
- Both models appear before `codex-auto-review`.
- `display_name` matches the model name.
- `slug` matches the model name.
- Default reasoning is `medium`.
- Allowed reasoning levels are `low`, `medium`, `high`, and `xhigh`.

## Fallback

If modifying only `models_cache.json` does not make Codex read the new entries, add this top-level key to `~/.codex/config.toml`:

```toml
model_catalog_json = "~/.codex/models_cache.json"
```

This fallback must not change provider settings, `base_url`, or tokens.

---

## 中文

本教程说明如何在 Codex 本地模型 catalog 中新增自定义模型，同时继续复用现有 provider 配置。

## 目录

- [目标](#目标)
- [文件](#文件)
- [备份](#备份)
- [Catalog 规则](#catalog-规则)
- [验证](#验证)
- [兜底方案](#兜底方案)
- [English](#add-custom-models-to-the-codex-local-catalog)
- [Table of Contents](#table-of-contents)
- [Target](#target)
- [Files](#files)
- [Backup](#backup)
- [Catalog Rules](#catalog-rules)
- [Validation](#validation)
- [Fallback](#fallback)

## 目标

在 Codex 本地模型菜单里新增：

- `deepseek-v4-flash`
- `deepseek-v4-pro`

两个模型都继续使用 `~/.codex/config.toml` 中已经配置好的现有 provider。

## 文件

通常会涉及：

- `~/.codex/config.toml`
- `~/.codex/models_cache.json`

可复用文档和 prompt 中不要写死具体机器路径。

## 备份

修改前，先给所有会改到的文件创建带时间戳的备份。

示例备份名：

- `config.toml.bak-YYYYMMDD-HHMMSS`
- `models_cache.json.bak-YYYYMMDD-HHMMSS`

## Catalog 规则

- 不要修改现有 provider。
- 不要修改 `model_provider`。
- 不要修改任何 `[model_providers.*]` section。
- 不要修改 `base_url`。
- 不要修改任何 token 或 API Key。
- 将新增模型插到现有 GPT 模型后面、`codex-auto-review` 前面。
- `display_name` 和 `slug` 都使用真实模型名。
- 复用已有 catalog 条目使用的 provider 值或 provider 引用。
- 保持 `models_cache.json` 现有 schema，不要凭空发明新结构。
- 默认 reasoning 设置为 `medium`。
- reasoning 不要使用 `none` 或 `max`。
- Codex 本地 catalog reasoning 只使用：
  - `low`
  - `medium`
  - `high`
  - `xhigh`

## 验证

修改后，用 `codex debug models` 或等效命令验证 Codex 实际读取到的本地 catalog。

确认以下内容：

- 存在 `deepseek-v4-flash`。
- 存在 `deepseek-v4-pro`。
- 两个模型都位于现有 GPT 模型后面。
- 两个模型都位于 `codex-auto-review` 前面。
- `display_name` 等于模型名。
- `slug` 等于模型名。
- 默认 reasoning 是 `medium`。
- 可用 reasoning 档位是 `low`、`medium`、`high`、`xhigh`。

## 兜底方案

如果只改 `models_cache.json` 后 Codex 实际菜单没有读取新增模型，可以在 `~/.codex/config.toml` 顶层增加：

```toml
model_catalog_json = "~/.codex/models_cache.json"
```

这个兜底项不能改变 provider、`base_url` 或 token。
