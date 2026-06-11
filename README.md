# ISTARI.AI Documentation (Mintlify)

Public documentation for [ISTARI.AI](https://www.istari.ai), hosted at [docs.istari.ai](https://docs.istari.ai).

This repository is the **Mintlify** docs source. Content is migrated from [istari-docs-external](https://github.com/istariAI/istari-docs-external), which continues to use MkDocs + Cloud Run.

## Local development

Install the [Mintlify CLI](https://www.mintlify.com/docs/development) and run from the repo root:

```bash
npm i -g mint
mint dev
```

Preview at [http://localhost:3000](http://localhost:3000).

## Publishing

Connect this repository in the [Mintlify dashboard](https://dashboard.mintlify.com) and install the GitHub App. Pushes to `main` deploy automatically.

No monorepo path is needed — `docs.json` lives at the repository root.

## Structure

- `docs.json` — site config and navigation
- `.mintlify/Assistant.md` — AI assistant instructions (not published)
- `goi/`, `api/`, `mcp/`, `research-data/`, `tools/` — documentation pages
- `images/` — screenshots and assets

## Support

Questions: [support@istari.ai](mailto:support@istari.ai)
