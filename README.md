# GitHits Claude Code Plugin

Find code examples from global open source directly in Claude Code using
[GitHits](https://githits.com). When you're stuck, need an up-to-date API
example, or encounter an error you can't resolve, GitHits helps find a working
solution in seconds.

## Prerequisites

- Node.js 20 or later
- A [GitHits](https://githits.com) account

## Installation

### Quick Install (recommended)

1. Add the GitHits marketplace:
   ```
   /plugin marketplace add GitHits-com/githits-claude-code-plugin
   ```
2. Install the plugin:
   ```
   /plugin install githits@githits-plugins
   ```

## Commands

| Command                   | Description                               |
| ------------------------- | ----------------------------------------- |
| `/githits:search <query>` | Search for code examples from open source |
| `/githits:login`          | Authenticate with your GitHits account    |
| `/githits:status`         | Show your current authentication status   |
| `/githits:logout`         | Remove stored credentials                 |
| `/githits:help`           | Show available commands and usage         |

> The plugin expects the `githits` CLI to be published on npm. Marketplace
> installs should happen after the CLI package is live.

## How It Works

This plugin connects to the GitHits MCP server via the
[`githits`](https://www.npmjs.com/package/githits) npm package, started with
`npx -y githits mcp start` over stdio. Claude Code gets three tools:

| Tool              | Purpose                                        |
| ----------------- | ---------------------------------------------- |
| `search`          | Find code examples by describing what you need |
| `search_language` | Look up supported programming language names   |
| `feedback`        | Rate search results to improve future quality  |

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

GitHits requires authentication. Claude handles login automatically — if your
session isn't authorized, it opens your browser for quick OAuth approval and
retries once you're logged in.

### Manual Login

If you run into issues with automatic login, you can authenticate directly:

```
npx -y githits login
```

This opens your browser for secure OAuth authentication. Tokens are stored
locally and refreshed automatically.

Useful flags:

- `--no-browser` — prints a URL instead of opening a browser (useful for SSH,
  CI, or containers)
- `--force` — re-authenticate even if already logged in
- `--port <port>` — use a specific port for the local callback server

Check your current authentication status:

```
npx -y githits auth status
```

Log out and remove stored credentials:

```
npx -y githits logout
```

### API Token

For CI or headless environments, set an environment variable:

```
export GITHITS_API_TOKEN=your-token-here
```

## Local Development & Testing

### Test the plugin locally

Use the `--plugin-dir` flag to load the plugin without installing it from a
marketplace:

```
claude --plugin-dir ./githits-claude-code-plugin
```

This starts Claude Code with the plugin loaded for that session. You can verify
it loaded by running `/mcp`.

### Test CLI changes locally with `npm link`

To test unpublished `githits-cli` changes with the plugin, link your local build
globally:

```
cd /path/to/githits-cli
bun run build
npm link
githits --version    # verify the linked version
```

Then load the plugin as usual:

```
claude --plugin-dir ./githits-claude-code-plugin
```

## License

MIT
