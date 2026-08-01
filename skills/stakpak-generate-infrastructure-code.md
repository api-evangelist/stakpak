---
name: Generate infrastructure code with Stakpak
description: Use Stakpak's OpenAI-compatible chat completion and MCP endpoints to generate Terraform, Kubernetes, Dockerfile, and GitHub Actions code.
api: openapi/stakpak-openapi-original.yml
operations: [chat_completion_handler, mcp_handler, cancel_request_handler]
---

# Generate infrastructure code with Stakpak

Stakpak generates infrastructure code (Terraform, Kubernetes, Dockerfile, GitHub Actions) through an
OpenAI-compatible chat endpoint and an MCP endpoint.

## Auth
Send `Authorization: Bearer <STAKPAK_API_KEY>` on every request.

## Steps
1. **Chat completion** — `POST /v1/chat/completions` (`chat_completion_handler`). OpenAI-compatible request/response; describe the infrastructure you want.
2. **MCP** — `POST /v1/mcp` (`mcp_handler`) exposes the `generate_infrastructure_code` tool for MCP clients. Alternatively run `npx @stakpak/mcp@latest` or `stakpak mcp start` locally (see `mcp/stakpak-mcp.yml`).
3. **Cancel** — `POST /v1/chat/requests/{request_id}/cancel` (`cancel_request_handler`) to stop an in-flight request.

## Rules
- The chat endpoint mirrors OpenAI semantics; reuse OpenAI SDKs by pointing the base URL at `https://apiv2.stakpak.dev/v1`.
- See `conventions/stakpak-conventions.yml` for auth and pagination details.
