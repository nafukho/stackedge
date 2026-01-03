
### Stackedge

<div align="center">
  <img src="/download.jfif" alt="Stackedge Logo" width="200"/>
</div>

[![npm version](https://img.shields.io/badge/npm-v0.0.0-lightgrey)](https://www.npmjs.com/) [![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Decentralized app hosting on Android using Termux + Tor. Run web apps (Node.js, PHP, Go, Python, etc.) from your device and expose them via Tor onion services.

Quick links: Installation · Quick Start · Commands · Configuration · Troubleshooting · Contributing

---

## Quick Start

1. Clone and install:

```bash
cd $HOME
git clone https://github.com/Frost-bit-star/stackedge.git
cd stackedge
npm install -g .
```

2. Start an app from the app directory:

```bash
cd ~/my-react-app
stackedge start blog -- npm start
```

The app starts immediately; Tor will bootstrap in the background and the onion address appears when ready.

---

## Installation

- Requirements: Android device with Termux and recommended packages:

```bash
pkg update && pkg upgrade -y
pkg install nodejs git tor -y
# optional
pkg install php golang python -y
```

- Install globally via npm (from repo root):

```bash
npm install -g .
```

Verify with `stackedge` to see the status summary and available commands.

---

## CLI Commands

- `stackedge start <name> -- <command>` — start app named `<name>` (everything after `--` is executed).
- `stackedge stop <name>` — stop the app.
- `stackedge restart <name>` — restart the app.
- `stackedge list` — list apps, state, ports and onion addresses.
- `stackedge resurrect` — restore apps after Termux restart or network issues.

Examples:

```bash
stackedge start blog -- npm start
stackedge stop blog
stackedge list
stackedge resurrect
```

---

## Configuration & Data

Stackedge stores runtime state under `$HOME/.stackedge/`:

```
$HOME/.stackedge/
 ├── apps.json       # registered apps and metadata
 ├── tor/
 │   ├── torrc
 │   └── services/   # onion services
 └── logs/           # app and tor logs
```

Minimal `apps.json` example (auto-managed):

```json
{
  "blog": {
    "cwd": "/data/data/com.termux/files/home/my-react-app",
    "cmd": "npm start",
    "port": 3000
  }
}
```

See `lib/config.js` for configurable defaults.

---

## Termux Auto-Resurrect

To automatically resurrect apps when Termux starts, add this to your shell config:

```bash
echo 'if command -v stackedge >/dev/null; then stackedge resurrect >/dev/null 2>&1 & fi' >> ~/.bashrc
```

---

## Tor & Troubleshooting

- Logs: check `$HOME/.stackedge/logs/` for app and Tor logs.
- If Tor doesn't bootstrap, verify Tor is installed and inspect `tor/log` inside the `.stackedge` directory.
- Common fixes: ensure storage permissions in Termux, restart Tor, or re-run `stackedge resurrect`.

If you still see issues, open an issue with logs attached.

---

## Examples

Create an `examples/` folder (recommended) with small sample apps and start commands for Node, PHP, Python, and Go to help new users.

---

## Contributing

Contributions welcome. Please:

- Fork the repo and open a PR with a clear description.
- Run linters/tests (if added) before submitting.
- Use concise commits and reference issues.

See `CONTRIBUTING.md` for more (create one if you want a template).

---

## Security

Report security issues via a private issue or email. Do not post sensitive details publicly.

---

## Support

If you find Stackedge useful, consider sponsoring or buying a coffee.

---

## License

MIT License — see `LICENSE`.
