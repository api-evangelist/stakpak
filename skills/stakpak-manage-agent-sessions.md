---
name: Manage Stakpak agent sessions
description: List agent sessions, inspect a session's details and its latest checkpoint, and read usage stats.
api: openapi/stakpak-openapi-original.yml
operations: [get_agent_sessions_handler, get_agent_session_handler, get_agent_session_latest_checkpoint_handler, get_agent_session_stats_handler]
---

# Manage Stakpak agent sessions

Use the Stakpak API (`https://apiv2.stakpak.dev`) to observe autonomous agent runs.

## Auth
Send `Authorization: Bearer <STAKPAK_API_KEY>` on every request (see `authentication/stakpak-authentication.yml`).

## Steps
1. **List sessions** — `GET /v1/agents/sessions` (`get_agent_sessions_handler`). Page with `limit` and `offset` query params.
2. **Get a session** — `GET /v1/agents/sessions/{session_id}` (`get_agent_session_handler`) for full details.
3. **Latest checkpoint** — `GET /v1/agents/sessions/{session_id}/checkpoints/latest` (`get_agent_session_latest_checkpoint_handler`) to see current agent state.
4. **Usage stats** — `GET /v1/agents/sessions/{session_id}/stats` (`get_agent_session_stats_handler`).

## Rules
- Errors are HTTP-status based (see `errors/stakpak-problem-types.yml`); 404 means the session id is wrong, 401 a bad token.
- No idempotency keys; these are read operations so retries are safe.
