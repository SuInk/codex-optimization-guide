# Use an API Key While Preserving Codex Login State

Configure local Codex so model requests use an API key, while the existing ChatGPT/Codex login state remains available for Codex plugins, connectors, and mobile control features.

## Goal

- Use an API key for model requests.
- Keep Codex logged in.

## Files to Handle

### 1. Handle `~/.codex/auth.json`

Do not rewrite the whole file. Only modify it to ensure it contains these two fields:

```json
{
  "auth_mode": "chatgpt",
  "OPENAI_API_KEY": null
}
```

If the file already contains `tokens`, `last_refresh`, or other login-related fields, preserve all of them. Do not delete them. These fields are used by Codex features that depend on login state.

### 2. Handle `~/.codex/config.toml`

Add the following content. If these fields already exist, update their formatting and values to match the example below. If I have not provided the model `base_url` or API key, ask me before making changes.

```toml
model_provider = "OpenAI"

[model_providers.OpenAI]
name = "OpenAI"
base_url = "https://replace-with-provider-base-url"
wire_api = "responses"
experimental_bearer_token = "sk-replace-with-api-key"
requires_openai_auth = true
```

## Requirements

- Back up every file before editing.
- Preserve unrelated `config.toml` settings.
- Preserve existing `auth.json` login state.
- Do not delete `tokens`, `last_refresh`, or other login fields from `auth.json`.
- Do not write the API key back to `auth.json`.
- Do not duplicate an existing `[model_providers.*]` section.
- If the provider section already exists, update that existing section.
- Keep provider fields in their proper TOML section. Do not paste a provider table at the first line of an existing TOML file.
- After editing, read the files back and confirm the effective fields.
- Finally, remind me to restart Codex or open a new session so the config reloads.

## Acceptance Criteria

`~/.codex/auth.json` should at least contain:

```json
{
  "auth_mode": "chatgpt",
  "OPENAI_API_KEY": null
}
```

Other existing login fields may remain.

The currently active provider in `~/.codex/config.toml` should contain:

```toml
model_provider = "OpenAI"

[model_providers.OpenAI]
name = "OpenAI"
base_url = "https://replace-with-provider-base-url"
wire_api = "responses"
experimental_bearer_token = "sk-replace-with-api-key"
requires_openai_auth = true
```

The final result should allow Codex model requests to use the API key while plugins, connectors, mobile control, and other features that depend on login state remain available.
