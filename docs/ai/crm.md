# Integrations: Salesforce and other apps

Presay's MCP server is at:

```
https://mcp.presay.hyver.app/mcp
```

This page is for apps that ask for a **client ID and secret** before they will connect to an MCP server, such as Salesforce. **HubSpot works differently and is much simpler:** see [Connect Presay in HubSpot](/ai/hubspot.md). For assistants such as Claude, ChatGPT, Cursor or VS Code, which register themselves, see [Connect an Assistant (MCP)](/ai/mcp.md).

> **Status: Salesforce is not supported yet.** Presay's side is built and was tested end to end on production, but we have **not** connected a real Salesforce org, and Salesforce's rules raise open questions about our tools (see [Known risks](#known-risks-with-salesforce)). Use this page to evaluate it, not as a finished setup guide. If you need Salesforce, email [support@hyver.app](mailto:support@hyver.app).

## What Salesforce requires

From Salesforce Help ("MCP for Agentforce", checked 24 November 2026):

- The server must use the **Streamable HTTP** transport. Presay does.
- If the server uses authentication, it must be **OAuth 2.0 client credentials**. Salesforce also supports a **per-user** option through a Salesforce *external credential* (browser flow). Basic, JWT and API-key styles are planned, "but aren't yet available".
- You need **Enterprise, Performance, Unlimited or Developer Edition**, Einstein generative AI set up, and an **Agentforce Service or Agentforce Employee** agent built in the new Agentforce Builder (the legacy builder is not supported).
- Only an MCP server's **tools** are used, not its prompts or resources. Each MCP tool action is billed like any other agent action.

## Two ways to connect

| | **A. OAuth 2.0 (client credentials)** | **B. Per-user external credential** |
| --- | --- | --- |
| Who Presay sees | One Presay account: **the person who created the integration**. Everyone using the agent acts as them and spends their allowance | Each Salesforce user signs in with their **own** Presay account |
| Agents | Agentforce Service and Employee | **Agentforce Employee only** |
| Setup | Short: one form in Salesforce | Long: an external auth identity provider and credential in Salesforce, and each user allows access |
| Fits many users in one org | Only as a shared service account | Yes |

## A. OAuth 2.0 (client credentials)

1. In Presay, open **Settings, AI agents, Integrations**, choose **Salesforce**, tick **Service account** and choose **Read only** (or read and write), then **Create integration**. Copy the client ID and secret now: the secret is shown once.
2. In Salesforce **Setup**, search for **Agentforce Registry**, choose **New**, and register a server from scratch.
3. Enter these values:

   | Field | Value |
   | --- | --- |
   | Server name, description | `Presay`, and a one-line description |
   | URL | `https://mcp.presay.hyver.app/mcp` |
   | Authentication method | **OAuth 2.0** |
   | Identity Provider URL | `https://mcp.presay.hyver.app/oauth/token` (Presay's **token** endpoint; Salesforce's own example uses a token URL here) |
   | Scope | `presay:read` (or `presay:read,presay:write`), comma-separated as Salesforce asks |
   | Client ID, client secret | From step 1 |

   The Presay panel shows `https://mcp.presay.hyver.app` as the identity provider URL. For Salesforce, use the token URL above.
4. Choose **Create and Continue**. Salesforce pings the server, then lists its tools. **Allowlist only the tools you want.**
5. In **Agentforce Builder**, open the agent, pick a topic, **This Topic's Actions**, **Add from Asset Library**, and add the Presay tools. Start with the read-only ones.
6. Ask the agent: "List my Presay audiences."

Treat the secret like a password. Disconnect or delete the integration in Presay at any time: access ends at once.

## B. Per-user external credential

Salesforce documents this as: create an external credential (OAuth, browser flow), register the server with **Use External Credential**, then each user opens **My Personal Information, External Credentials** and chooses **Allow Access**. For Presay, the pieces are:

| Salesforce asks for | Presay value |
| --- | --- |
| Authorization URL | `https://mcp.presay.hyver.app/oauth/authorize` |
| Token URL | `https://mcp.presay.hyver.app/oauth/token` |
| Client ID and secret | From **Settings, AI agents, Integrations** (Salesforce, without Service account) |
| Scopes | `presay:read presay:write` |
| PKCE | Presay accepts it and also works without it for an integration that has a secret |

Salesforce then shows a **callback URL** for the identity provider. Add it in Presay under **Callback URLs** for that integration. We have not run this flow in a real org, so some labels and the callback URL format may differ.

## Known risks with Salesforce

We checked Presay's tools against Salesforce's published limits. These are **unverified** until a real org confirms them:

- **Tool names.** Salesforce documents tool names as up to 128 characters from letters, digits, `.`, `/` and `-`. Presay's 21 tools use underscores (`create_study`, `get_report`). If Salesforce enforces that list, no Presay tool can be used until we offer Salesforce-compatible names.
- **Long descriptions.** Salesforce says properties must be 255 characters or less. Four of our tool descriptions are longer (about 400 to 630 characters).
- **Nested results.** Agentforce Builder handles flat results best. Presay reports are nested, so the agent can use them but may not store them in variables.
- **Timeouts.** Salesforce stops waiting after 60 seconds. Presay starts a study and returns at once, so this should be fine.

## OAuth or API key?

**OAuth.** Presay has no API key or personal access token, on purpose. Salesforce does not offer API-key authentication for MCP servers yet. A service account (option A) is the closest thing: a revocable credential you create, limited to the access you choose, with one-hour tokens and no refresh token. It shows under **Connected assistants** as "(service account)", where **Disconnect** ends it.

## Other apps

For any other app that asks for an OAuth client for an MCP server: choose **Other app**, create the integration, and give the app the client ID, the secret if shown, the server URL, and the **token** and **authorization** URLs above. Add the callback URL the app shows under **Callback URLs**. Presay supports the authorization-code flow with PKCE (or a secret), refresh tokens, and client credentials for a service account.

## Safety and control

- Only you can create, edit or delete integrations, in the web app. An assistant connected through MCP cannot.
- Secrets are stored only as a hash. Deleting an integration stops its connections from refreshing at once; tokens already issued last up to an hour, except a service account's, which stop immediately.
- Callback URLs must be plain `https` addresses. The sign-in page shows people which app is asking and where it will send them.

## Until Salesforce works

The study loop still fits a Salesforce workflow:

- Run the study in the [web app](/getting-started/first-study.md) or through an [assistant](/ai/mcp.md), then paste the [shared report link](/reports/share-export.md) into the Salesforce record.
- Export the report as PDF, Word or JSON and attach it. See [Share & Export](/reports/share-export.md).

> The respondents are simulated. Whatever an agent reports back is a directional signal, not measured demand. See [Limits of Synthetic Research](/limits.md).
