# Connect an Assistant (MCP)

Presay is also a remote [MCP](https://modelcontextprotocol.io) server. Claude, ChatGPT, Cursor, VS Code and other assistants can run studies, read reports and manage audiences and drafts on your behalf, **inside your own study allowance**.

```
https://mcp.presay.hyver.app/mcp
```

You need a Presay account first. The assistant asks you to sign in with it and approve access. You can disconnect it at any time.

## Connect

| Client | How |
| --- | --- |
| **Claude** (web, desktop) | Settings, Connectors, Add custom connector, paste the URL |
| **Claude Code** | `claude mcp add --transport http presay https://mcp.presay.hyver.app/mcp`, then `/mcp` to sign in |
| **VS Code** (Copilot agent mode) | `code --add-mcp '{"name":"presay","type":"http","url":"https://mcp.presay.hyver.app/mcp"}'` |
| **Cursor** | Add `{"mcpServers": {"presay": {"url": "https://mcp.presay.hyver.app/mcp"}}}` to `~/.cursor/mcp.json`, then choose **Needs login** |
| **Gemini CLI** | `gemini mcp add --transport http presay https://mcp.presay.hyver.app/mcp`, then `/mcp auth presay` |
| **Other clients** | Transport **Streamable HTTP** at the URL above, auth **OAuth 2.1 with PKCE**. Discovery is automatic. |

Client menus change between versions. **Settings, AI agents** in the web app has current step-by-step instructions with copy buttons, a test prompt and a **Connected** confirmation.

## First run

1. Connect the assistant.
2. Ask: "List my Presay audiences". This checks the sign-in.
3. Ask: "Run a study of this headline on US adults, 20 respondents", then "Show me the report".

A study takes a minute or two. The assistant checks on it until it completes.

## What the assistant can do

| Area | Tools |
| --- | --- |
| **Studies** | `create_study`, `get_study`, `get_study_runs`, `get_report`, `list_studies`, `rename_study`, `delete_study` |
| **Sharing** | `share_study`, `unshare_study` |
| **Audiences** | `list_audience_templates`, `list_audiences`, `create_audience`, `delete_audience`, `compare_audience` |
| **Drafts** | `create_revision`, `get_revision`, `list_revisions`, `compare_revision`, `improve_and_retest` |
| **Uploads and usage** | `create_media_upload`, `get_usage` |

An assistant can request read-only access, in which case it can use only the tools that read.

## Limits

- Studies the assistant starts use **your** weekly and daily allowance, the same as the website.
- A burst of parallel studies may be queued. Retry in a few seconds.
- Sessions end after 90 days; sign in again from the client.
- After too many wrong passwords on sign-in, wait 15 minutes or reset your password on the website.

## Disconnect

Remove the connection under **Settings, AI agents**. The assistant loses access immediately.

> The respondents are simulated. An assistant reporting a result is relaying a directional signal, not measured demand.
