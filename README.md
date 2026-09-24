# Darkmoon for VS Code

Browse [Darkmoon](https://dark-moon.org) penetration-test **campaigns**, **vulnerabilities** and **reports** without leaving your editor. One extension, both editions:

- **Darkmoon OSS** — reads local campaign / findings / report artifacts produced by the CLI.
- **Darkmoon Pro** — talks to the Pro REST API.

The extension consumes the shared `@darkmoon/client` contract, so the same UI works across versions and degrades gracefully when a capability is not available.

## Install

- **Marketplace:** search for **Darkmoon** in the Extensions view and click Install.
- **From VSIX:** `code --install-extension darkmoon-vscode-0.1.0.vsix` (or Extensions view → `...` → *Install from VSIX…*).

## Connect

Open Settings and pick your edition with `darkmoon.mode`:

- **OSS** — set `darkmoon.dataDir` to your Darkmoon settings directory (the tree that holds `campaigns/` and `vulnerabilities/`). Reports are read from `<dataDir>/reports` by default; set `darkmoon.cliPath` to `darkmoon.sh` if you want to launch campaigns from the editor.
- **Pro** — set `darkmoon.baseUrl` to your Pro API (`https://…`, with or without `/api/v1`) and store your JWT via **Darkmoon: Set Pro API Token**.

Then run **Darkmoon: Refresh**. Want a no-backend preview first? Toggle `darkmoon.dev.useFixtures` to load the bundled synthetic *Demo Shop* sample data.

## Use

1. **View findings** — open the **Campaigns** tree (status, overall risk, severity breakdown, agents) and the **Vulnerabilities** table (filter by severity/status, search, sort).
2. **Open a finding** — click a row to see description, redacted evidence and remediation.
3. **Open a report** — **Darkmoon: Open Report** shows the redacted Markdown; **Darkmoon: Open Full Report** reveals real values (local, non-remote workbench only, with a confirmation).

> **CI pass/fail is not decided here.** This extension is browse-only; the findings-based fail policy (`--fail-on`) lives in the `darkmoon-ci` CLI and the CI/CD integrations (GitHub Actions, GitLab, Jenkins).

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
| `darkmoon.dataDir` | OSS artifacts directory (reports are read from `<dataDir>/reports`) |
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

MIT © 2026 ASC-IT (SARL) / Darkmoon. See [LICENSE](LICENSE).
