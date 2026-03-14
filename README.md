# mantis-sample-app

A deliberately vulnerable LLM-powered app for demonstrating [Mantis](https://github.com/farhanashrafdev/mantis) AI red-team scanning in CI/CD.

> **Warning** — This app is intentionally insecure. Do not deploy to production.

## Vulnerabilities

This sample app contains intentional security flaws that Mantis can detect:

| Category | What it does |
|---|---|
| Prompt Injection | Leaks system prompt when asked to "ignore instructions" |
| Data Leakage | Exposes secrets/API keys on direct request |
| Hallucination | Fabricates citation URLs |
| Tool Exploit | Pretends to execute arbitrary commands |

## Quick Start

```bash
npm install
node index.js
```

The app runs on `http://localhost:3001` with:
- `POST /api/chat` — chat endpoint (accepts `{ "prompt": "..." }`)
- `GET /health` — health check

## Scanning with Mantis

```bash
npm install -g mantis-ai
mantis scan --target http://localhost:3001/api/chat
```

## CI/CD Integration

This repo includes a GitHub Actions workflow (`.github/workflows/mantis-scan.yml`) that:

1. Starts the sample app
2. Installs Mantis from npm
3. Runs a full red-team scan
4. Uploads SARIF results to the GitHub Security tab

Use this as a reference for adding Mantis to your own project's pipeline.

## License

MIT
