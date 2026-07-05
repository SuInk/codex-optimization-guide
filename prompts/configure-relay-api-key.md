# Configure Codex Relay API Key

You are a local configuration assistant. Configure Codex to use a relay API key.

## Goal

- The relay API key uses the `sk-...` format.
- Requests should use the OpenAI Responses API.
- Requests should use a custom relay `base_url`.
- Do not store the API key in `auth.json` as `OPENAI_API_KEY`.

## Files

### 1. Handle `~/.codex/auth.json`

Do not rewrite the whole file. Only ensure these two fields are set:

```json
{
  "auth_mode": "chatgpt",
  "OPENAI_API_KEY": null
}
```

If the file already contains `tokens`, `last_refresh`, or other fields, keep them.

### 2. Add relay config in `~/.codex/config.toml`

Add or confirm this top-level field:

```toml
model_provider = "OpenAI"
```

Then add or update this provider section:

```toml
[model_providers.OpenAI]
name = "OpenAI"
base_url = "https://replace-with-relay-base-url"
wire_api = "responses"
experimental_bearer_token = "sk-replace-with-relay-api-key"
requires_openai_auth = true
```

## Requirements

- If `[model_providers.OpenAI]` already exists, update that section instead of creating a duplicate.
- Do not paste the whole `[model_providers.OpenAI]` table at the first line of an existing TOML file. TOML keys after a table header belong to that table until the next table header.
- Keep `model_provider = "OpenAI"` in the top-level config area.
- Keep `[model_providers.OpenAI]` as its own section.
- Preserve unrelated `config.toml` settings.
- Do not write the API key back to `auth.json`.
- Do not delete existing login tokens or other fields from `auth.json`.
- After editing, read the files back and confirm the key fields.
- Finally, remind me to restart Codex or open a new session so the config reloads.

## Acceptance

`~/.codex/auth.json` should at least contain:

```json
{
  "auth_mode": "chatgpt",
  "OPENAI_API_KEY": null
}
```

Other existing fields may remain.

`~/.codex/config.toml` should contain:

```toml
model_provider = "OpenAI"

[model_providers.OpenAI]
name = "OpenAI"
base_url = "https://your-relay-base-url"
wire_api = "responses"
experimental_bearer_token = "sk-your-relay-api-key"
requires_openai_auth = true
```
