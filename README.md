# GitHits Claude Code Plugin

Find code examples from global open source directly in Claude Code using
[GitHits](https://githits.com). When you're stuck, need an up-to-date API
example, or encounter an error you can't resolve, GitHits helps find a working
solution in seconds.

## Prerequisites

- Node.js 20 or later
- A [GitHits](https://githits.com) account

Authenticate before installing the plugin:

```
npx -y githits login
```

This opens your browser for secure OAuth authentication. For headless
environments (SSH, CI), use `--no-browser` to get a URL instead, or set the
`GITHITS_API_TOKEN` environment variable.

## Installation

### From the Official Anthropic Plugin Directory

```
/plugin install githits
```

### From GitHub

```
/plugin install github:GitHits-com/githits-claude-code-plugin
```

## Commands

| Command                   | Description                                  |
| ------------------------- | -------------------------------------------- |
| `/githits:search <query>` | Search for code examples from open source    |
| `/githits:login`          | Authenticate with your GitHits account       |
| `/githits:status`         | Show your current authentication status      |
| `/githits:logout`         | Remove stored credentials                    |
| `/githits:help`           | Show available commands and usage             |

> The plugin expects the `githits` CLI to be published on npm. Marketplace
> installs should happen after the CLI package is live.

## How It Works

This plugin connects to the GitHits MCP server via the
[`githits`](https://www.npmjs.com/package/githits) npm package, started with
`npx -y githits mcp start` over stdio. Claude Code gets three tools:

| Tool              | Purpose                                                   |
| ----------------- | --------------------------------------------------------- |
| `search`          | Find code examples by describing what you need            |
| `search_language` | Look up supported programming language names              |
| `feedback`        | Rate search results to improve future quality             |

Claude decides when to call these tools on its own — typically when it's stuck,
needs a working example for an unfamiliar API, or encounters an error it can't
resolve from its training data alone.

### License Filtering

Search results respect license filtering by default, excluding copyleft-licensed
code. Three modes are available:

- **strict** (default) — excludes copyleft licenses
- **yolo** — includes all licenses, no filtering
- **custom** — uses your custom blocklist configured at
  [githits.com](https://githits.com)

## Authentication

GitHits requires authentication. Two options are available:

### Browser Login (recommended)

```
npx -y githits login
```

Tokens are stored locally and refreshed automatically. If a refresh fails, run
the command again.

Useful flags:

- `--no-browser` — prints a URL instead of opening a browser
- `--force` — re-authenticate even if already logged in
- `--port <port>` — use a specific port for the local callback server

### API Token

For CI or headless environments, set an environment variable:

```
export GITHITS_API_TOKEN=your-token-here
```

## License

MIT
