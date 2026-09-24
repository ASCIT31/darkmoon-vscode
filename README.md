# Darkmoon for VS Code

Browse [Darkmoon](https://dark-moon.org) penetration-test **campaigns**, **vulnerabilities** and **reports** without leaving your editor. One extension, both editions:

- **Darkmoon OSS** — reads local campaign / findings / report artifacts produced by the CLI.
- **Darkmoon Pro** — talks to the Pro REST API.

The extension consumes the shared `@darkmoon/client` contract, so the same UI works across versions and degrades gracefully when a capability is not available.

## Features

- **Campaigns** — a tree of your campaigns with status, overall risk, severity breakdown, dispatched agents and their findings.
- **Vulnerabilities** — a rich table with **filter** (severity, status), **search** and **column sort** (severity, title/type, target/component, status, campaign).
- **Finding detail** — description, evidence (commands, request/response, logs) and remediation.
- **Reports** — Markdown preview of assessment reports.
- **Launch campaign** — start an assessment against a target you are authorised to test.

## Privacy & safety

- Reports and findings are shown **redacted by default**. Real infrastructure values (IPs, hosts, credentials, tokens) are revealed only on an **explicit, local** action, and never over a remote/untrusted workbench.
- Tokens and license keys are stored in the OS secret store (VS Code **SecretStorage**), never in `settings.json` and never logged.
- Webviews run under a strict Content-Security-Policy with no remote content.

## Capability boundary (OSS vs Pro)

Some capabilities are Pro-only and are hidden/disabled automatically on OSS (e.g. live status of running campaigns, the hosted web dashboard). This extension does **not** include an infrastructure graph or any automated pull-request feature.

## Configuration

| Setting | Description |
| --- | --- |
| `darkmoon.mode` | `auto` \| `oss` \| `pro` |
| `darkmoon.baseUrl` | Pro REST base URL (use `https`) |
| `darkmoon.dataDir` | OSS artifacts directory |
| `darkmoon.cliPath` | OSS CLI entrypoint (for launching campaigns) |
| `darkmoon.reports.redactByDefault` | Redact sensitive values until revealed |
| `darkmoon.dev.useFixtures` | Demo mode with bundled sample data |

Set secrets via the commands **Darkmoon: Set Pro API Token** and **Darkmoon: Set License Key**.

## Development

```bash
npm install
npm run compile        # bundle to dist/ (esbuild)
npm test               # headless integration + unit tests (@vscode/test-cli)
npx @vscode/vsce package   # produce the .vsix
```

## License

Proprietary — © ASC SARL. See [LICENSE](LICENSE).
