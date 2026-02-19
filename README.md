# GitHits Claude Code Plugin

Search GitHub repositories and code directly from Claude Code using the [GitHits](https://githits.com) MCP server. Find code examples, explore repositories, and discover solutions without leaving your coding session.

## Installation

### From the Official Anthropic Plugin Directory

```
/plugin install githits
```

### From GitHub

```
/plugin install github:githits/githits-claude-code-plugin
```

## Commands

| Command | Description |
|---|---|
| `/githits:search <query>` | Search GitHub repositories and code |
| `/githits:login` | Log in to your GitHits account |
| `/githits:logout` | Log out of your GitHits account |
| `/githits:help` | Show available commands and usage |

## How It Works

This plugin connects to the GitHits MCP server (`@githits/mcp`) via npx, giving Claude Code the ability to search GitHub repositories and code on your behalf. When you run a search command or ask Claude to find code, the plugin routes the request through the GitHits API and returns relevant results directly in your session.

## License

MIT