# CookieCloud Community for Firefox — AMO Build Instructions

This repository contains only the Firefox extension source and the files required to reproduce the package submitted to Mozilla Add-ons (AMO).

## Environment

- Ubuntu 24.04 LTS or another recent Linux distribution
- Node.js 22.x
- pnpm 10.28.0
- Network access to the npm registry during dependency installation

The package-manager version is pinned in `package.json`; JavaScript dependencies are locked in `pnpm-lock.yaml`.

## Build

Run from the repository root:

```bash
cd ext
corepack enable
corepack prepare pnpm@10.28.0 --activate
pnpm install --frozen-lockfile
pnpm compile
pnpm zip
```

The unsigned Firefox package is written to:

```text
ext/dist/*firefox*.zip
```

## Source contents

The submitted source archive includes:

- Firefox background and content scripts;
- React popup/settings UI;
- localization and icon assets;
- WXT, TypeScript, PostCSS and Tailwind configuration;
- `package.json` and `pnpm-lock.yaml`;
- this reproducible-build document;
- README, privacy notice and GPL-3.0 license.

It excludes generated output, `node_modules`, server-side code, Chromium-specific release tooling, SDKs and unrelated scaffolding.

## Verification

`.github/workflows/build-firefox.yml` performs the same build and verifies:

- extension version `1.0.4`;
- add-on ID `cookiecloud-firefox@neoheee.github.io`;
- Firefox Android minimum version `120.0`;
- required data categories `websiteContent` and `browsingActivity`;
- Mozilla `web-ext lint` results;
- generation of the unsigned Firefox package and AMO source archive.

No API keys, environment variables, private services or remote runtime code are required.
