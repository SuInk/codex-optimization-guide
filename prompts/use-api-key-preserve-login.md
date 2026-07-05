# Use an API Key While Preserving Codex Login State

Configure local Codex so model requests use an API key, while the existing ChatGPT/Codex login state remains available for Codex plugins, connectors, and mobile control features.

## Goal

- Use an API key for model requests.
- Keep Codex logged in.
- Preserve `auth.json` login fields such as `tokens` and `last_refresh`.
- Do not store the API key in `auth.json` as `OPENAI_API_KEY`.
- Store the API key in the active model provider config.

## Files

### 1. Handle `~/.codex/auth.json`

Do not rewrite the whole file. Only ensure these two fields are set:

```json
{
  "auth_mode": "chatgpt",
  "OPENAI_API_KEY": null
}
```

If the file already contains `tokens`, `last_refresh`, or other login-related fields, keep them. These fields are required for login-dependent Codex features.

### 2. Handle `~/.codex/config.toml`

Keep the existing active provider unless I explicitly ask to change it.

If the active provider is `OpenAI`, the relevant section should contain an API key like this:

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

## Acceptance

`~/.codex/auth.json` should at least contain:

```json
{
  "auth_mode": "chatgpt",
  "OPENAI_API_KEY": null
}
```

Other existing login fields may remain.

The active provider in `~/.codex/config.toml` should contain:

```toml
experimental_bearer_token = "sk-your-api-key"
```

The final result should allow Codex to use the API key for model requests while keeping login-dependent features available.
