# Perspective

Follow the people you trust. [Perspective](https://useperspective.com) consumes their podcasts, YouTube videos and
newsletters, so your agent can tell you what they said about whatever you're thinking about, and it widens what you
follow over time.

This plugin connects your agent to Perspective's MCP server (`https://useperspective.com/mcp`) and adds skills for
following people, asking what they've said, and growing your library. Signing in the first time creates your
Perspective account.

## Install

**Claude Code**

```
/plugin marketplace add scalpels-app/perspective
/plugin install perspective@scalpels
```

Then run `/mcp` and sign in to Perspective.

**Claude (desktop and claude.ai)**: Customize → Plugins → Add → Add marketplace → `scalpels-app/perspective`, install
Perspective, then connect it on the plugin's Connectors tab.

**Codex**

```
codex plugin marketplace add scalpels-app/perspective
```

Then install Perspective from `/plugins`.

**Any other MCP client**: add `https://useperspective.com/mcp` as a remote MCP server.

## Skills

| Skill | What it does |
|---|---|
| `following-people` | Turns "follow Jason Cohen" into everything he publishes now, skipping finished shows and namesakes. |
| `asking-perspective` | Answers "what are my people saying about X?" with who said what, when, and links to the moment. |
| `growing-the-library` | Notices the people your sources talk about and offers them, one at a time, when relevant. |
| `getting-started` | First-run setup, newsletters and billing. |

## Development

The skills drive tools on the Perspective server (in `artisan-build/useperspective.com`). Validate with
`claude plugin validate .`, and try it locally with `claude --plugin-dir .`.
