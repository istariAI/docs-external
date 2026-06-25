# API Reference spec

`openapi.json` is the OpenAPI document that powers the interactive API playground
under the **API & MCP → API Reference** group in `docs.json`.

**Do not edit it by hand.** It is generated from the FastAPI app in the
`istariAI/GOI-Production` repo and kept in sync by the
`.github/workflows/sync-docs-openapi.yml` workflow there, which opens a PR
against this repo whenever the API changes.

The generator (`api/scripts/export_openapi.py` in GOI-Production) sets the public
`https://api.istari.ai/v2` server, strips the internal `/v1` path prefix, and
injects the `x-api-key` security scheme.

## Regenerate manually

From a local `GOI-Production` checkout:

```bash
cd ~/code/GOI-Production/api
PYTHONPATH=. uv run --with-requirements public_api/requirements.txt \
  python scripts/export_openapi.py \
  /path/to/docs-external/api-reference/openapi.json
```
