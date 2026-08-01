---
name: Work with the Stakpak knowledge store
description: Search, read, create, and overwrite knowledge files in the Stakpak knowledge store.
api: openapi/stakpak-openapi-original.yml
operations: [search_handler, read_handler, create_handler, overwrite_handler, delete_handler]
---

# Work with the Stakpak knowledge store

The knowledge store holds files the agent uses as persistent context, addressed by `path`.

## Auth
Send `Authorization: Bearer <STAKPAK_API_KEY>` on every request.

## Steps
1. **Search / list** — `GET /v1/knowledge` (`search_handler`) to list or search knowledge files.
2. **Read** — `GET /v1/knowledge/{path}` (`read_handler`) for the raw bytes; pass `peek=true` for a short preview.
3. **Create** — `POST /v1/knowledge/{path}` (`create_handler`). Returns `409 Conflict` if a file already exists at that path.
4. **Create-or-overwrite** — `PUT /v1/knowledge/{path}` (`overwrite_handler`) when you intend to replace existing content.
5. **Delete** — `DELETE /v1/knowledge/{path}` (`delete_handler`) removes a file or directory (recursive).

## Rules
- Choose `create` vs `overwrite` deliberately: `create` is safe (409 on conflict), `overwrite` is destructive.
- See `conventions/stakpak-conventions.yml` and `errors/stakpak-problem-types.yml`.
